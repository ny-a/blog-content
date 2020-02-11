---
title: "Removing diversion by rpikernelhack"
date: 2020-02-12
---

Raspbian のインストールをしていたのですが、 `apt-get upgrade` を実行すると見慣れない `rpikernelhack` という文字を
見掛けました。

検索してみると、[Stack Exchange](https://raspberrypi.stackexchange.com/a/94827) で fake package だという情報が
見つかりました。
fat32 では Hard link がサポートされていないから、  dpkg の diversion という機能を使用(濫用？)しているようです。

RPi forum の [upgrade to unbootable](https://www.raspberrypi.org/forums/viewtopic.php?t=99264)
と同じようなメッセージを見かけたのですが、どうもファイルシステムのサイズを拡張する前にアップグレードすると
このようなメッセージが出ると書いてあります。

初回起動時にファイルシステムのサイズが調整されると思っていて、それは済んでいるはずですがそれとは違うんでしょうか。
今のところ再起動しても起動しなくなるようなことはないですが、初回アップグレード前に一度再起動する必要があると
いうことなんでしょうかね。
