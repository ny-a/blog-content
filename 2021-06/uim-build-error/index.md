---
title: "uimのビルドエラー"
date: 2021-06-01
---

AUR の [uim](https://aur.archlinux.org/packages/uim/) パッケージに、ビルドが失敗するという
コメントをいただきました。

しかし、手元の Docker 環境でビルドしてみたところ、正常にビルドを完了することができました。

ビルドエラーは csi というコマンドで発生しているようで、手元のビルド環境にはこの実行ファイルは
存在していませんでした。
`Makefile.in` ファイルを確認した所、ビルド時に `csi` 実行ファイルが存在していればそのコマンドが
実行されるようになっていました。

Arch のパッケージで `/usr/bin/csi` が含まれているものを探してみると、

```
$ pacman -Fy
$ pacman -F /usr/bin/csi
usr/bin/csi is owned by extra/mono 6.12.0.107-1
```

どうやら [mono](https://archlinux.org/packages/extra/x86_64/mono/) に含まれているようでした。
`error CS2006: Command-line syntax error: Missing '<text>' for '-R' option` というエラーも、
検索してみた限りでは mono のエラーと考えてよさそうです。

ただ、uim は mono に依存していないようなので、この csi は mono に含まれているバイナリを
期待しているわけではなさそうです。GitHub の issue を探してみると、[#26](https://github.com/uim/uim/issues/26) で
csi について言及されていました。
これによると、Chicken Scheme のインタプリタが csi という名前のようです。

依存に含まれていない以上何とも言えないですが、上記の issue も閉じられていないようなので
Chicken Scheme が実行可能でもエラーになってしまいそうな気がしました。

ひとまず、mono の入っていない環境では正常にビルドできそうです。
