---
title: "GitHubのdependabotにPRをもらったのでマージしました"
date: 2020-02-28
---

Jekyll で作ったブログのレポジトリに dependabot から PullRequest が来ていたのでマージしてみました。
今回はついでに他の Gem もアップデートしたので、コマンドラインからマージしました。

来た PullRequest は
[Bump nokogiri from 1.10.7 to 1.10.8 #1](https://github.com/ny-a/blog/pull/1)
です。

PR のブランチは `dependabot/bundler/nokogiri-1.10.8` に切られていました。
単に `git fetch` すれば降ってきます。
`git merge dependabot/bundler/nokogiri-1.10.8` すれば手元でのマージができるので、
`git push origin master` して PullRequest のマージが完了します。
PR のブランチは push 時に自動で削除されました。

`git fetch -p` すればリモートトラッキングブランチが削除されて、全て完了します。

CVE などを購読して使っているソフトウェアのバージョンを管理するのは大変なので、
(GitHub 上の OSS に限りますが)セキュリティの問題を監視してもらえるのは助かります。
(今回は static なページだったのであまり影響はないと思いますが……。)
