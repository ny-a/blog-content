---
title: "DNSSEC validation failed エラー"
date: 2020-02-09
---

Raspberry Pi に ArchLinux をインストールして RTC モジュールの設定をしてみたのですがうまくいかず、
DNSSEC のエラーでホスト名の解決ができない問題に遭遇しました。

始めの問題としては、 `pacman -Syu` が通りませんでした。

```shell script
$ sudo pacman -Syu
:: Synchronizing package databases...
error: failed retrieving file 'core.db' from mirror.archlinuxarm.org : Could not resolve host: mirror.archlinuxarm.org
error: failed to update core (invalid url for server)
error: failed retrieving file 'extra.db' from mirror.archlinuxarm.org : Could not resolve host: mirror.archlinuxarm.org
error: failed to update extra (invalid url for server)
error: failed retrieving file 'community.db' from mirror.archlinuxarm.org : Could not resolve host: mirror.archlinuxarm.org
error: failed to update community (invalid url for server)
error: failed retrieving file 'alarm.db' from mirror.archlinuxarm.org : Could not resolve host: mirror.archlinuxarm.org
error: failed to update alarm (invalid url for server)
error: failed retrieving file 'aur.db' from mirror.archlinuxarm.org : Could not resolve host: mirror.archlinuxarm.org
error: failed to update aur (invalid url for server)
error: failed to synchronize all databases

```

`/etc/resolv.conf` の内容は問題なさそうですし、 `systemd-networkd` と `systemd-resolved` も問題なく動いていて、
その2つを restart してみても変わりませんでした。

`dig` コマンドを入れようにも pacman が通らないのですが、 `systemd-resolve` コマンドでホスト名の解決ができるようです。
試してみると、

```shell script
$ systemd-resolve ntp.org
ntp.org: resolve call failed: DNSSEC validation failed: no-signature
```

などと出てホスト名が解決できないようです。
`systemctl status systemd-resolved` を見てみると、他のホスト名も同様にエラーになっています。
(初めの方は `no-signature` ではなく `signature-expired` が出ていました)

[[SOLVED] DNS not working after pacman -Syu](https://archlinuxarm.org/forum/viewtopic.php?f=9&t=13614)
に `systemd-resolved` を止めるという解決方法が書かれていたので試したところ、うまくいきました。

DNSSEC についてあまり詳しくないので、きちんと調べてみようと思いました……。

