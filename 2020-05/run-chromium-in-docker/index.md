---
title: "Chromium の GUI を docker コンテナ内で実行する"
date: 2020-05-17
---

前は Firefox でやりましたが、Chromium はサンドボックスがあったりして
前のままのコマンドでは動いていませんでした。

以下のコマンドで動きました。といっても `--privileged` を追加しただけですが。
`--privileged` なしでも `--no-sandbox` をつけて chromium を起動すれば
一応ウィンドウまでは出るのですが、グラフィックドライバがうまく
読み込まれずに真っ白のままになってしまうという問題がありました。

```
sudo docker run --rm \
  -v /tmp/.X11-unix \
  -v ~/.Xauthority:/home/user/.Xauthority \
  -e DISPLAY \
  -e XAUTHORITY=/home/user/.Xauthority \
  --net host \
  --privileged \
  archlinux \
  sh -c 'pacman -Syu --noconfirm chromium; useradd user; chown user:user /home/user; su user chromium'
```

もう少し `--cap-add` などで Capability を絞ってもいけそうですね。

Firefox に比べれば安定しているかなという印象ですが、やはり
YouTube などを FullHD で視聴しようとするとタブがクラッシュしてしまうので、
実用には厳しいかなという印象でした。

わざわざ Docker 内で起動しなくても、psd なんかで毎回リセットするように
してあげればほぼ同じことが実現できるんですけどね……。

