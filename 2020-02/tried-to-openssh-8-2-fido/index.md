---
title: "OpenSSH8.2でfido2/u2fを試そうとしました"
date: 2020-02-17
---

OpenSSH 8.2 がリリースされ、 fido2/u2f が公式にサポートされたようなので試してみました。

私は ArchLinux を使っているので比較的早くパッケージが降ってきます。
具体的には、 2020-02-14 にリリースされ、当日中には
testing レポジトリに入り、 2020-02-16 03:30Z に core レポジトリに入りました。
core に入ったことにより `pacman -Syu` でインストールできるようになったので試してみましょう。

[OpenSSH 8.2 のリリースノート](https://www.openssh.com/txt/release-8.2) を見ると、
`ssh-keygen -t ecdsa-sk` で FIDO token backed key を生成することができるようですが、
試してみると、

```shell script
$ ssh-keygen -t ecdsa-sk                                                                   :(
Generating public/private ecdsa-sk key pair.
You may need to touch your authenticator to authorize key generation.
Provider "" dlsym(sk_api_version) failed: /usr/lib/ssh/ssh-sk-helper: undefined symbol: sk_api_version
Key enrollment failed: invalid format
```

となり失敗します。

[Yubico/libfido2 Issue#116](https://github.com/Yubico/libfido2/issues/116)
を見ると、 `ssh-keygen -t ecdsa-sk -w /usr/lib/libsk-libfido2.so` を実行すると以下のようなエラーが出ると書かれています。

```shell script
$ ssh-keygen -t ecdsa-sk -w /usr/lib/libsk-libfido2.so                                     :(
Generating public/private ecdsa-sk key pair.
You may need to touch your authenticator to authorize key generation.
Provider "/usr/lib/libsk-libfido2.so" implements unsupported version 0x00020000 (supported: 0x00040000)
Key enrollment failed: invalid format
```

[FS#65513](https://bugs.archlinux.org/task/65513)
にも書かれていますが、これは OpenSSH の configure 時に `--with-security-key-builtin` オプションを付けてビルドすると
-w オプションなしで使えるようになるようです。
上記でパッケージのバグとコメントされているので、数日中に直るでしょう。

リビルドすれば試せますが、現状は Yubikey で間に合っているので降ってきたら試そうと思っています。
