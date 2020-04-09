---
title: "RPi に aarch64 の ArchLinux を入れて RTC モジュールを有効化してみる"
date: 2020-04-09
---

ArchLinuxARM では簡単に RTC が有効化できた記憶があったのですが、再度試してみると
うまくいかなかったのでいろいろ試してみました。


まず、前に設定して動いている Raspbian の `dmesg` を見てみます。

```
[    5.310771] rtc-ds1307 1-0068: registered as rtc0
```

このログの通り、 `/dev/rtc0` ができていて、時刻同期はスクリプトで行われます。

一方、ArchLinuxARM だと以下のようなログが出ていました。

```
[    7.114025] hctosys: unable to open rtc device (rtc0
...
[    7.258978] i2c-bcm2835 3f805000.i2c: Could not read clock-frequency property
```

`/dev/rtc0` も起動時は存在しない状態で、
`echo 'ds1307 0x68' | sudo tee /sys/bus/i2c/devices/i2c-1/new_device`
を実行しないといけません。

- https://archlinuxarm.org/forum/viewtopic.php?t=11802
- https://gist.github.com/Alex131089/de45d552372a9296abbbbe407ae52180
- https://raspberrypi.stackexchange.com/questions/38186/how-to-install-real-time-clock-rtc-on-raspbian

上記のようなサイトをいくつか参照したのですが、ずばりの(？)解決策は
なさそうです。よく考えたら Raspbian と違い aarch64 でした……

`hctosys` は `systemd` の起動前に(initramfs で)実行されているようです。
initramfs 内の udev に認識させればいけそうでしょうか。

