---
title: "AGC054-A"
date: 2021-06-28
---

今日は AGC054 に参加しました。レーティングは変化しませんが。

A 問題以外はとても解けそうにないので、とりあえず A 問題に挑戦しました。

見た感じ、答えは -1,1,2 のいずれかになりそうです。
が、3以上になる可能性もありそうで、入力サンプルからはその可能性の検証は難しそうでした。

そこで、一旦愚直に実装してみます。
10^5 だと N^2 は通らなさそうなので、なんとか高速化の方法を考えます。

まず、できるだけ最長の部分列を消したいので、先頭から見ると考えると、
末尾と一致しない文字ができるだけ早く出現するところから見るとよさそうです。

いちいち探索していると遅いので、グラフみたいに簡単に引けるようにしておきたいです。
今回は文字の種類が26種類で、末尾の文字に対して先頭の文字は異なる文字を探したいので、
文字種ごとに vector を用意して、それぞれに一致する文字以外の vector に push_back していきます
(分かりにくい)。

そして、あとは DFS の要領で……。TLE しました。

即座に値を返す条件を追加して……。TLE しました。

ループ内で既に見た先頭部分は見ないようにして……。TLE しました。

DFS 全体で既に見た先頭部分は見ないようにして(！！？？)、AC しました！

解説見たら始めの直感合ってそうですね。とほほ。