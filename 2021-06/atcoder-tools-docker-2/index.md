---
title: "Atcoder-toolsのDockerイメージをAlpineベースに変更"
date: 2021-06-21
---

atcoder-tools の docker イメージを Alpine ベースに変更しました。
ArchLinux ベースだと手元とほぼ同じ環境なのですごい楽なんですが、
今回はパッケージ数も少なくてそんなに大変ではなかったので
Alpine ベースに変更してみました。

libc6-compat も入れるとよりよいのかもしれませんが、
どうせソースからビルドすることが大半なので、あまり関係ないと思っています。
