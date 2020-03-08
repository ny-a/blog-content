---
title: "CoreOS rktプロジェクトが終了していました"
date: 2020-03-08
---

CoreOS のプロジェクトが終了して Fedora CoreOS が後続になるという話は知っていたのですが、
rkt プロジェクトもそれに伴って終了していたようです。

[Github の rkt/rkt](https://github.com/rkt/rkt) も Archived になっていて特に代替になるものや
活発に開発されている fork も今のところなさそうです。

他のコンテナランタイムとしては [runc](https://github.com/opencontainers/runc)
や、 kubernetes 用の [cri-o](https://github.com/cri-o/cri-o) などもありますが、
runc は containerd から利用されているようで(前 Docker のリリースか何かで読んだ気がする)、
Docker/rkt を置き換えるものではないですね……。

まあ単純に Docker を使えばいいんだとは思いますが……、Docker のセキュリティ面での懸念に対処していた
rkt プロジェクトが終了してしまうのは個人的に残念でした。
