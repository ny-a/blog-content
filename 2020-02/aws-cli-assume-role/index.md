---
title: "AWS CLIでAssumeRole"
date: 2020-02-24
---

AWS のアカウントを CLI から操作することが多いので credentials を保存しているのですが、
権限を多く持ったユーザーの認証情報を持っておくのは少し不安になったので、 AssumeRole を使って普段はあまり権限を
持たないユーザーの認証情報を持っておくことにしました。

## 方法

方法は
[How do I assume an IAM role using the AWS CLI?](https://aws.amazon.com/premiumsupport/knowledge-center/iam-assume-role-cli/)
に書いてある通りです。

AssumeRole 時に MFA を要求するように設定することもできます。

また、
[Using an IAM Role in the AWS CLI](https://docs.aws.amazon.com/cli/latest/userguide/cli-configure-role.html)
に記載のあるように、 AWS CLI では `--profile` オプションで指定することにより、自動で簡単に AssumeRole を
使用することができます。

MFA を併用することで、 TOTP をパスワードとした sudo のような操作も可能になります。
また、検証環境と本番環境のロールを分けるといったことも考えられます。
誤操作を防ぎ、安全性を高められると思うので、このような機能は積極的に使っていこうと思いました。
