---
title:  "Svelteをwebpackで使ってみました"
date:   2020-01-19
---

[Building A Svelte 3 Todo App From Start To Deployment](https://medium.com/codingthesmartway-com-blog/building-a-svelte-3-todo-app-from-start-to-deployment-1737f72c23a6)
に従いつつ、 rollup の代わりに webpack を使って from stratch で作成してみました。

## 手順

まずは Svelte アプリの作成をします。 webpack を使った template は
[sveltejs/template-webpack](https://github.com/sveltejs/template-webpack)
にありますが、これを参考に以下のコマンドを実行します。

```
mkdir svelte-todo-webpack
cd svelte-todo-webpack
yarn init
git init
yarn add -D webpack{,-cli,-dev-server} svelte{,-loader} {css,style}-loader mini-css-extract-plugin
```

今回は `cross-env`, `serve`, `sirv-cli` などを使わないようにするため、いくつか変更している箇所があります。
とは言っても、 `serve` はどこで使っているか分からなかったので、単に webpack の設定を function にして、
`--env.NODE_ENV=development` という風に渡すように変更しただけですが。……多分。

あとはシュッと ToDo アプリの実装をします。簡単でしたね。

## HMR でのエラー

`TypeError: "todoitem.$on is not a function"`
というようなエラーがブラウザのコンソールに出ていました。
どうやら HMR に対応していないようなので、 HMR を無効にすることで対応しました。

## 感想

他のフレームワークで webpack+babel+typescript といった構成にすることが多いので、 rollup のときよりも理解がしやすい
構成になっているかなと思いました。
