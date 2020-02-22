---
title: "nftablesでdockerを使ってみました"
date: 2020-02-22
---

Linux 3.13 から利用可能な、 iptables を置き換える(ことを目的とした)パケット分類フレームワークの(ファイアーウォール？)
nftables を、 docker を使っている環境で使ってみました。

## インストール・有効化

Docker から使うには、 iptables の互換フロントエンドをインストールする必要があります。
nftables と一緒にインストールするには、以下を実行します。
(`iptables-nft` は `iptables` を置き換えます。)

```shell script
sudo pacman -S nftables iptables-nft
```

`nftables.service` を起動すると、 `/etc/nftables.conf` から設定を読み込みます。
起動・自動的に起動するようにするには、以下を実行します。

```shell script
sudo systemctl enbale --now nftables
```

ArchLinux の nftables パッケージの `etc/nftables.conf` には、
シンプルでセキュアなファイアーウォールが設定されています。
1:0.9.3-1 時点での設定内容は以下の通りです。

```text
#!/usr/bin/nft -f
# ipv4/ipv6 Simple & Safe Firewall
# you can find examples in /usr/share/nftables/

table inet filter {
  chain input {
    type filter hook input priority 0;

    # allow established/related connections
    ct state {established, related} accept

    # early drop of invalid connections
    ct state invalid drop

    # allow from loopback
    iifname lo accept

    # allow icmp
    ip protocol icmp accept
    ip6 nexthdr icmpv6 accept

    # allow ssh
    tcp dport ssh accept

    # everything else
    reject with icmpx type port-unreachable
  }
  chain forward {
    type filter hook forward priority 0;
    drop
  }
  chain output {
    type filter hook output priority 0;
  }

}

# vim:set ts=2 sw=2 et:
```

## Docker を使用するための設定

標準のままだと、 Docker コンテナとの通信は forward チェインのルールにより drop されてしまいます。
docker エンジンによって作成される `DOCKER-USER` チェインのパケットを accept するには、以下のコマンドを実行します。

```shell script
# ip ファミリーに filter テーブルを作成し、 DOCKER-USER チェインを追加する
$ sudo nft add table ip filter                                                                                                                                                                          :(
$ sudo nft add chain ip filter DOCKER-USER
$ sudo nft add rule ip filter DOCKER-USER mark set 1
# inet filter forward の drop ルールの handle を確認する (この場合は `handle 12`)
$ sudo nft list ruleset -a
table inet filter { # handle 25
	chain input { # handle 1
		type filter hook input priority filter; policy accept;
		ct state { established, related } accept # handle 5
		ct state invalid drop # handle 6
		iifname "lo" accept # handle 7
		ip protocol icmp accept # handle 8
		ip6 nexthdr ipv6-icmp accept # handle 9
		tcp dport 22 accept # handle 10
		reject # handle 11
	}

	chain forward { # handle 2
		type filter hook forward priority filter; policy accept;
		drop # handle 12
	}

	chain output { # handle 3
		type filter hook output priority filter; policy accept;
	}
}
table ip filter { # handle 26
	chain DOCKER-USER { # handle 1
		meta mark set 0x00000001 # handle 2
	}
}
# drop ルールの前に insert する(ここの `handle 12` は上で確認した handle に変更してください)
$ sudo nft insert rule inet filter forward handle 12 mark 1 accept
# ルールを /etc/nftables.conf に保存する
$ sudo nft list ruleset | sudo tee /etc/nftables.conf 
table inet filter {
	chain input {
		type filter hook input priority filter; policy accept;
		ct state { established, related } accept
		ct state invalid drop
		iifname "lo" accept
		ip protocol icmp accept
		ip6 nexthdr ipv6-icmp accept
		tcp dport 22 accept
		reject
	}

	chain forward {
		type filter hook forward priority filter; policy accept;
		meta mark 0x00000001 accept
		drop
	}

	chain output {
		type filter hook output priority filter; policy accept;
	}
}
table ip filter {
	chain DOCKER-USER {
		meta mark set 0x00000001
	}
}
```

nftables の設定の保存が完了したら、 `docker.service` を再起動することで
docker によりファイアウォールルールが作成されます。
(docker は iptables フロントエンドを使用するため、 `iptables-nft` パッケージに付属する `iptables` コマンドを使用して
ルールが追加されます。)
念のため `nftables.service` も再起動して、今保存したルールを再読み込みします。

`sudo systemctl restart nftables docker`

`docker.service` が正常に起動したら、 docker のルールが追加され、コンテナとの通信ができるようになっているはずです。

## nftables インストール前の iptables ルールの参照

`iptables` コマンドの代わりに `iptables-legacy` コマンドを使用することで、
iptables で使っていたルールを確認することができます。

docker のルールもこちらからインポートしようかなと思ったのですが、そうすると iptables-nft の互換性が壊れてしまって
docker.service の起動に失敗したので、 ArchWiki の方法に従いました。
