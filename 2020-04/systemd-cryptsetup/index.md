---
title: "systemd-cryptsetup"
date: 2020-04-20
---

ArchLinuxARM で初期インストール時から `cryptsetup` が入っていて
気になっていたのですが、systemd が `cryptsetup` に依存していることを
知りました。

ArchLinuxARM を使ってエアギャップコンピュータ上で GPG 鍵を管理しようと
思っていたときに、バックアップ時に `LUKS` を使おうと思ったら既に
`cryptsetup` が入っていて驚きました。
メインのマシン上ではフルディスク暗号化を使用しているため明示的に
インストールしていたので気付きませんでした。

`systemd-cryptsetup`、起動時に `crypttab` に記載されている暗号化
パーティションをマウントするために使われているようですね。
私は initramfs 内でマウントしているのでしばらく使うことはなさそうですが……。

