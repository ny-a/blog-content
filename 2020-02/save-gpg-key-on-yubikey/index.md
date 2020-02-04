---
title: "YubikeyにGPGキーを登録しました"
date: 2020-02-05
---

[新しいGPGキーを作成しました](/2020-02/create-new-gpg-key/)
で GPG キーを作成しましたが、 Yubikey も活用できるように Yubikey にも GPG キーを登録してみました。

マスターキーの入っている環境で新しくサブキーを作成します。
`ykman piv` や `gpg` コマンドで試した感じでは、手元の Yubikey には RSA 以外の ECDSA/EdDSA のキーを
登録することができませんでした。
(Yubikey5 NFC, Firmware 5.1.2 なのでできると思ったのですが……)
そのため、 RSA 4096bit のサブキーを3種類作成します。

そして、それぞれ `keytocard` を実行して、 Yubikey に秘密鍵を移動します。
移動すると `ssb>` と表示され、 `Card serial No.`  が表示されます(このあたりがどう保存されているか気になっています)。

あとは PIN を適宜変更するのですが、 `gpg --edit-card` と `ykman piv` で PIN の管理が別なのかはよく分かっていません。
(登録してみた感じだと別で管理されているようですが、きちんと調べられていません)
`gpg` の PIN, Admin PIN, `ykman piv` の PIN, PUK に加え、 Management Key というものがありますが、
これは `ykman piv change-management-key -p` を実行して PIN を入力することで、 PIN から生成して PIN で認証するように
することができます。

無事登録できたので、`password-store` では PC に保存しているサブキーと Yubikey に移動したサブキーの両方で
使えるようにしようと思ったのですが、 gpg では最新の暗号化用のキーを使って暗号化するようで、 キー ID の末尾に `!` を
つけないと意図した通りに動きませんでした。

これで、普段使いのマシンではローカルのサブキーを使って復号化し、それ以外のマシンでは(秘密鍵をインポートしなくても)
Yubikey を使って復号化できるようになりました。
Android では Yubico Authenticator も使ってみようと思いますが、
`password-store` で Yubikey を使えると嬉しいなという思いもあり……
PIV 対応アプリがあるのかは探してみますが、自分で作ることも考えています。
