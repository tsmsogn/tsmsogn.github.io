---
layout: post
title:  "AOJ: Area of Polygon"
date:   2015-09-29 15:46:03
categories: aoj
---
[Area of Polygon](http://judge.u-aizu.ac.jp/onlinejudge/description.jsp?id=0079)

> 凸 n 角形（すべての頂点の内角が 180 度未満である多角形、要するにへこんでいない多角形のこと）

とのことなので、基準点から反時計回りにソートして、順にヘロンの公式を使って面積を合計した。

{% gist tsmsogn/536ca2f505166053f762 %}
