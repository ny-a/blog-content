---
title: "Git rerereサブコマンドを知りました"
date: 2020-02-16
---

[The Git Rerere Command — Automate Solutions to Fix Merge Conflicts](https://levelup.gitconnected.com/the-git-rerere-command-automate-solutions-to-fix-merge-conflicts-d501a9ab9007)
を見て `git-rerere` サブコマンドを知りました。
と言ってもまだ experimental なようで、 `git config [--global] rerere.enabled true` を実行しないと使えないようです。

上記の記事を見て少し試してみましたが、業務では今のところ使おうとは思いませんでした。
conflict したときに `git consult` みたいなコマンドを呼んで、過去の似た conflict 解消を含む merge commit を参照して、
似たような解決を試みるようなものが欲しいのかなと思いました。
といっても、それだと rebase なんかを consult できないので、 rerere の方が少し強力ではありますが。

[git-rerere のドキュメント](https://git-scm.com/docs/git-rerere) をちらっと見てみて、他にもいろいろな
サブコマンドがあるのでそれを見てみたら、 `git-worktree` など知らないコマンドを知ることができて楽しいです。

とはいえ、 git も複雑になりすぎているのでは……と思うこともあります。
サブコマンドに分かれているとはいえ……
