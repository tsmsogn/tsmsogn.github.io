---
layout: post
title:  "AOJ: Factorial II"
date:   2015-09-11 13:19:24
categories: aoj
---
[Factorial II](http://judge.u-aizu.ac.jp/onlinejudge/description.jsp?id=0052)

> n! の末尾に連続して並んでいる 0 の数を出力して終了するプログラムを作成してください。

「階乗求めて、`10` で割るんでしょ？」と余裕ぶっこいて解くも、上位の人と Time 差が大きい、、、。

調べてみると、`10` で割り切れるということは、素因数分解したら、`2` と `5` がセットで何回でてくるか？ということらしい。

ということで、修正。

{% gist tsmsogn/222beb51df223f5e864d %}

Oh, my code!

{% gist tsmsogn/dbda846983d4cbae469f %}

## Reference sites

- [http://www.geocities.jp/math12345go/math-qa/kaijou.htm](http://www.geocities.jp/math12345go/math-qa/kaijou.htm)
