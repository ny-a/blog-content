---
title: "Firefox の GUI を docker コンテナ内で起動する"
date: 2020-03-20
---

[Qubes OS](https://www.qubes-os.org/) はアプリケーションを VM で分離しますが、 Arch Linux 上で Docker コンテナを利用して
同じようなことを試してみました。

例えば、 Firefox を起動するには以下のようにします。

```shell script
sudo docker run --rm \
  -v /tmp/.X11-unix \
  -v ~/.Xauthority:/home/user/.Xauthority \
  -e DISPLAY \
  -e XAUTHORITY=/home/user/.Xauthority \
  --net host \
  archlinux/base \
  sh -c 'pacman -Syu --noconfirm firefox; useradd user; chown user:user /home/user; su user firefox'
```

Dockerfile には USER instruction があるので、それを使って Xorg を起動中の UID と一致させればよいはずです。

`-v /home/user/.Xauthority` だけだとディレクトリとしてマウントされてしまってうまくいきませんでした。
`--net host` を付けないと、リモートホストからの X 接続と認識されるため、 xhost などが必要になると思います。

また、ウィンドウサイズを FullHD 程度にするとクラッシュしてしまう問題もあります。これはまだ解決法が分かっていませんが、
SSH の X 転送を使って他のマシンの Firefox を起動したときは起きないため、Docker のメモリか cgroup か何かが原因かなと
思っています。

Arch Linux のインストールプロセスは overlayfs と親和性が高そうなので、 pacman のインストールを docker のレイヤーに
置き換えたようなコンテナシステムを作りたいと思っていますが、 alpm hook 周りを理解しないといけなかったり、
まだまだ先は長そうです。
