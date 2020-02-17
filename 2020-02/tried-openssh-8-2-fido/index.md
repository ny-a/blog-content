---
title: "OpenSSH8.2でFIDO2を試しました"
date: 2020-02-18
---

といってもキーの生成だけですが……

とりあえず手元にある古い(？) Yubikey を使って ecdsa-sk のキーの生成ができることを確認してみます。

```shell script
$ ssh-keygen -t ecdsa-sk -b 521
Generating public/private ecdsa-sk key pair.
You may need to touch your authenticator to authorize key generation.
Enter passphrase (empty for no passphrase): 
Enter same passphrase again: 
Your identification has been saved in ...
Your public key has been saved in ...
The key fingerprint is:
SHA256:LHym5H0zQ6tvRXNZp/bMEUy7F1WN6tUicAGJMjxSOZQ ...
The key's randomart image is:
+-[ECDSA-SK 256]--+
|     +oo ..o..oo=|
|    . E . o . .o*|
|     . =   o . Bo|
|     . .    = B.+|
|      + S .o * *o|
|     o * . .o   =|
|      o . *.     |
|         o.+     |
|        .o.      |
+----[SHA256]-----+
```

256 bit になってしまいました、 Yubikey 側の制限ですかね？

念のため？ ed25519-sk のキーも生成してみます。

```shell script
$ ssh-keygen -t ed25519-sk -b 521
Generating public/private ed25519-sk key pair.
You may need to touch your authenticator to authorize key generation.
Key enrollment failed: requested feature not supported
```

Yubikey が ed25519 に対応していないのでこちらは当然失敗しました。

生成に成功した ecdsa-sk キーを使って ssh しようとしてみましたが、相手が openssh7.9p1 だったので失敗しました。

とはいえ Yubikey の SmartCard の方が〜〜〜、というか対応サーバーが十分普及したら使うか考えましょう。

リリースノート、FIDO2/U2F と書いている部分と FIDO2 しか書いていない部分があって、 U2F しか書いていない部分はない？ので、
U2F についてはよく分かっていません……というか、認証周りいろいろややこしすぎて……追い追い調べてまとめようと思います。
