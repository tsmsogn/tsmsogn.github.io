---
title: Message InspectorというLINEメッセージをデバッグしてくれるものを作った
layout: post
date: '2018-01-12 16:51:20'
---

![Message Inspector example 1]({{site.baseurl}}/images/Screenshot_20180112-170804.png)

LINE Messaging API を使って、Message Inspector というものを作りました。

[https://line.me/R/ti/p/%40trd4052u](https://line.me/R/ti/p/%40trd4052u)

その名の通り、ユーザの送信したメッセージをトリガーにして、LINEメッセージの内容をデバッグできるようなものです。

バックエンドに Google Apps Script を使用しています。

## 使い方

- 上記の URL より、友達に登録
- メッセージを送信

## 動作イメージ

![Message Inspector example 2]({{site.baseurl}}/images/Screenshot_20180112-170810.png)

## コード

{% gist 4fd25693b7ad9486744265d2ff6f7725 %}
