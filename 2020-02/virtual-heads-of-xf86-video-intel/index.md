---
title: "Xorgの仮想ディスプレイについて調べました"
date: 2020-02-26
---

Linux デスクトップで、他のデバイスを VNC などを使って仮想的にワイアレスディスプレイとして使うために、
仮想ディスプレイを追加する方法を調べました。

## 余っているディスプレイ出力を使う

[[SOLVED] Creating a Virtual Display/monitor - Arch Forum](https://bbs.archlinux.org/viewtopic.php?id=180904)
を見ると、余っている(ディスプレイを接続していない)ディスプレイ出力を使用して仮想ディスプレイを作成することができるようです。
ディスプレイを接続して表示している状態で切断した状態と同じだと思います。

ただ、前回これを使って VNC で接続した場合、リフレッシュレートがかなり下がってしまっていた記憶があるため、
他の方法を探してみました。

## VIRTUAL1を作成する

[Add VIRTUAL output to Xorg - Stack Exchange](https://unix.stackexchange.com/questions/378373/add-virtual-output-to-xorg)
を見てみると、 intel ドライバを使って VirtualHeads を作成することができるようです。

```shell script
sudo pacman -S xf86-video-intel
cat <<EOH | sudo tee /etc/X11/xorg.conf.d/20-intel-virtual-heads.conf
Section "Device"
    Identifier "intelgpu0"
    Driver "intel"
    Option "VirtualHeads" "2"
EndSection
EOH
```

Xorg を再起動すると、output として VIRTUAL1 が追加されています。

ただ、
[Intel Graphics - Arch Wiki](https://wiki.archlinux.jp/index.php/Intel_Graphics#.E3.82.A4.E3.83.B3.E3.82.B9.E3.83.88.E3.83.BC.E3.83.AB)
に書かれていますが、 `xf86-video-intel` は非推奨扱いになっていて、標準の `modesetting` ドライバが推奨されているようです。

とはいえ、
[xorg/xserver Issue#179](https://gitlab.freedesktop.org/xorg/xserver/issues/179)
に issue が上がっていますが、 `modesetting` ドライバに VirtualHeads 機能は追加されていないようです。

modesetting ドライバで仮想ディスプレイを作成する方法も調べてみましたが、うまく情報をみつけることができませんでした。
本当は Xmonad のワークスペースをマシン間で任意に対応させたいのですが……それはかなり難しそうですね。
