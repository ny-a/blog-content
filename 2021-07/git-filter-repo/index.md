---
title: "git filter-repoを使ってみました"
date: 2021-07-03
---

Git を使っていて、何らかの理由でコミット履歴を書き換えたいとき、
標準サブコマンドの中でよく使われるのは filter-branch でしょう。

ただ、[公式ドキュメント](https://git-scm.com/docs/git-filter-branch)
を見てみると、filter-branch を使う代わりに、
[filter-repo](https://github.com/newren/git-filter-repo)
というサードパーティーの代替などを使うように警告されます。

そこで、filter-repo を使ってみました。
ArchLinux では [community/git-filter-repo](https://archlinux.org/packages/community/any/git-filter-repo/)
からインストールできます。

今回やりたいことは (いつも同じで)、個人で使っているこのアカウントが
Author/Committer となっているコミットを、仕事で使っている情報に書き換えることです。
(毎回 git config をやり忘れるの、何か対策したいところですが……。)

ドキュメントを見てみると、どうもあまりオプションはないようです。
というより、Python のコードをオプションとして渡してあげると、
いい感じに実行してくれるようです。

今回はまだ自分しかコミットしていないリポジトリだったので、
常に同じバイナリ列 (文字列ではダメです) を返すコードを書きます。

……その前に、バックアップを取っておきます。
filter-repo では、clone したばかりの clean なリポジトリを使うことが推奨されています。
/tmp で `git clone /path/to/repository --no-local` を実行して、リポジトリを複製します。

次に、実際の書き換えを行っていきます。
`--email-callback` と `--name-callback` を使います。
どちらも現在の値を考慮する必要はないため、
`"return b'user@example.com'"` のような引数を与えればいいです。

そして実行すると……、一瞬で終わりました。
filter-branch では original が残りますが、filter-repo では残らないようです。
軽く見た感じ問題なく完了しているようなので、
`git push /path/to/repository branch:branch_new` を実行して、
元のリポジトリに書き換えたコミットを push します。

元のブランチと diff を取って、当然何も出ないことを確認したら、
`git reset --hard branch_new` したり、
`git branch -f branch branch_new` したりして古いブランチを新しいブランチに移動します。

あとは、必要に応じて force push したり(関係するメンバーに謝りましょう……)、
運よく push していなければ、もう二度と同じ誤ちを繰り返さないように心に誓ったりしましょう。
