---
title: Webhooksを使って自動でdeployするときに、ちょっと安全にgit pullしてくれるものを作った
layout: post
date: '2016-09-09 04:38:31'
categories: git
---

## TL;DR

-  ローカルリポジトリに `HEAD` と差分がない
-  ローカルリポジトリのコミットがリモートリポジトリより進んでいない

時に、`git pull` するシェルスクリプトを書いた。

また、使用するには以下の条件が必要です。

- .gitignore に追加するなどして、Gitプロジェクトに不要なファイルがないこと
- リモートリポジトリにパスフレーズなしでアクセスできること
- Webユーザとローカルリポジトリの所有者が同一であること

{% gist db7d47e7378089ed6165155c16b1bcd5 %}

## 背景

本番環境の Gitプロジェクトを Gitを扱えない人が変更するような状態があって、
Webhooks を使って自動で deploy する時に、何かしらのファイルに更新があることを検出したい、もし変更があれば、反映しないようにしたいと思って作りました。

## 勉強になったこと

- `git rev-parse --abbrev-ref HEAD` で `HEAD` のブランチ名を取得できる
- [https://git-scm.com/docs/git-rev-list](https://git-scm.com/docs/git-rev-list) を知った
- Shell の `-a` と `&&` では挙動が違う。`-a` は右辺・左辺とも実行され評価される。それに対して  `&&` ではまず左辺だけが実行され評価される
- Shell の exitコードにも意味がある。[http://tldp.org/LDP/abs/html/exitcodes.html](http://tldp.org/LDP/abs/html/exitcodes.html)

## あわせて読みたい

<a href="https://www.amazon.co.jp/%E8%A9%B3%E8%A7%A3-%E3%82%B7%E3%82%A7%E3%83%AB%E3%82%B9%E3%82%AF%E3%83%AA%E3%83%97%E3%83%88-Arnold-Robbins/dp/4873112672/ref=as_li_ss_il?ie=UTF8&qid=1473748899&sr=8-3&keywords=%E3%82%B7%E3%82%A7%E3%83%AB%E3%82%B9%E3%82%AF%E3%83%AA%E3%83%97%E3%83%88&linkCode=li2&tag=tsmsogn-22&linkId=6cae7856259489b0dfe371b0f3de5ea8" target="_blank"><img border="0" src="//ws-fe.amazon-adsystem.com/widgets/q?_encoding=UTF8&ASIN=4873112672&Format=_SL160_&ID=AsinImage&MarketPlace=JP&ServiceVersion=20070822&WS=1&tag=tsmsogn-22" ></a><img src="https://ir-jp.amazon-adsystem.com/e/ir?t=tsmsogn-22&l=li2&o=9&a=4873112672" width="1" height="1" border="0" alt="" style="border:none !important; margin:0px !important;" />