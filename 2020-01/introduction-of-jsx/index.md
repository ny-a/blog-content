---
title:  "JSXを単体で使ってみました"
date:   2020-01-21
---

JSX といえば React というイメージですが、別に一緒に使わないといけないわけではないと思うので、
`webpack`, `babel` あたりを使って試してみました。

`React.createElement` 相当のライブラリは一旦 `jsx-render` を使ってみました。
[Lessons learned using JSX without React](https://itnext.io/lessons-learned-using-jsx-without-react-bbddb6c28561)
を参考にしましたが、レポジトリが消えているようなので代替を探す必要があるかもしれません。

また、 `eslint` や `prettier` もよく使うのでインストールしました。
eslint で JSX はサポートされているようですが、 unused-var になるなど問題点もあるようです。

Aurelia などもありますが、できるだけフロントエンドフレームワークを使わないで Web 標準を使って
Web アプリを作る方法を模索してみるのもよいかもしれません。(JSX, Web components など。)
