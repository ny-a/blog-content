---
title: "dhcpcd が core から extra に移動されるかもしれません"
date: 2020-04-22
---

Arch Linux のメーリングリストを眺めていたら、dhcpcd の移動に関する話題が
上がっていました。

どうやら dhcpcd の利用率が低下していて、core には他の代替がある
(`networkd` と書かれていましたが、`dhclient` のことですかね？)
ため、extra リポジトリに移動することを提案していました。

pacman を使う上では core も extra も変わりはないのですが、
他のクライアントも使ってみてもいいかもしれませんね。

