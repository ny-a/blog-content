---
title: "Blogの内容を別レポジトリに移動しました"
date: 2020-01-29
---

今までは gatsby のブログ用レポジトリにブログの内容を追加していましたが、
テンプレートと内容は分けた方がいいかなと思い、内容だけ別レポジトリに分けてみました。

具体的には、 gatsby-source-filesystem を使っていたのを gatsby-source-git に変更しました。
基本的に gatsby-source-filesystem と同様に使えると書いてありましたが、
slug の生成に createFilePath を使っていたのが gatsby-source-filesystem に依存していたので、
node.parent.file.relativeDirectory から生成するように変更しました。

また、 gatsby-source-git の指定だけだと、タイミングの問題なのか gatsby-transformer-remark あたりで
問題が発生していたので、 gatsby-source-filesystem でダミーのソースを指定することでとりあえず対処しました。

レポジトリを分離したので CI を使ってビルドするようにしようかなと思ったのですが、そうすると
別に gatsby-source-git を使わなくても、 CI 側で事前に checkout しておけばいいのでは……と思ってきました。
また戻すかもしれません。
