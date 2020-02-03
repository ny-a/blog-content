---
title: "新しいGPGキーを作成しました"
date: 2020-02-04
---

Yubikey もあることですし、そろそろ GPG や SSH の秘密鍵を統一しようと思います。
[GPGで自分用の秘密鍵を1つに統一する](http://joemphilips.com/post/gpg_memo/)
を参考に進めていきました。

上記記事ではエアギャップコンピュータが推奨されていますが、今回はマスターキーのバックアップの
利便性のため、ネットワークに接続した状態で行いました。
[QUBES OS](https://www.qubes-os.org/) はよさそうですね。 Fedora ベースなのが
少し気になるといえばそうですが……(ArchLinux に慣れているため)。

さて、普段使いの環境にはマスターキーの秘密鍵は置いておきたくないので、
マスターキーの生成は別の環境で行います。
バックアップの利便性なども考えて、 LUKS で暗号化したパーティションをファイルに保存します。

```shell script
dd if=/dev/zero of=encrypted_partition.img bs=1M count=64
sudo cryptsetup luksFormat -i 5000 --use-random encrypted_partition.img
# type 'YES' and set password
sudo cryptsetup luksOpen encrypted_partition.img gpg_container
sudo mkfs.ext4 /dev/mapper/gpg_container
sudo mount /dev/mapper/gpg_container /mnt
sudo mkdir /mnt/.gnupg
sudo chown [current_user] /mnt/.gnupg
```

GPG の操作は今作成した `/mnt/.gnupg` を GNUPGHOME に設定して行います。
必要なだけマスターキーとサブキーを作成していきます。

```shell script
GNUPGHOME=/mnt/.gnupg gpg --full-gen-key
```

作成が終わったら、サブキーだけをエクスポートします。キーの fingerprint は `gpg -K` で確認できます。

```shell script
GNUPGHOME=/mnt/.gnupg gpg --output [exported-file] --export-secret-subkeys [fingerprint]
```

エクスポートしたファイルを scp などで普段使う環境にコピーしたら、インポートして信頼します。
今自分で作成したキーなので、信頼度は 5 (I trust ultimately) でよいでしょう。

```shell script
gpg --import [exported-file]
gpg --edit-key [fingerprint]
    > trust
    > 5 # I trust ultimately
    > save
```

あとは、 `gpg -K --with-keygrip` で ssh に使いたいキーの keygrip を確認して、 `~/.gnupg/sshcontrol` に追加します。
`~/.ssh/config` の `IdentityFile` でキーを指定する場合は、 `gpg -K --with-subkey-fingerprint` でサブキーの
fingerprint を確認して、 `gpg --export-ssh-key [fingerprint] > ~/.ssh/id_something.pub` を実行します。
`IdentityFile` には今作成した `id_something.pub` を指定してください。

gpg-agent を ssh-agent として使う方法は
[GnuPGのssh-agentエミュレータを使ってみました](/2020-01/introduction-of-gpg-ssh-agent/)
に書いた通りです。

addkey をする場合やサブキーの有効期限を変更する場合などはマスターキーが必要になりますが、
それまではマスターキーの秘密鍵がない状態でうまく機能するでしょう。
将来的にはオフラインのマシン上で行いたいですが、ひとまず普段から GPG を使う習慣をつけて
慣れておこうと思っています。
