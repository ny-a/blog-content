---
title: "ブラウザ上でssh-keygenができるツール"
date: 2020-02-11
---

[ssh-keygenをブラウザだけでローカルで安全に鍵生成するWebアプリ](https://scrapbox.io/nwtgck/ssh-keygen%E3%82%92%E3%83%96%E3%83%A9%E3%82%A6%E3%82%B6%E3%81%A0%E3%81%91%E3%81%A7%E3%83%AD%E3%83%BC%E3%82%AB%E3%83%AB%E3%81%A7%E5%AE%89%E5%85%A8%E3%81%AB%E9%8D%B5%E7%94%9F%E6%88%90%E3%81%99%E3%82%8BWeb%E3%82%A2%E3%83%97%E3%83%AA)
を見つけました。

[Secure ssh-keygen only on Web browser](https://ssh-keygen.netlify.com/)

[Web Crypto API](https://developer.mozilla.org/en-US/docs/Web/API/Web_Crypto_API)
を使って実現しているようです。

上記の Web アプリでは RSA にしか対応していませんが、 Web Crypto は ECDSA にも対応しているようです。
EdDSA には対応していないんでしょうか。
乱数ソースも提供されているので、 EdDSA は javascript で実装してしまえば……などと思いました。
EdDSA についてあまりよく分かっていないので調査しようと思いました。
