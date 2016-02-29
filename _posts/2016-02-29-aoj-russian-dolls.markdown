---
layout: post
title:  "AOJ: Russian Dolls"
date:   2016-02-29 10:50:03 +0900
categories: aoj
---
[Russian Dolls](http://judge.u-aizu.ac.jp/onlinejudge/description.jsp?id=0157)

マトリョーシカの性質上、DAG になる。動的計画法を使って解けた。

dp[i] := i個のマトリョーシカを使ってでできる最大のマトリョーシカ

{% highlight ruby %}
while line = gets
  n = line.chomp.to_i
  break if n == 0

  dolls = []
  n.times do
    dolls << gets.chomp.split.map(&:to_i)
  end

  m = gets.chomp.to_i
  m.times do
    dolls << gets.chomp.split.map(&:to_i)
  end

  dolls.sort! do |a, b|
    if a[0] == b[0]
      a[1] <=> b[1]
    else
      a[0] <=> b[0]
    end
  end

  dp = Array.new(dolls.size + 1, 0)

  for i in 1..dolls.size
    for j in 1..i
      if i - j == 0 || (dolls[i - 1][0] > dolls[i - j - 1][0] && dolls[i - 1][1] > dolls[i - j - 1][1])
        dp[i] = [dp[i], dp[i - j] + 1].max
      end
    end
  end

  puts dp.max
end
{% endhighlight %}
