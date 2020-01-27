---
title:  "AndroidアプリでHelloWorldをしました"
date:   2020-01-11
---

今まで Android アプリ開発には Android Studio を使っていて、
IntelliJ IDEA と両方使っていたのですが、 Android アプリも
Intellij IDEA で開発してみました。

## 背景

今までも何度か IntelliJ で Android アプリの開発を試みていたのですが、
謎のエラーに悩まされていて、特に Visual Layout Editor が機能しなくて困っていました。

`Sync Project with Gradle Files` を選ぶと以下のエラーが出ていました。

```
New Gradle Sync is not supported due to containing Kotlin modules
```

## 原因

上記のエラーメッセージで検索すると、皆さんいろいろな方法で解決されているようですが、
私はどの方法でも解決しませんでした。

結論としては、システムの JRE のバージョンが 13 だったことが原因だったようです。

[Java - Arch Wiki](https://wiki.archlinux.org/index.php/Java#Launching_an_application_with_the_non-default_java_version)
を参考に、 IntelliJ を Java8(1.8) を使って起動するようにしたら解決しました。

## 感想

IntelliJ の設定は複雑すぎる気がします……
とはいえ、新しい IDE を使う度に同じことを思っている気もします。

シンプルにすればいいというわけではないですが、エラーメッセージはもう少し詳細に書いてほしいのと、
プロジェクト作成などある程度のことは CLI でもできるようにするなど、
問題の切り分けがやりやすくなればいいなと思いました。
