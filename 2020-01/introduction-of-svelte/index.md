---
title:  "Svelteを使ってみました"
date:   2020-01-07
---

[9 Projects you can do to become a Frontend Master in 2020](https://dev.to/simonholdorf/9-projects-you-can-do-to-become-a-frontend-master-in-2020-n2h)
をこなしていきます。今回は Svelte で ToDo アプリを作るやつを少しだけ進めてみました。

## 導入

[The easiest way to get started with Svelte](https://svelte.dev/blog/the-easiest-way-to-get-started)
に書いてある通りですが、 `degit` を `yarn` で使うには少し注意が必要です。

`npx degit` の場合、2番目の引数はカレントディレクトリのフォルダ名になりますが、
(`~/node_modules/.bin/degit` を使う場合の) `yarn degit` の場合は、ホームディレクトリからのフォルダ名になるような気がします。

そのため、代わりに以下のコマンドを実行するのでもよさそうです。

```
git clone https://github.com/sveltejs/template my-svelte-project
cd my-svelte-project
rm -r .git
yarn
yarn dev
```

## 感想

今回はデフォルトの `rollup` をそのまま使ってみましたが、 `webpack` も使えるようです。
また `webpack` でも試してみようかなと思います。
