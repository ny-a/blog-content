---
title: "RPi 上の ArchLinuxArm での DNSSEC signature expired エラーの対処"
date: 2020-04-08
---

[DNSSEC validation failed エラー](/2020-02/dnssec-error/)
に、始めの方は `signature expired` エラーが出ていたと書いていました。
再インストールの際も同じ問題に遭遇したので対処法をメモしておきます。

といっても、時間を合わせるだけです。RPi には RTC が搭載されていないため、
インターネットに接続するまでは平気で時間が遅れてしまいます。
そのため、`signature expired` になっているようでした。

時間を合わせるだけなので、いくつか方法はありますが、事前に時刻設定して
おいた RTC モジュールを接続する、CLI で手動で時刻を設定する、など
でしょうか。

あるいは、DNSSEC 非対応のリゾルバ・DNS サーバーを使うなども可能でしょう。
ArchLinuxARM で割と遭遇しそうな問題なので、フォーラムなど調べてみようと
思いました。

