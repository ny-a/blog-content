---
title: "TsukuCTF2021 Writeup(OSINT以外)"
date: 2021-09-15
---

[TsukuCTF](https://tsukuctf.sechack365.com/)

ny_a です。182チーム中5位でした。

## Web

### Logonly

解けませんでした。

デカいログを見てみると、214154行目に攻撃が成功しているという情報しかありませんでした。

Kali Linux は使ったことないな〜、ダウンロードも面倒だし、と思いググってみると、
[kalilinux/wordlists](https://gitlab.com/kalilinux/packages/wordlists) リポジトリに
rockyou というパスワードリストがあるようでした。サイズも十分大きいし、最終更新も8年前なのでバージョンの問題もなさそうです。
ungzip して214154行目の `qwertzu` で incorrect。別ファイルかなーと思い諦めました。

ちなみに、作問者さんに聞いてみた所想定解法っぽいですね。1つ古い？バージョンだと `/dev/null` が入っていないらしいです。なるほど。

guess 問題なのでエスパーすればよかったですね。

### digits

python の `int()` が int を返せば ok そうです。
ドキュメントを見るとアンダースコアを任意の位置に入れることができるようです。

`1_1_1111111`

### Login

SQLi ですか。普通にフレームワークを使ってバックエンドの開発をやっていると、そのような脆弱性を作り込むこともほぼないので、
攻撃方法についてはあまり詳しくなく……。調べながらクエリを投げたらログインできました。

### Login2, Login3

解けませんでした。

同じようにログインはできましたが、あんまり攻撃するのも申し訳なくなってきたので諦めました。
バックエンドエンジニアにこんなことさせないで……と思いましたが、次までには解けるように練習しておきます。

### Journey

HTTP ステータスコードを見ろと言われたので見ると、Method not allowed。

OPTIONS の返答から一つずつ試していくと、CONNECT で referrer 関連のエラーメッセージが出ます。

`curl -XCONNECT --referrer (railwaysのURL)` とかするとフラグが得られます。

### gyOTAKU

解けませんでした。

適当にローカルファイルを iframe に表示する HTML を書いて、適当に GitHub Pages にデプロイしてみたものの、キャッシュの問題か404……。
適当にローカルに nginx コンテナでサーバーを建ててみたものの、ディレクトリ一覧はなぜか表示されず。

`/etc/passwd` とか見るのもかわいそう(？)だと思い試しませんでしたが、試していたら解けていたかもしれません。
いやだからあんまり攻撃させないでください…………。

## Rev

### Legacy code

pentium と書かれている所は x87 FPU の命令っぽいですね。

800.635 + 0.365 をしているようです。ちょうど801くらいになりますね。

それを `PC%d%.0f` で表示しているようです。多分 `PC9801` でしょう。試したら通りました。

$9 って即値なんですね。知りませんでした。

## Network

### Genesis

ブロックチェーンの知識はないですが、データ構造を見ながら前や後を見ていくと、GENESIS と書かれたものを発見。

その tx から、
`/api/getrawtransaction?txid=f44d8ca0b6e787c2193297aec523d685bc0ab5a38eca5a0b014c5a679507b13e&decrypt=1`
にアクセスして、適当に hex を ascii に変換してみたらフラグがありました。

## Crypt

### CrackSSH!

適当に e と n を見てみると、e がデカいのが脆弱なようです。

適当に d を調べて、適当に rsatool で秘密鍵を作ると、ログインが……できません。

多分 ssh-agent が悪いんでしょう。適当に docker コンテナ内から ssh すると入れました。

`flag.txt` ファイルにフラグが書いてありました。

## Misc

### TORitsukushi

VSCodeで開いて適当に s/TSUKUSHI//g な置換をしまくったら、case insensitive になっていたようで incorrect。
case sensitive にしてやり直しました。

### Customization

マンダラートは何か分かりませんでしたが、目標とか書いてあるので9x9のあのなんか、あれでしょうか。
真ん中に目標書いてありそうですよね。背景色が変わっていますが、数式バーには出るので見るだけです。

### discriminate

あー、途中まで見覚えのある文章ですね……。
とりあえず内容が破綻し始める位置のあたりをつけて、ポスターと完全一致している所の末尾5文字を投げてみます。
それでダメだったらモデルを動かして……と思ったのですが、通ったのでヨシ！

## Hardware

### CAD

ご丁寧にも CAD ソフトいらないよと書いてあるので stl online viewer とかでググって適当に開きます。
左右の {} が微妙に違っていて、tかな……？とかやって incorrect になってしまいました。
CTF 初心者なのでフラグ形式でピンと来ず……。

### Ltika

Arduino ですね。丁寧に関数を作って点滅させているようです。
関数名だけ無視して、長いのと短いのがあるのでモールス信号だろうと推測、適当なサイトで復号(？)しました。

### PCB

なんかオンラインのガーバービューアーだと丸い基板みたいな感じに表示されてしまった？ので、
最近はあまり出番のない KiCad を起動して開きます。

そもそも LED と POWER の区別すらしないで適当に星座と見比べていたらそれっぽいのを見つけたので投げてみました。

## Tsukushi

### Welcome

補足にスクリーンネームでいいよって書いてあったのでそちらで。
終わった後にアカウント見たら、ユーザー名がフラグ形式になっていたのでこちらが想定解だったんだなと気付きました。


## 感想

CTF、多分期間の決まっていて一般公開されているものに出るのは初めて？な気がするのですが、出てみるもんですね。楽しかったです。

(上記に該当しないものとして、CpawCTF と、セキュキャンの講義内で CTF 形式の演習はやったことがあります。その程度で、マジの初心者です。いやこれはマジなんですよ。信じて。)

サービスを守るには攻撃手法の概要くらいを知っていればいいか……と思っていたのですが、
具体的な攻撃手法を知ることも大事なのかなと考え直しました。勉強します。

とはいえ、fork bomb で怒られてしまう国ではなかなか難しい気もしないでもないんですよね……。