---
layout: post
title:  "シェルスクリプトでHTTPステータスコードをチェックできるものを作った"
date:   2016-09-04 23:37:19 +0900
categories: shell
---
シェルスクリプトで HTTPステータスコードをテストできるものを作った。

[http_status_code_test](https://github.com/tsmsogn/http_status_code_test)

## 使用例

{% highlight shell %}
./http_redirect_test.sh --status 200 http://tsmsogn.github.io/
{% endhighlight %}

実行結果は、`$?` で取れます。`0` で成功、`1` で失敗です。

また、`--`オプションで以下の引数を、内部で使用している `curl` に渡すことが出来ます。Basic認証など必要なときはこのオプションを使用してください。

## まとめ

以前作った [http_redirect_test](https://github.com/tsmsogn/http_redirect_test) の 2番煎じです。orz
