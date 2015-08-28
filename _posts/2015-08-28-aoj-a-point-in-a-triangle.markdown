---
layout: post
title:  "AOJ: A Point in a Triangle"
date:   2015-08-28 10:09:20
categories: aoj
---
[A Point in a Triangle](http://judge.u-aizu.ac.jp/onlinejudge/description.jsp?id=0012)

点P が ΔABC の内部に存在するなら、ΔABC の面積（S）、ΔABP の面積（S1）、ΔBCP の面積（S2）、ΔCAP の面積（S3）には `S = S1 + S2 + S3` が成り立つ。

「ヘロンの公式使えば余裕！」とほざきながら、解いてみるも誤差問題でぶち当たる。。。

何か他に方法はないかと探していたら、外積を使う方法があるらしいので、そちらで解いてみる。

{% gist tsmsogn/74a91b22ea79d39db0c9 %}

蛇足: ヘロンの公式使って「A Point in a Triangle」

{% gist tsmsogn/948a407bb07724b8ebcb %}

## Reference sites

- [http://kone.vis.ne.jp/diary/diaryb09.html](http://kone.vis.ne.jp/diary/diaryb09.html)
- [http://www.deqnotes.net/acmicpc/2d_geometry/products](http://www.deqnotes.net/acmicpc/2d_geometry/products)
