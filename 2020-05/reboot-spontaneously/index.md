---
title: "ノート PC が突然勝手に起動するようになっていました"
date: 2020-05-13
---

しばらく放置していたノート PC を久しぶりに起動しようとしたのですが、
電源ボタンを押しても反応がありませんでした。
放置していた期間中ずっと AC アダプタを接続していたので、電源関係の
問題ではないと思ったのですが、一旦電源を外してみたり、再度接続して
充電が完了するまで待ったりしてみても起動しませんでした。

諦めてしばらく電源ボタンを連打していたら、いつのまにか起動していました。
Arch のアップデートなどを済ませて電源を落としたら、今度はなぜか勝手に
起動するようになってしまいました。
しかも、しばらく放置していると勝手に電源が落ちているようでした。
WoL などは設定していないはずで、マジックパケットなども飛んでいないはずですが、
念のため LAN ケーブルを外して電源だけ接続している状態にしても改善しません
でした。

AC アダプタを外したり、閉じた状態にしておけば……と試してみても、一向に
改善しませんでした。
これは電池が空になるまで続くのか……と思っていたのですが、電源を入れたり
切ったりしてみているうちに起きなくなっていました。

今のところどちらの問題も再発はしていないようですが、一体原因は何で、
PC が壊れているのかどうかも分かりませんが、もうしばらく様子を見ようと
思います……。
電源 (少なくとも LED) が消えた状態から勝手に起動するようなロジックが
存在するのでしょうか、それとも外来ノイズか何かでしょうか。

