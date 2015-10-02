---
layout: post
title:  "AOJ: Square Searching"
date:   2015-10-02 09:58:13
categories: aoj
---
[Square Searching](http://judge.u-aizu.ac.jp/onlinejudge/description.jsp?id=0092)

動的計画法で解けた。

> dp[i][j] に (i, j) を正方形の右下とする最大の正方形の大きさを入れる。

らしい。こんなの思いつかないYO!

{% gist tsmsogn/408279df5f93a671e100 %}

安心してください。総当りでやって TLE しました。。。orz

{% gist tsmsogn/79a480bcd4cbb3c217f7 %}
