---
layout: post
title:  "AOJ: Blackjack"
date:   2016-02-29 15:03:23 +0900
categories: aoj
---
[Blackjack](http://judge.u-aizu.ac.jp/onlinejudge/description.jsp?id=0169)

動的計画法問題

dp[i][j] := i枚のカードを使った時、合計jとなる組み合わせの数

{% highlight ruby %}
while line = gets
  break if line.chomp == '0'

  cards = line.chomp.split.map(&:to_i)

  dp = Array.new(cards.size + 1) { Array.new(22, 0) }

  dp[0][0] = 1

  for i in 0...cards.size
    card = cards[i]
    for j in 0...22
      if card == 1
        dp[i + 1][j] = [dp[i + 1][j], dp[i][j - 1]].max if j - 1 >= 0 && j - 1 < 22
        dp[i + 1][j] = [dp[i + 1][j], dp[i][j - 11]].max if j - 11 >= 0 && j - 11 < 22
      else
        card = 10 if card > 10
        dp[i + 1][j] = dp[i][j - card] if j - card >= 0 && j - card < 22
      end
    end
  end

  a = 0
  for i in 0...22
    a = i if dp[cards.size][i] == 1
  end
  puts a
end
{% endhighlight %}
