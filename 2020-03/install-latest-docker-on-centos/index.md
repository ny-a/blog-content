---
title: "Dockerの最新版をCentOSにインストールしてみました"
date: 2020-03-06
---

CentOS のパッケージは、普段使っている ArchLinux に比べるとかなり古いです。
しかし、 epel などのレポジトリを使うことで、比較的新しいバージョンを使うことができます。

docker は [CentOS 用のインストールマニュアル](https://docs.docker.com/install/linux/docker-ce/centos/)
があるので、これに従えばよいです。

まず、既に docker がインストールされている場合は `yum remove` コマンドで削除します。
そして、 `yum-utils` `device-mapper-persistent-data` `lvm2` パッケージをインストールします。
(手元の環境では全て最新版がインストールされていました。)
次に、 Docker CE のレポジトリを追加します。
`yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo`

あとは `yum install docker-ce docker-ce-cli containerd.io` を実行すれば最新版がインストールされます。

また、 `docker-compose` はこの状態で yum でインストールしようとすると古いバージョンが入るので、
`pip` を使ってインストールしてあげると最新版がインストールされます。
ただ、インストールが `/usr/local/bin/` 以下になることがあり、 `sudo` 時の PATH に含まれていないことがあるので
注意が必要です。(とりあえずはフルパスで指定すると動きます。)

ArchLinux を使っていると pip も 3 が標準な気がしてしまいますが、他の disto では 3 の suffix がついているんですね。
そろそろ 2 系も EOL なので、 suffix なしの 3 系が標準になってほしいものです。
