---
title: "GitHubのrepository-dispatchイベント"
date: 2021-06-14
---

repository-dispatch イベントは前から使っていたのですが、`everest-preview` をつけたまま使っていました。
もう不要になったのかと思い [GitHub のドキュメント](https://docs.github.com/en/rest/reference/repos#create-a-repository-dispatch-event)
を見てみた所、やはり不要になっていました。

改めてドキュメントを見てみると、この API エンドポイントは GitHub の外からトリガーするために使うもののようですね。
GitHub Actions 内から他のリポジトリの Action をトリガーする方法が何かあるのでしょうか。
