---
title: "GPU 上で FFT を計算する"
date: 2021-06-03
---

GPU で何を計算するかのアイデアを探していたのですが、
よく考えたら FFT も GPU 上で計算できそうだと思って
少し調べてみました。

すると、2次元 FFT の話題が多いようでした。
2次元の周波数成分といえば、JPEG の圧縮に使われている
やつですね……(あれは DCT ですが)。

数は比較的少なそうですが、FFT の並列計算に関する話題もありました。
[GPU を用いた高スループット計算システムの実装](https://www.cs.hiroshima-u.ac.jp/WTCS2014/lib/exe/fetch.php?media=d-4.pdf) など。

実際に実装に進んで……といきたいところですが、まずは
FFT を CPU で計算してみて (numpy にもあったはず)、
それを使うコードを書くのが先ですかね……。

……とここまで書いておいてあれですが、PyVideoCore の
作者の方の [Qiita 記事](https://qiita.com/9_ties/items/15ab7fa198991a61a3a9) に

> 他の人が書いたFFT(公式サンプルとしてraspbianに収録)

……既にあるみたいですねw

[GPU_FFT](http://www.aholme.co.uk/GPU_FFT/Main.htm)

これとかでしょうか。
バタフライ演算の図なんかもあり、FFT の知識がなくても
これを読むだけで勉強になりそうです！(？)
