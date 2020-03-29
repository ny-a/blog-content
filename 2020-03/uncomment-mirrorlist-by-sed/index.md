---
title: "Pacman の multilib を sed で有効化する"
date: 2020-03-29
---

タイトルの通りで、 Arch Linux の Docker イメージを AUR のビルド用にしたくて、 multilib を使う必要があったので方法を
探してみました。

まず試したのは patch だったのですが、初期インストール状態に含まれていないため、あまり慣れていない sed を使うことに
しました。
調べてみると
[How to edit next line after pattern using sed? - StackExchange](https://unix.stackexchange.com/a/285162)
にちょうど ArchLinux 用の(こちらは mirrorlist の方ですが)回答がありました。
multilib レポジトリの有効化用に変更したコマンドは以下の通りです。

```shell script
sed -e '/\[multilib\]/,/^$/{s/^#//}' /etc/pacman.conf
```

元のコマンド `/\[multilib\]/,/^$/{//!s/^#//}` には `//!` が入っていて、これで1行目を無視しているようなのですが、
これがどう動くのかは勉強不足で分かっていません……

とりあえず sed で思ったよりいろんなことができることが分かりました。
