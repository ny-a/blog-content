---
title: "RPi の MAC アドレスを電源を入れないで確認したい"
date: 2020-04-30
---

RPi がたくさんあると MAC アドレスや固体の識別できる情報を
電源がなくても(ハードウェアの見た目のみで)確認したくなったり
すると思うのですが、調べてみた限りではそのような方法は
なさそうでした……。

MAC アドレスは EEPROM ではなく CPU のシリアル No を使っている
ようなので、CPU の情報が基板に記載されていれば……
その可能性は低そうですね。

唯一？あるのは製造番号らしき16桁の番号の入ったデータマトリクスと、
いくつかの日付のような印字のみでしょうか。
このあたりの情報も出ていれば嬉しいのですが、まあ誰も
データマトリクスなんて読まないですよね……。

