---
layout: post
title:  "AOJ: Smart Calculator"
date:   2016-03-01 11:36:01 +0900
categories: aoj
---
[Smart Calculator](http://judge.u-aizu.ac.jp/onlinejudge/description.jsp?id=0109&lang=jp)

<pre>
演算はすべて整数で行い、小数点以下切捨てとします。
</pre>

をちゃんとできていなくて、`WA`。。。

{% highlight ruby %}
class Fixnum
  def /(o)
    self.fdiv(o).to_i
  end
end

n = gets.chop.to_i

n.times do
  puts eval(gets.chop.gsub(/=$/, ''))
end
{% endhighlight %}

`Numeric#fdiv` を覚えた。
