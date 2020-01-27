---
title:  "Jekyllを使い始めました"
date:   2020-01-01 11:23:40
---

一年の計は元旦にあり！

……

…………

………………

( ˘ω˘ )

元日なのでセーフということで……

Jekyll をセットアップしてブログを書き始めました。
今年は毎日何かアウトプットすることが目標です。

## Jekyll のセットアップ

セットアップの方法は、基本的に[公式の docs](https://jekyllrb.com/docs/github-pages/)に書いてある通りです。

```
jekyll new blog
cd blog
sed -i -e 's/^gem "jekyll"/# &/' -e '/gem "github-pages"/s/^#//' -e '$a gem "faraday", "~> 0.17"' Gemfile
bundle update
sed -i -e 's#baseurl: ""#baseurl: "/blog"#' _config.yml
bundle exec jekyll serve
```

1つ問題があり、数ヶ月前に同様の手順を踏んだときから `faraday` が 1.0 にアップデートされたようで、実行時に
`jekyll 3.8.5 | Error:  uninitialized constant Faraday::Error::ClientError` というエラーが出るようになっていました。

そのため、 workaround として `faraday` を 0.17 系を使用するようにしました。

## Happy new year!

& Happy development!!
