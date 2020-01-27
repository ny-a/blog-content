---
title: "grpc-nodeのビルドに失敗する"
date: 2020-01-28
---

[npm install grpc build from source fails](https://github.com/grpc/grpc-node/issues/922)
に書いてある通りなのですが……。

node v13 ではソースからのビルドになってインストールに失敗します。
node v10 を使えばバイナリパッケージがあるようです。

nvm をインストールしてとりあえずの対処をしようと思います。
