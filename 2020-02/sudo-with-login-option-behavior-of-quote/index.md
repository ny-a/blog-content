---
title: "sudoに-iオプションをつけるとクオートの挙動が変わってハマりました"
date: 2020-02-29
---

`sudo` コマンドには `-i/--login` オプションがあり、コマンドを走らせるユーザー(デフォルトは root)のログインシェルを
使ってコマンドを実行できますが、このオプションを指定する場合としない場合でクオートの扱いが変わってハマってしまいました。

具体的には、EC2 の root で実行される user_data スクリプトで、 パスフレーズなしのキーペアを生成する際に

```shell script
sudo -u ec2-user -i ssh-keygen -f .ssh/id_rsa -N ''
```

とすると、 `option requires an argument -- N` というエラーが発生してしまいます。

(ちなみにここで生成したキーペアは、 git clone をするための deploy key として使おうとしています。
user_data とはいえ private key を含めたくなかったので、インスタンスで生成して public key を登録する形にしました。
結局 API を叩くときなどに使用する token/secret は user_data に含めることになるんですが……)

## issues

この問題ズバリの issue が5年前に出ていますが、1つもコメントはついていません。
[Bug 679 - sudo -i ignores empty arguments](https://bugzilla.sudo.ws/show_bug.cgi?id=679)

10 年前の
[Bug 413 - Unexpected change in quoting behaviour with -i flag](https://bugzilla.sudo.ws/show_bug.cgi?id=413)
も同じ問題を指しているように読めますが、こちらも1ヶ月経たずに放置されてしまっています。

## workaround

とりあえずの解決策としては、
[#679](https://bugzilla.sudo.ws/show_bug.cgi?id=679)
にある stackoverflow へのリンク
[Passing empty arguments to sudo -i](https://stackoverflow.com/questions/27892812/passing-empty-arguments-to-sudo-i)
にある通り、 `sudo -i sh -c 'foo "bar" ""'` などとすればうまく動くようです。

ただ、あまり嬉しい見た目ではないので、私は `-i` オプションを使わないで、
`sudo -u ec2-user ssh-keygen -f /home/ec2-user/.ssh/id_rsa -N ''`
とすることにしました。

`sudo` がデファクトスタンダードのようなものと認識していて、何の疑問もなく使っていたのですが、
脆弱性の問題なども見かけるので `doas` なども使ってみようかなと思いました。
