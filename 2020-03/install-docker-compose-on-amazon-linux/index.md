---
title: "AmazonLinux2-minimal に docker-compose をインストールしてみました"
date: 2020-03-23
---

AmazonLinux では、 `amazon-linux-extras` を使って docker は簡単にインストールすることができますが、
`docker-compose` のインストールは少しハマる場合がありました。

`amazon-linux-extras` から epel リポジトリを有効化すると、 yum で docker-compose が利用可能になりますが、
これはアーキテクチャに関わらず現在インストールすることができません(python3.6 系に依存しているため)。

## x86_64
`pip3 install docker-compose` で素直に入ります。特にハマることはないと思います。

## aarch64
x86_64 と同じように `pip3` でインストールはできますが、依存ライブラリのビルドに必要な依存関係を解決しておく必要があります。
以下のコマンドでインストール可能です。

```shell script
yum install gcc libffi-devel openssl-devel python3-devel
pip3 install docker-compose 
```

ビルドが走るので少し時間がかかります。頻繁に使うのであれば AMI を作成しておく方が便利だと思います。

今回は minimal で試しましたが、normal の方では試していないため、また必要になったら試してみようと思います。

といっても、docker-compose を直接インスタンスで使うよりも、最近では ECS や Kubernetes を使うことの方が多そうですね……。
