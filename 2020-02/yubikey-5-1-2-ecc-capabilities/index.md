---
title: "手元のYubikey5NFCのECCの対応状況を調べました"
date: 2020-02-13
---

[Yubikeyのファームウェア5.2.3がリリースされていました](/2020-02/yubikey-firmware-5-2-3/)
で、新しい Yubikey では Ed25519 などの ECC (楕円曲線暗号) に対応していることを知りましたが、
手元にある v5.1.2 の Yubikey の対応状況を調べてみました。

Yubikey の商品説明のページには、
`RSA 2048, RSA 4096 (PGP), ECC p256, ECC p384`
と書いてあります。私はてっきり OpenPGP モードでも ECC p384 が使えると思っていたのですが、
どうやら OpenPGP では RSA 2048/4096 、 PIV では 3DES, RSA 1024/2048, ECC p256/384 が使えるようです。

ますます新しい Yubikey が欲しくなってきたのですが、まだまだ PIV あたりの仕様や PGP Smartcard などについても
慣れていないので、まずはいろいろ試してみようと思いました。
