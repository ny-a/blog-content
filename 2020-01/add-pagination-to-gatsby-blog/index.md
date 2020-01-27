---
title:  "Gatsbyのブログにページネーションを追加しました"
date:   2020-01-17
---

この Gatsby を使っているブログも10ポストを超えてきました。
そこで、普通のブログのようにページネーションを導入しました。

[NickyMeuleman/gatsby-paginated-blog](https://github.com/NickyMeuleman/gatsby-paginated-blog)
を参考に、といっても `gatsby-node.js` と `src/pages/index.js` を編集するだけですが……。
[commit e871f7e](https://github.com/ny-a/blog2/commit/e871f7ec3e153bb8feec22719ca94e8bce3347e2)
で変更した通りです。 

実装を見てみると簡易的なもののようなので、10ページ程度になる前にもうちょっとちゃんとした
実装に変更しないといけないかなと思っています。
