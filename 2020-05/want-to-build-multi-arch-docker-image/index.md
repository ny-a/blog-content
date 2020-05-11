---
title: "マルチアーキテクチャ対応の Docker イメージを作りたい"
date: 2020-05-11
---

multi-arch 対応の docker image をビルドしたいと思ったのですが、
docker manifest サブコマンドや docker buildx サブコマンドはまだ
experimental な上、manifest を作るには insecure ではない registry
が必要そうで、事前のセットアップが少し大変そうで一旦諦めました。

LAN 内に insecure な registry を立てて遊ぼうと思っていたのですが、
目論見が外れた形ですね。きちんと外部に公開して Let's encrypt で
SSL 対応して、認証も……とやってもいいのですが、今は少し元気が足りず……


