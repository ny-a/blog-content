---
title: "gatsbyを使い始めました"
date: 2020-01-05
---

Jekyll を使い始めたところですが、早速浮気して Gatsby を使っていこうと思います。

[9 Projects you can do to become a Frontend Master in 2020](https://dev.to/simonholdorf/9-projects-you-can-do-to-become-a-frontend-master-in-2020-n2h)
に丁度 gatsby で blog を作るという項目があったので、これを順不同でこなしていこうと思います。

## 導入

`gatsby new` を実行します。

## gh-pages

公式ドキュメントの [How Gatsby Works with GitHub Pages](https://www.gatsbyjs.org/docs/how-gatsby-works-with-github-pages/)
を参考に、 `yarn add -D gh-pages` を実行して、 deploy スクリプトを追加します。

また、 `gatsby-config.js` に `pathPrefix` を追加して、実際のレポジトリに合わせて設定します。

## GitHub Pagesにデプロイ

`yarn deploy` を実行します。

標準では自動で `gh-pages` ブランチに push されるようです。

## 感想

内部で GraphQL を使っていてなるほど〜となりました。
今までこういった Static Site Generator を使ったことはなかったのですが、理想に近いものだと感じました。

でも github-pages 公式サポートのある Jekyll の方が楽なんですよね……少し悩んでいます。

後日 gatsby with TypeScript に挑戦したいと思っています。
