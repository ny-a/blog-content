---
title: "AmazonLinux2-minimalについて調べました"
date: 2020-03-10
---

AmazonLinux 自体は知っていましたが、どんなバリエーションがあるかなどはあまり知らず、
Docker を使いたいときは始めから入っている ECS optimized な AMI を選ぶなど適当だったので調べてみました。

まず、メジャーバージョンとしては現在1と2があるようで、
1 の方は 2020/12/31 に [EOL](https://aws.amazon.com/blogs/aws/update-on-amazon-linux-ami-end-of-life/)
となって、 2023/06/30 までメンテナンスサポートフェーズとなるようです。
そのため、これから使い始めるのであれば AmazonLinux2 にしておいた方がよさそうですね。

AmazonLinux2 は 通常版と minimal のものがあり、通常版でも標準で入っているパッケージは少なめなようですが
minimal の方はさらに少なくなっています。
とはいえ、 bash や curl は始めから入っていますし、気になるのは awscli が入っていないことくらいでしょうか。
普段 docker で alpine をよく使っているので、むしろ minimal がまだ削れそうに感じます。

また、 `amazon-linux-extras` コマンドから追加のソフトウェアをインストールすることができるので、
困ることはほとんどないと思います。
`docker` や `epel` もコマンド1つで入りますし、変わったものでは `ecs` クライアントもインストールすることができます。

今まで適当に ECS Optimized な AMI を使っていましたが、 AmazonLinux2-minimal を積極的に使っていこうと思いました。
