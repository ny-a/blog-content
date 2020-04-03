---
title: "RaspberryPi の乱数生成の速度をテストしてみました"
date: 2020-04-04
---

まず、比較のための普段使いのマシンで `rngtest -c 1000 < /dev/random` を
実行した結果です。rngd のソースにはx86_64 の `rdrand` を使っています。

```
rngtest 6.10
Copyright (c) 2004 by Henrique de Moraes Holschuh
This is free software; see the source for copying conditions.  There is NO warranty; not even for MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.

rngtest: starting FIPS tests...
rngtest: bits received from input: 20000032
rngtest: FIPS 140-2 successes: 1000
rngtest: FIPS 140-2 failures: 0
rngtest: FIPS 140-2(2001-10-10) Monobit: 0
rngtest: FIPS 140-2(2001-10-10) Poker: 0
rngtest: FIPS 140-2(2001-10-10) Runs: 0
rngtest: FIPS 140-2(2001-10-10) Long run: 0
rngtest: FIPS 140-2(2001-10-10) Continuous run: 0
rngtest: input channel speed: (min=6.199; avg=12.255; max=13.673)Mibits/s
rngtest: FIPS tests speed: (min=53.278; avg=113.896; max=138.214)Mibits/s
rngtest: Program run time: 1724040 microseconds
```

平均 12Mibits/s ですね、信頼性はよくわかりませんが……。

次に、RaspberryPi 3B+ での結果です。 `/dev/hwrng` をソースに使っています。

```
rngtest 6.10
Copyright (c) 2004 by Henrique de Moraes Holschuh
This is free software; see the source for copying conditions.  There is NO warranty; not even for MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.

rngtest: starting FIPS tests...
rngtest: bits received from input: 20000032
rngtest: FIPS 140-2 successes: 1000
rngtest: FIPS 140-2 failures: 0
rngtest: FIPS 140-2(2001-10-10) Monobit: 0
rngtest: FIPS 140-2(2001-10-10) Poker: 0
rngtest: FIPS 140-2(2001-10-10) Runs: 0
rngtest: FIPS 140-2(2001-10-10) Long run: 0
rngtest: FIPS 140-2(2001-10-10) Continuous run: 0
rngtest: input channel speed: (min=169.756; avg=203.404; max=252.963)Kibits/s
rngtest: FIPS tests speed: (min=48.533; avg=66.353; max=67.160)Mibits/s
rngtest: Program run time: 96309980 microseconds
```

平均 203Kibits/s です。だいたい 1/60 といったところでしょうか。

これくらい出ればエアギャップコンピュータとして GPG 鍵の生成などを
行ってもストレスないでしょうか。試してみようと思いました。

