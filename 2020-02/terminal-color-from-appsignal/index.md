---
title: "ターミナルの色をAppSignalベースに変更しました"
date: 2020-02-19
---

ターミナルエミュレータは rxvt-unicode を使っていて、デフォルトの白背景で使っているのですが、
黄色の文字がどうにも見えなくて困っていました。

ターミナルの基本的な ANSI escape sequence に対応する色は
[ANSI_escape_code - Wikipedia](https://en.wikipedia.org/wiki/ANSI_escape_code#3/4_bit)
に一覧があります。 rxvt-unicode は xterm のものとほぼ同じようです。

白背景で見やすい色の組み合わせを探してみたところ、
[jeffkreeftmeijer/appsignal.terminal](https://github.com/jeffkreeftmeijer/appsignal.terminal)
が白背景でも黒背景でも見やすく感じたため、試してみました。

itermcolors は XML で RGB それぞれ 0-1 の実数値で表現されているようなので、きっと先人が hex に変換するスクリプトを
公開しているはずです。
Gist にありましたが、 `Color Space` が入っているものに対応していないようだったので、少し修正して
[Gist](https://gist.github.com/ny-a/35fe6c8e9babeff6a0fded6dfb58f563)
に公開しておきました。

さて、基本は上記スクリプトで変換して `Xresources` に設定するだけですが、赤だったところが青になったり、少し違和感を
感じました。そこで、色の対応を似ているものに変更してみました。

```text
URxvt.color0: #463f31
URxvt.color4: #3316c3
URxvt.color2: #50af4c
URxvt.color6: #04aaef
URxvt.color5: #c46109
URxvt.color1: #8f0c8a
URxvt.color3: #8a7d06
URxvt.color7: #c5beb0
URxvt.color8: #5f584a
URxvt.color12: #7255ff
URxvt.color10: #8fee8b
URxvt.color14: #43e9ff
URxvt.color13: #ffa048
URxvt.color9: #ce4bc9
URxvt.color11: #c9bc45
URxvt.color15: #fffbf2

URxvt.foreground: 15
URxvt.background: 0
```

赤というよりマゼンタ、マゼンタというよりオレンジという感じになってしまいましたが
(もしかしたらマゼンタとオレンジを入れ替えた方が自然かも)、
とりあえず今までとあまり変わりなく、視認性がかなり上がりました。

ちなみに、 `urxvtc -fg 15 -bg 0` で起動すると、黒背景にすることができます。

IDEA や VSCode のターミナルの色はそのままですが……設定を同期するのがそれなりに面倒くさいので、色設定などは
設定ファイルを共通化したいものですね。
