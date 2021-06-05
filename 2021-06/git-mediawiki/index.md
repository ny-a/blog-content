---
title: "Git-Mediawiki"
date: 2021-06-05
---

ArchWiki の編集で割とつらいのが、編集が textarea で行う必要があることです。
普段はあまり気にならないですが、サイズの大きいページを編集する際などは
レスポンスの悪さが気になることもあります。

これが、テキストファイルをテキストエディタで編集するようにできたら
色々な問題が解決しそうです。また、revision の仕組みなどを考えると、
git などでバージョン管理をしてあげると嬉しいかもしれません。

そこで、「git mediawiki」などで検索してみると、やりたいことズバリの
[Git-Mediawiki](https://github.com/Git-Mediawiki/Git-Mediawiki) という
プロジェクトを発見しました。

git は perl に依存しているので驚くことでもありませんが、Git-Mediawiki も
perl で書かれていて、perl の依存のインストールが必要です。
私は、各言語の依存パッケージでマシンの環境を汚したくないので、このような
場合には Docker イメージに閉じ込めてしまう場合が多いです。
いつも通り archlinux/archlinux ベースイメージから、git と各依存パッケージを
インストールしてイメージを作成しました。

さて、早速 ArchWiki 日本語版を pull していきたいところですが、実際に
やってみると途中で落ちます。author の特殊文字のエスケープが抜けていますね……。

あと、今まで気付いていなかったのですが、このプロジェクトは git-core に
取り込まれているようです。知名度はそんなに高くない気がしますが、
git コミッタの周りでの使用者が多いんでしょうか……。

とにかく、この場合パッチを送るのは git-core の方になりそうなので、
git の [コントリビューションの方法](https://github.com/git/git/blob/master/Documentation/SubmittingPatches) を調べるところから始めないと
いけないですね。

設定項目としては、標準では標準名前空間のみ対象としているため、ArchWiki の
全ての名前空間を対象にするには、

`git config remote.origin.namespaces "(Main) Talk User User_talk ArchWiki ArchWiki・トーク File File_talk MediaWiki MediaWiki_talk Template Template_talk Help Help_talk Category Category_talk"`

を実行する必要がありますね。