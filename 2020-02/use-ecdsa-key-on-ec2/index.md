---
title: "EC2にECDSAのキーを使ってSSHできるようにしました"
date: 2020-02-25
---

AWS のキーペアは RSA しか対応していないと思いますが、最近は RSA を使うこともかなり減っていて、新しくセットアップした
PC などでは ECDSA/Ed25519 のキーしか作っていないこともあります。
そこで、 UserData を使って普段使いの SSH キーを取得して SSH できるようにしました。

## UserData

AmazonLinux2 を使っているので、ログインユーザーは `ec2-user` です。

UserData を以下のようにします。

```shell script
#!/bin/bash

set -eu

curl https://github.com/ny-a.keys >> /home/ec2-user/.ssh/authorized_keys
```

AmazonLinux に入っている OpenSSH のバージョンが古くて RSA にしか対応していないわけではないので、
`authorized_keys` に入れてあげさえすれば使うことができます。

AWS のキーペアで管理しないため、本番環境などでは何か問題があるかも……とは思いますが、普段使いのキーを使える上に、
普段使いのキーを更新したあとに起動したインスタンスは新しいキーを使えるようになるので、利便性は高いんじゃないかなと
思います。

とりあえず、開発中などはこのようにすると便利そうだと思いました。
