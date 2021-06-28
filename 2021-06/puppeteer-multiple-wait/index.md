---
title: "Puppeteerで複数のwaitを組み合わせる"
date: 2021-06-29
---

puppeteer の page.click なんかを使うときに、waitForNavigation
などと連続の await で組み合わせるとうまく遷移の完了を検知できずにつらいなと思っていました。

よくよく [ドキュメント](https://pptr.dev/#?product=Puppeteer&version=v10.0.0&show=api-pageclickselector-options)
を読んでみると、Promise.all で同時に開始して、Promise.all を await するとよいと書いてありました。

ドキュメントはしっかり読むべきですね……。
