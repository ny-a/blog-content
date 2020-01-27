---
title:  "GnuPGのssh-agentエミュレータを使ってみました"
date:   2020-01-10
---

今まではあまり気にしていなかったのですが、gh-pages のデプロイ時に2回パスフレーズを聞かれるのが
さすがに気になってしまい、 ssh-agent を使うことにしました。

前に何度か使っていたような記憶があるのですが、システム自体をあまり理解していなかったのもあり、
今の環境をセットアップするときには有効にしていませんでした。

## 設定

基本的には[GnuPG - ArchWiki](https://wiki.archlinux.org/index.php/GnuPG#SSH_agent) に従うだけです。

`~/.pam_environment` で `SSH_AUTH_SOCK` の設定をして、Xorg で使う場合は TTY の設定をします。

## 感想

ssh-agent と変わらずパスフレーズのキャッシュなどは普通に便利なのですが、
gpg-agent は内部で ssh-key を gpg-key としてインポートしていそうな感じですね。(追って調査します)

gpg-key で ssh することも可能なので、行く行くは gpg-key にまとめてしまおうかなと思っています。
