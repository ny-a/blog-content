---
title:  "octokit 4.15.0がリリースされました"
date:   2020-01-04 01:18:27
---

[octokitをアップデートしました](/2020-01/update-octokit/) では octokit のリリースがまだだったので github から
直接インストールするようにしてアップデートしましたが、 4.15.0 がリリースされたのでそちらにアップデートします。

## github 指定を削除

`gem "octokit", github: "octokit/octokit.rb", ref: "ae5838a"` を削除して、 `bundle update` を実行します。

これで faraday 1.0 系でもエラーにならずに正しく実行できるようになりました。

リリースありがとうございます！


