---
layout: post
title:  "Disjoint-set with Ruby"
date:   2015-03-19 13:17:05
categories: ruby
---
自分の友達 `安倍` さん、その `安倍` さんの友達 `オバマ` さんと、 `安倍` さんを介して自分とつながっているとするならば、
つながりを一旦調べると、以後、 `安倍` さんを介してつながりの確認をする必要がない。
そんなことが出来てしまうのが Disjoint-set だ。

{% gist tsmsogn/ed83f73ecd763f0dad17 %}

Disjiont-set を使って Connected component が解けたり、Minimum spanning tree の Kruskal's algorithm なんかで使われる。

## Reference sites

- [http://www.mathblog.dk/disjoint-set-data-structure/](http://www.mathblog.dk/disjoint-set-data-structure/)
