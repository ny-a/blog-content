---
title: "Git に git サブコマンドを追加してみました"
date: 2020-04-17
---

私はよくシェルに `git` と打ち込んでから行う操作を考えて、その後再度 `git` と入力してしまう
傾向にあります。`git git status` を実行するのはほぼ癖といってもいいかもしれません。

よく知られているように、git にはカスタマイズ可能なサブコマンド機能があります。
任意の実行ファイルを起動することも可能です。そこで、この機能を使って `git git` に
対処してみようと思いました。

```
git config --global alias.git '!git'
```

上記を実行すると、`git` の後に `git` が何回続いても正常に(？)コマンドが実行されるようになります。
これで `git git status` などと打ってエラーになることもなくなりました。

さて、`git git` でエラーになる問題は解決したわけですが、新たに別の問題が出てきました。
それは……このページが `git git` になっていることです……。

不思議なことにこの alias を設定した後は `git git` と打つことも減ったような気がします。
せっかく設定したんですけどね……。

