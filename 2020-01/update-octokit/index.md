---
title:  "octokitをアップデートしました"
date:   2020-01-03 01:06:28
---

[Jekyllを使い始めました](/2020-01/introduction-of-jekyll/) でセットアップ時に
エラーが出ていたので調査しました。

## 原因

`faraday` gem の 1.0 がリリースされたことが原因ですが、リリースされたのが丁度01/01でした。
情報が少なかったわけです。

依存ツリーとしては

- github-pages
- github-pages-health-check, jekyll-gist, jekyll-github-metadata
- octokit
- (sawyer)
- faraday

となっているようです。
また、 `~> 0` のような、1系が入らないバージョン指定もないようです。

## 各gemのissueの確認

- [issue github/pages-gem#665](https://github.com/github/pages-gem/issues/665)
- [PR octokit/octokit.rb#1154](https://github.com/octokit/octokit.rb/pull/1154)

どうやら原因は octokit にあるようです。
修正の PR 自体は master ブランチにマージされていて、リリースを待つだけのようです。

[issue octokit/octokit.rb#1177](https://github.com/octokit/octokit.rb/issues/1177) によると、来週にはリリースする予定ということです。

## workaround

01/01 に書いたように faraday の 0.17 を指定することでもエラーは出なくなりますが、
octokit を github から取得するようにしても対応できます。

具体的には、

```
gem "octokit", github: "octokit/octokit.rb", ref: "ae5838a"
```

を Gemfile に追加することで、 faraday の 1系を使えるようになります。

(`ae5838a` 以降であればいいので、 `branch: "master"` などでも問題ないです。)

## まとめ

octokit のメンテナさん、リリース頑張ってください！いつもありがとうございます。
