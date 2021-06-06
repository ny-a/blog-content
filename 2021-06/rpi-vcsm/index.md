---
title: "rpi-vcsmが更新されました"
date: 2021-06-06
---

[Idein/rpi-vcsm](https://github.com/Idein/rpi-vcsm) の [issue #2](https://github.com/Idein/rpi-vcsm/issues/2) で
vcsm-cma に対応していただけるとのことだったのですが、今日 GitHub から通知が来て、
なんともう対応していただけたようです。すごく早い……ありがたいですね。

早速最新のカーネルで試してみましょう。`5.10.17-v7+` で試しました。

先に rpi-vcsm をインストールします。書いてある通りです。インストールできたら py-videocore の
example を試してみましょう。

py-videocore の方にも PR が出されているので、[フォークされたブランチ](https://github.com/Terminus-IMRC/py-videocore/tree/rpi-vcsm-3) を
clone してきます。あとは書いてある通りに試していくと……エラーが出ますね。

`ImportError: libf77blas.so.3: cannot open shared object file: No such file or directory`

numpy のインストール時の常識でしょうか……。`sudo apt-get install libatlas-base-dev` しましょう。

```
$ python3 examples/sgemm.py 
==== sgemm example (96x363 times 363x3072) ====
threads: 12
numpy: 0.4205 sec, 0.5113 Gflops
GPU: 0.0294 sec, 7.3126 Gflops
minimum absolute error: 0.0000e+00
maximum absolute error: 9.1553e-04
minimum relative error: 0.0000e+00
maximum relative error: 1.0522e+01
```

ちゃんと動いているようです。

最新カーネルでも py-videocore が動くことを確認できました。
これでネクストキャンプも安心ですね！
