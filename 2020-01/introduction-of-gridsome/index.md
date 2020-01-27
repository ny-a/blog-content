---
title: "gridsomeを使ってみました"
date: 2020-01-26
---

いつものように
[9 Projects you can do to become a Frontend Master in 2020](https://dev.to/simonholdorf/9-projects-you-can-do-to-become-a-frontend-master-in-2020-n2h)
を進めていっています。
今回は gridsome を使ったブログです。

だいたい gatsby と同じような感じですが、クエリを `<page-query>` 内に書くなど、 Vue らしさというか XML 側に寄せているような
雰囲気があるのが大きな違いでしょうか。

HTML や vanilla な javascript はもはやバイナリのような扱いを受けることもあるので、
React/Gatsby など、 typescript などにロジックを寄せて、html なども生成するような形にするのが筋が通っているように感じられます。

……というのは多分 `<page-query>` 内のインデントがボロボロになってしまったのが気になったのもあると思います。
Intellij 用の gridsome プラグインを書きましょう……となりました。

