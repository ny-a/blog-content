---
title: "AlpineLinux のパッケージのシステムは ArchLinux 由来です！"
date: 2020-04-01
---

エイプリルフールネタです、と言いたいところなんですが、どうやら事実のようです……。

[AlpineLinux の Wiki](https://wiki.alpinelinux.org/wiki/Alpine_Linux:Overview#Technical_overview)
によると、 `makeinitcpio`, `makepkg`, `pacman`, `PKGBUILD`, `ABS` あたりと非常に
似たシステムになっているようです(もっとも、コンテナで使うときは initramfs は
使いませんが……。)

AlpineLinux はコンテナ上でよく使っているので、これからコミュニティの雰囲気に
慣れていって、少しずつ貢献を始めていこうと思いました。
ただ、 ArchLinux への貢献も続けていきたいので、どう両立させていくかというのは
今後の課題です……。

