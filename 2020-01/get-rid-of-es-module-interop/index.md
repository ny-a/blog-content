---
title:  "esModuleInteropを使わないようにしました"
date:   2020-01-18
---

このブログに Typescript を導入したとき、 default import でエラーが出ていたので一旦
`tsconfig.json` に `esModuleInterop` を追加して対処していました。

ただ、デフォルトの設定を変更するのはあまり好ましくないと感じたので、
[microsoft/TypeScript#3337](https://github.com/microsoft/TypeScript/issues/3337)
を参考に、 `import React from 'react` を `import * as React from 'react` に
書き換えることで対処しました。

これが esModuleInterop に対する正しい対処方法かは分かりませんが……。
