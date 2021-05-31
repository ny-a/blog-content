---
title: "ChromiumをDockerコンテナ内で実行する"
date: 2021-05-31
---

Chromium を Docker コンテナ内で安定して動かすことができるようになったので
方法をメモしておきます。

[ny-a/chrome-in-docker](https://github.com/ny-a/chrome-in-docker)

上記リポジトリで `docker-compose up --build` すれば済むのですが、解説します。

`SYS_ADMIN` は chrome が namespace の操作権限を必要とするので付けています。
`--no-sandbox` オプションをつけて chrome を起動することでも対処はできますが、非推奨です。
どちらもないと、`Failed to move to new namespace` というエラーが出ます。
(sysctl から設定を変更することでも可能なようですが、Arch標準のカーネルの設定で起動することを考えています。)
参考: [jessfraz/dockerfiles #350](https://github.com/jessfraz/dockerfiles/issues/350)

`network_mode: host` は、ホストの X11 サーバーに直接ウィンドウを表示するために必要です。

`devices: /dev/snd` があると音が出ます。環境によっては ALSA の設定なんかを Docker 内から
見えるようにする必要があるかもしれません。

`${XAUTHORITY}:/home/user/.Xauthority` ボリュームは、X11 の認証に必要です。

`DISPLAY` 環境変数は、X11 サーバーが複数立ち上がっているときに区別するために必要です。
まあほとんどの環境で `:0` にしておけば問題ないはずです。

docker-compose を使いたくなければ、

```
docker build . -t chrome
docker run --rm -te DISPLAY=$DISPLAY --net host -v ~/.Xauthority:/home/user/.Xauthority chrome
```

みたいな感じでいけると思います。

日本語入力したかったらコンテナ内に IME 入れてください。ホストは関係ないので好きなやつを入れることが
できます。
