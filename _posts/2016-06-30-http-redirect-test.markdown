---
layout: post
title:  "http_redirect_testの紹介"
date:   2016-06-30 15:57:21 +0900
categories: shell
---
シェルスクリプトでリダイレクトテストができるツールを作りました。その名も `http_redirect_test` というそのままの命名。

リダイレクトだけじゃなく、ステータスコード `200`、`404` と `410` にも対応しています。

[http_redirect_test](https://github.com/tsmsogn/http_redirect_test)

## 使い方

<pre>
./http_redirect_test.sh [OPTIONS...] source_path destination_path
</pre>

実行結果は、`$?` で取れます。`0` で成功、`1` で失敗です。

## Let's try

### リダイレクトだけのテスト

{% highlight shell %}
# Succeeded
./http_redirect_test.sh http://httpstat.us/301 http://httpstat.us
echo $? # 0
{% endhighlight %}

{% highlight shell %}
# Failed
./http_redirect_test.sh http://httpstat.us/302 http://httpstat.us/404
echo $? # 1
{% endhighlight %}

### `--status`オプションで、ステータスコードを指定

{% highlight shell %}
# Succeeded
./http_redirect_test.sh --status 301 http://httpstat.us/301 http://httpstat.us
echo $? # 0
{% endhighlight %}

### ステータスコード 200のテスト

{% highlight shell %}
# Succeeded
./http_redirect_test.sh --status 200 http://httpstat.us/200
echo $? # 0
{% endhighlight %}

### `--debug`オプションでデバッグ

{% highlight shell %}
# Succeeded
./http_redirect_test.sh --debug http://httpstat.us/301 http://httpstat.us
# ---> http://httpstat.us/301
# Expected: status:  url: http://httpstat.us
# Actual: status: 301, url_effective: http://httpstat.us, redirect_url: http://httpstat.us
echo $? # 0
{% endhighlight %}

### もちろん一括テストもできちゃいます

{% highlight shell %}
#!/bin/sh

succeeded=0
failed=0

for source_destination in \
    "http://httpstat.us/300" \
    "http://httpstat.us/301 http://httpstat.us" \
    "http://httpstat.us/302 http://httpstat.us" \
    "http://httpstat.us/303 http://httpstat.us"
do
    source=`echo $source_destination | cut -f1 -d" "`
    destination=`echo $source_destination | cut -f2 -d" "`

    ./http_redirect_test.sh $source $destination

    case $? in
        0)
            succeeded=`expr $succeeded + 1`
            ;;
        *)
            failed=`expr $failed + 1`
            ;;
    esac
done

echo "succeeded: $succeeded, failed: $failed"
# succeeded: 4, failed: 0
{% endhighlight %}

## その他

バグレポートや機能追加の `PR` お待ちしてます！

## Thanks

- Ruby で書かれた [http_redirect_test](https://github.com/eightbitraptor/http_redirect_test) に大変影響を受けています
