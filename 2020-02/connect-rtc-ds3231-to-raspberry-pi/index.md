---
title: "RaspberryPi(Raspbian)にRTCモジュール(DS3231)を接続しました"
date: 2020-02-08
---

エアギャップコンピュータを準備するにあたって、時刻合わせは面倒な課題です。
特に GPG などで証明書を発行する場合、発行する日の情報は必要不可欠だからです。

ただ、普通のコンピュータは NTP などでインターネットから時刻情報を取得できますが、
Raspberry Pi をオフラインで使用すると、 RTC モジュールが搭載されていないため、
毎回時刻を手動で合わせる必要があります。

そこで、 I2C 接続で 1000円程度で買うことができる RTC モジュールを接続してみました。

Raspbian での設定は
[Install DS3231 Real Time Clock - Latest Info](https://www.raspberrypi.org/forums/viewtopic.php?t=161133)
に書いてある通りです。
ArchLinux だと `/boot/config.txt` の1行だけでいけたかもしれません。明日もう一度確認してみます。
