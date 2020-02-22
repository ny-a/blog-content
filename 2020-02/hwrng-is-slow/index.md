---
title: "/dev/randomが遅かったので高速化を試してみました"
date: 2020-02-22
---

ArchLinux をインストールしているノート PC に `rng-tools` をインストールして、
初期設定の状態で `rngd.service` を起動していたのですが、乱数生成が遅く感じたので調べてみました。

## 乱数生成の速度計測

乱数生成の速度の計測は以下のコマンドで行いました。

```shell script
sudo dd if=/dev/random of=/dev/null bs=1 count=1000000 iflag=fullblock status=progress
```

この結果が、前から使っているノート PC では 400kB/s 程度出ていて、
[Rng-tools - ArchWiki](https://wiki.archlinux.org/index.php/Rng-tools)
では 50kB/s 程度出ていれば問題ないと書かれていますが、
新しい方のノート PC では 4kB/s 程度でした。

`/dev` を確認してみると、 `/dev/hwrng` は存在して、 `rngd` もそれを認識して正常に使用しているようでした。
搭載している tpm は 2.0 で、特に tpm 関連のエラーも出ていません。
また、 `lscpu` で確認すると、 `rdrand` `rdseed` 両方のフラグが立っています。

## rngd のソースの優先順位

[rngd(8) の Entropy_Source](https://www.mankier.com/8/rngd#Entropy_Sources)
を見ると、 

1. hwrng
1. tpm
1. rdrand
1. darn
1. nist
1. jitter
1. pkcs11

の順で使用するようです。

## hwrng の無効化

そこで、 `-r /` など、適当なパスを指定して、hwrng を使わないように設定しました。
その結果、 600 kB/s 程度出るようになりました。

hwrng の方が品質がよさそうですが、普段そこまでエントロピーの品質を気にしない場面においては、
速度が出る方が便利そうだと思い今回はこのように設定しました。
GPG キーなんかを作るときは hwrng を使った方がよさそうですが、そもそもノート PC などインターネットに接続された
マシンよりも、専用に用意したオフラインのマシンを使用する方が安全だと思うので、ほとんどの場面において
問題なさそうです。
