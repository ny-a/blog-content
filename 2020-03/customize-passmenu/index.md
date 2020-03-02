---
title: "passmenu をカスタマイズしてみました"
date: 2020-03-03
---

パスワードマネージャーには [Pass / password-store](https://www.passwordstore.org/) を使っていて、
GUI 環境での入力には `passmenu` を使っているのですが、 passmenu のデフォルト動作は クリップボードへのコピーで、
直接入力させるには `--type` オプションを付ける必要があり少し面倒だったので、動作をカスタマイズしてみました。

オリジナルのソースは [contrib/dmenu](https://git.zx2c4.com/password-store/tree/contrib/dmenu/passmenu) にあります。
pass は全体がそうなのですが、中身はシンプルな bash スクリプトなので、好きなように修正してしまいます。

```shell script
#!/usr/bin/env bash

shopt -s nullglob globstar

line=1
if [[ "$1" =~ ^[0-9]+$ ]]; then
  line=$1
  shift
fi

prefix=${PASSWORD_STORE_DIR-~/.password-store}
password_files=( "$prefix"/**/*.gpg )
password_files=( "${password_files[@]#"$prefix"/}" )
password_files=( "${password_files[@]%.gpg}" )

password=$(printf '%s\n' "${password_files[@]}" | dmenu)

[[ -n $password ]] || exit

pass $@ "$password" | tail -n+$line | head -n1 | tr -d '\n' | xdotool type --clearmodifiers --file -
```

- 直接 type して欲しいときの方が多いのでデフォルト動作を type に変更
  (コピーしたかったら pass コマンドを使うので、というか直接 type させる以外する必要ない気が……)
- 複数行に対応するため、1つめの引数が数字であればその行を出力するように変更
- otp なども入力できるように、以降の引数は dmenu ではなく pass に渡すように変更

などをしました。

dmenu にオプション渡してどうしたいんだろう……と思ってしまいました。 dmenu に慣れていないだけなんでしょうか？
それはともかく、パスワードを pass にがっつり依存してしまっているので、このスクリプトでかなり便利になりました。

pass was written by Jason A. Donenfeld of zx2c4.com and is licensed under the [GPLv2](http://www.gnu.org/licenses/gpl-2.0.html)+

contrib なのでライセンス違うような気もしますがそうでもない気もします。contrib だから違うってことはないか。はい。
