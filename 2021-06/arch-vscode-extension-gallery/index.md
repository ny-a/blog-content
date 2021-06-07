---
title: "Arch LinuxのCode-OSSの拡張機能"
date: 2021-06-07
---

[Arch LinuxのCode-OSSの拡張機能の検索先を変更する](https://blog.browniealice.net/post/code-oss_marketplace_issue_on_arch/)
に書いてある通りなんですが、Arch Linux の [code](https://archlinux.org/packages/community/x86_64/code/) パッケージは
OSS のもので、拡張機能のギャラリーは [Open VSX Registry](https://open-vsx.org/) を使用しているようです。

[Visual Studio Marketplace](https://marketplace.visualstudio.com/) で検索した拡張機能が
インストールできないと悩んでいたのですが、これが原因だったんですね。

調べてみた限りだと、ユーザーの設定ではギャラリーを変更できないようだったので、
一番始めのリンクの記事に書いてある通りに `/usr/lib/code/product.json` を書き換えると
Visual Studio Marketplace から検索することができるようです。

これって複数指定できないんですかね？あまり VSCode の拡張機能のレジストリについては
詳しくないですが……。
