---
title: "ターミナルでEnterが^Mになってしまうときの対処法"
date: 2020-02-06
---

`cat` コマンドなどでターミナルにバイナリ(制御文字)を吐いてしまうと、 Enter キーを押しても
`sudo` などのパスワード入力を確定できなくなることがあります。
(前使っていた xterm ではコマンドの入力もできなくなっていた気がしますが、 rxvt-unicode ではコマンドは使えるようです。)

[Pressing enter produces ^M instead of a newline - Ask Ubuntu](https://askubuntu.com/questions/441744/pressing-enter-produces-m-instead-of-a-newline/454663)
に書いてある通りですが、
`stty sane` (全てデフォルト値に戻す) か `stty icrnl` (CR を new line として扱う) を実行すれば直るようです。

これで遠慮なくバイナリを吐かせることができますね。
と思ったのですが、
[Can “cat-ing” a file be a potential security risk?](https://security.stackexchange.com/questions/56307/can-cat-ing-a-file-be-a-potential-security-risk)
などを見るとセキュリティ上あまり好ましくないようですね……
