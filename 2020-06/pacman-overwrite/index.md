---
title: "pacman の --overwrite についてよく分かっていない"
date: 2020-06-15
---

pacman の --overwrite オプションは滅多に使わないですが、パッケージが
壊れてしまったときなどには使うことがあります。

ただ、ワイルドカードがどのように解決されていて、ディレクトリを再帰的に
含めてくれるのか……などは分かっていません。

そういえば、昔は --force オプションなんかがあったような気がするのですが、
今見たらないようでした。なくなったんですかね？

--force にしろ --overwrite にしろ、上書き前にはそれぞれのファイルの状態を
確認しておきたいものです。私だったら、
[ArchWiki](https://wiki.archlinux.org/index.php/Pacman/Tips_and_tricks#Listing_all_changed_files_from_packages)
を参照して `paccheck --md5sum --quiet` なんかで壊れていそうなファイルの
一覧を得て、それぞれのファイルを確認してから xargs なんかで overwrite
するような気がします。

まあ時々再インストールしてあげるのもいいと思いますけどね。

