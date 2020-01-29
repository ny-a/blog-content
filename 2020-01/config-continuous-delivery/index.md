---
title: "GitHubActionsを使ってデプロイを自動化しました"
date: 2020-01-30
---

先日はブログのコンテンツと Gatsby のテンプレートを分離しましたが、
コンテンツを push すると CI/CD で自動でビルド・デプロイまでできるようにしました。

ビルド環境は Gatsby の方のレポジトリですが、 push でトリガーされるのはコンテンツのレポジトリなため、
[GitHub のフォーラム](https://github.community/t5/GitHub-Actions/Triggering-by-other-repository/td-p/30668)
を参考に、コンテンツのレポジトリに push されたときに Gatsby のレポジトリのビルドをトリガーするようにしました。

この調子で Gridsome と Jekyll もビルド・デプロイを自動化して、デザインを統一しようと思います。
3つもデプロイする必要はないですが……。
