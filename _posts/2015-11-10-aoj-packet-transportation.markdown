---
layout: post
title:  "AOJ: Packet Transportation"
date:   2015-11-10 14:52:21
categories: aoj
---
[Packet Transportation](http://judge.u-aizu.ac.jp/onlinejudge/description.jsp?id=0144)

普通にダイクストラ法

ノードが繋がっていない場合もあるみたいで、ちゃんとやっていなくて Wrong Answer になってしまった。。。

{% gist tsmsogn/35be8f14ed050c14c084 %}

その他、`Hash` の clone に `Marshal.dump()` というのを覚えた。

{% highlight ruby %}
clone = Marshal.load(Marshal.dump(original))
{% endhighlight %}
