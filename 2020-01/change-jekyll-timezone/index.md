---
title:  "Jekyllのタイムゾーン設定を変更しました"
date:   2020-01-04 01:00:00
---

[octokitをアップデートしました](/2020-01/update-octokit/) を投稿したのが01時
だったのですが、前日の投稿として表示されてしまいました。

## 原因・JST設定

GitHub の CI でのデフォルトのタイムゾーンが JST ではないからですね。

Jekyll の [Configuration Options](https://jekyllrb.com/docs/configuration/options/) を確認すると、
Timezone を設定できるようです。 `Asia/Tokyo` に設定しました。

## UTC に揃える

全部 UTC に揃えたら楽だとは思いますが、朝09時に日付が変わるのはまだ慣れないので……
と思ったのですが、 gatsby の方で面倒だったのでやっぱり UTC に揃えることにしました。


