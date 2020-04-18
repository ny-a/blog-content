---
title: "Gatsby のビルドが落ちていたので直しました"
date: 2020-04-19
---

node 13.13 に上がってから babel を 7.9.0 に上げるまでの間、ビルドが
落ちていました。

node 13.12 に下げてみた後、babel を 7.9.0`に上げて解決しました。

[babel/babel #11427](https://github.com/babel/babel/issues/11427)
あたりを参考にしました。

……gridsome も落ちてるんですが、そもそも放置しているので何とかしたい……

