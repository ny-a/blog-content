---
title: "DNSSECの設定をしました"
date: 2020-02-27
---

クライアント側もドメイン側も、設定するだけで DNSSEC が使える状態になっていたので、両方とも設定して
DNSSEC を有効にしてみました。

## クライアント設定

DNS リゾルバは `systemd-resolved` を使っているので、 DNSSEC 対応の DNS サーバーが使われていれば DNSSEC が有効になります。
`1.1.1.1` や `8.8.8.8` は DNSSEC に対応しています。
しかし、ルーターなどが提供するリゾルバは対応していないことが多いので、それをデフォルトで使っていて無効になっていました。
`1.1.1.1` を直接使うように設定するには、 `/etc/systemd/resolved.conf` に以下の行を追加します。

`DNS=1.1.1.1`

あとは `sudo systemctl restart systemd-resolve` を実行して、 `systemd-resolved` サービスを再起動すれば有効になります。

有効になっていれば、 `resolvectl query sigfail.verteiltesysteme.net` を実行すると `invalid` とエラーが出るはずです。

## ドメインの設定

[DNSSEC対応の独自ドメインを年額$0.88で運用できるよという話](https://hnw.hatenablog.com/entry/20160321)
を見ると、海外のレジストラは DNSSEC に対応しているところが多いようです。
私の使っている `nyaw.dev` は Gandi で取得したため、ボタン1つで有効化することができました。

[nyaw.dev - dnsviz](https://dnsviz.net/d/nyaw.dev/dnssec/)
を確認すると、正常に設定されていることが確認できます。

といっても、リダイレクトさせているのであんまり嬉しくはないんですが……。

ブログだけではなくポートフォリオも含めてページを充実させていって、ドメイン設定もきちんとしていこうと思っています。
