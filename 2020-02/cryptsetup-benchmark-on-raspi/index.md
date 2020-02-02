---
title: "RasPiでcryptsetup benchmarkを実行してみました"
date: 2020-02-03
---

タイトルの通りですが……
RaspberryPi 3B+ で `cryptsetup benchmark` を実行してみました。

```shell script
$ cryptsetup benchmark
# Tests are approximate using memory only (no storage IO).
PBKDF2-sha1       206738 iterations per second for 256-bit key
PBKDF2-sha256     316599 iterations per second for 256-bit key
PBKDF2-sha512     200415 iterations per second for 256-bit key
PBKDF2-ripemd160  174529 iterations per second for 256-bit key
PBKDF2-whirlpool   29153 iterations per second for 256-bit key
argon2i       4 iterations, 172077 memory, 4 parallel threads (CPUs) for 256-bit key (requested 2000 ms time)
argon2id      4 iterations, 177813 memory, 4 parallel threads (CPUs) for 256-bit key (requested 2000 ms time)
#     Algorithm |       Key |      Encryption |      Decryption
        aes-cbc        128b        28.2 MiB/s        56.6 MiB/s
    serpent-cbc        128b               N/A               N/A
    twofish-cbc        128b               N/A               N/A
        aes-cbc        256b        22.6 MiB/s        42.7 MiB/s
    serpent-cbc        256b               N/A               N/A
    twofish-cbc        256b               N/A               N/A
        aes-xts        256b        63.9 MiB/s        55.9 MiB/s
    serpent-xts        256b               N/A               N/A
    twofish-xts        256b               N/A               N/A
        aes-xts        512b        48.2 MiB/s        42.3 MiB/s
    serpent-xts        512b               N/A               N/A
    twofish-xts        512b               N/A               N/A
```

メインのマシンより1-2桁くらい遅くてびっくりしました。
RasPi でフルディスク暗号化とか少し検討していたのですが、これでは実用性が怪しいですね……
メモリがもっと潤沢にあれば PXE ブートなんかでディスクレスにしてもよさそうなんですが、RasPi4 でも 4GB とかなので、
もう少し欲しいな……と思っています。まあ USB ストレージから起動できるし当面問題はなさそうですが。
