---
title: "ブログのビルドが失敗するようになったのでnpmパッケージをアップデートしました"
date: 2020-03-09
---

この Gatsby のブログは Github Actions でビルドしているのですが、5日くらい前からビルドに失敗するようになっていました。
手元ではビルドできるので、 `npm run deploy` を手動で実行してデプロイしていたのですが、
ずっと放置しているわけにはいかないので直しました。

本当は [mxschmitt/action-tmate - GitHub](https://github.com/mxschmitt/action-tmate)
を使ってデバッグするつもりだったのですが、 npm パッケージをアップデートしたら直りました。

`npm audit` で `found 10 vulnerabilities (1 moderate, 9 high)` になっているのが少し気になりますが……
acorn は `package-lock.json` を見る限りだと 7.1.1 が入っているように見えますね……、
`npm audit` について調べてみないと分からないですが、今回は Gatsby なのであまり影響はないかなと認識しています。
