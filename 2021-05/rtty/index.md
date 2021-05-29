---
title: "RTTY のデコードを試してみました"
date: 2021-05-29
---

セキュリティ・ネクストキャンプに応募しようと思うので、その講義の中で扱われる
RTTY について少し試してみようと思いました。

講師の方のプロジェクトは [imaoca/RTTY - GitHub](https://github.com/imaoca/RTTY) にあります。

ここでは、サンプルの音声ファイルとして Wikipedia の [RTTY.ogg](https://en.wikipedia.org/wiki/File:RTTY.ogg) を
使用します。

ただ、このままでは使用できず、このプロジェクトのスクリプトで仮定されているフォーマットに
変換する必要があります。

サクっと ffmpeg を使って 8KHz sampling, mono, 8bit quantization, and no sign な wav ファイルに
変換しましょう。

```
ffmpeg -i RTTY.ogg -ar 8k -c:a pcm_u8 -f wav rtty3s.wav
```

`-i` の後の ogg ファイルが入力、`-ar` がサンプリングレート、`-c:a` で量子化ビット数と符号なしを指定して、
`-f` で wav フォーマットを指定、最後に出力先ファイル名です。

あとは README の Usage に従って、

```
python rtty8k.py > rtty.csv
```

を実行すれば、Excel なんかで読み込んでグラフ化することができるでしょう。

## 詰まった所

wav ファイルのフォーマットです。
サンプリングレートについては、始めは元ファイルの48kHzのままにして、プログラム側のパラメータ修正で
なんとかしていたのですが、フォーマットは pcm_s16le のままだとダメでした……。

普段 pcm_u8 なんて使わないので。。。README は穴が開くくらい読みましょうという感じでした。
