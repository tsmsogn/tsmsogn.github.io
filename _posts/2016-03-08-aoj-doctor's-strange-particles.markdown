---
layout: post
title:  "AOJ: Doctor's Strange Particles"
date:   2016-03-08 12:10:35 +0900
categories: aoj
---
[Doctor's Strange Particles](http://judge.u-aizu.ac.jp/onlinejudge/description.jsp?id=0131)

組み合わせの数が `2 ^ 100` で無理ゲーかとおもいきや、最上段の組み合わせの数の `2 ^ 10` でいける。それは、あるマスを反転させるのはそのひとつ下のマスでしかありえないから。

{% highlight ruby %}
def flip(x, y, grid)
  dx = [0, 0, 1, 0, -1]
  dy = [0, -1, 0, 1, 0]

  for i in 0...5
    if x + dx[i] >= 0 && x + dx[i] < 10 && y + dy[i] >= 0 && y + dy[i] < 10
      grid[y + dy[i]][x + dx[i]] ^= 1 
    end
  end

end


n = gets.chomp.to_i

n.times do
  original = []
  10.times do
    original << gets.chomp.split.map(&:to_i)
  end

  for i in 0...(1 << 10)
    clone = Marshal.load(Marshal.dump(original))
    result = Array.new(10) { Array.new(10, 0) }
    for j in 0...10
      if i >> j & 1 == 1
        flip(j, 0, clone)
        result[0][j] = 1
      end
    end

    for y in 1...10
      for x in 0...10
        if clone[y - 1][x] == 1
          result[y][x] = 1
          flip(x, y, clone)
        end
      end
    end

    unless clone.flatten.include?(1)
      result.each do |row|
        puts row.join(' ')
      end
      break
    end
  end
end
{% endhighlight %}
