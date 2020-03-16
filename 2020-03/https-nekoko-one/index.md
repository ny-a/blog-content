---
title: "nekoko.oneをHTTPSに対応させました"
date: 2020-03-17
---

といっても GitHub Pages なのでチェックボックス1つ入れるだけなんですが……。

GitHub Pages での独自ドメインの HTTPS 対応は初めてだったので(本当に簡単ですが)一応メモしておきます。

1. CNAME ファイルを作成して、使用する独自ドメインを指定する(Settings からでも可能)
1. [Managing a custom domain for your GitHub Pages site](https://help.github.com/en/github/working-with-github-pages/managing-a-custom-domain-for-your-github-pages-site)
に従って DNS レコードの設定をする  
  今回は Apex ドメインなので A レコードを設定しました。
1. 最大48時間待つ(6時間くらいでできていた気がしますが。)
1. `Enforce HTTPS` にチェックを入れたり、https でアクセスしてみる

という感じです。 GitHub 様々ですね。

というわけで割と(？)セキュアな [https://nekoko.one/](https://nekoko.one/) ができました。
