---
title: "RTTY のデコードを試す(6)"
date: 2021-06-24
---

さて、いよいよ ITA2 のデコードに進んでいこうと思います。

基本的には5ビットごとに切り出してコード表と対応させるだけなんですが、
その5ビットの区切りを見つけるのも一工夫必要そうです。

また、区切りとなるストップビットの長さも設定によってバラバラのようです。
そこで、スタートビットとストップビットの組み合わせが判明していると仮定して
(といっても2パターンしかないですが)、ストップビットの長さについては
任意の長さを受け入れられるようにしようと思います。

まず、始めに出てきたストップビット→スタートビットの変化を検出します。
ここではデータ列内にマッチする可能性もありますが、始めの何文字かを捨てることを許容できれば、
後で説明するようにいつかきちんとした区切りを検出できるようになるので、
ここでは気にしないことにします。

次のビットからは、データ列です。5ビット連続で読み込みましょう。
(データ列が下位ビットからか上位ビットからかは分かりません……が、
これも2パターンなのでなんとかなるでしょう。)

さて、ストップビットを検出するわけですが……、検出しません！！
長さも分からないですし、そもそもズレている場合もあるので、
次のストップビット→スタートビットの変化を検出するまで読み飛ばします。
そうすることで、ズレていても(多分)いつか正しい位置に補正されるわけです。

いや、試してないので分かりません！そう信じて実装しました！！

……という感じでデコードしてみると、うまくデコードできたようです。
よかった。。。
