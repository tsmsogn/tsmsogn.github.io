---
title: Hugoを使ってキュレーションサイトを作ってみる
layout: post
date: '2016-10-05 09:14:35'
categories: hugo
---

Hugo を使ってみました。

## TL;DR

- Jeklly がより柔軟（multi categories など）になったイメージ
- build がかなり早い印象
- 作ったものはこちらです -> [http://skitube.pubstorm.site/](http://skitube.pubstorm.site/)

## Let's Hugo!

Hugo を使って、簡単なキュレーションサイトのようなものを作ってみます。

### Hugoのインストール

<pre>
$ brew update && brew install hugo
$ hugo version
Hugo Static Site Generator v0.16 BuildDate: 2016-06-06T21:37:59+09:00
</pre>

### サイト作成

<pre>
$ hugo new site your_sitename
$ cd your_sitename
$ hugo serve
</pre>

[http://localhost:1313/](http://localhost:1313/)  にアクセスして、真っ白な画面が見えればおｋです。

### テーマを適応する

<pre>
$ mkdir themes
$ cd themes
$ git clone https://github.com/dim0627/hugo_theme_robust.git
$ cd hugo_theme_robust && git checkout b8ce466
$ cd ../../
$ hugo server --theme=hugo_theme_robust
</pre>

再度、[http://localhost:1313/](http://localhost:1313/)  にアクセスすると、テーマが適応されていると思います。

### サイト設定

{% highlight diff %}
diff --git a/config.toml b/config.toml
index 8aa38a5..2e84cd3 100644
--- a/config.toml
+++ b/config.toml
@@ -1,3 +1,3 @@
-baseurl = "http://replace-this-with-your-hugo-site.com/"
-languageCode = "en-us"
-title = "My New Hugo Site"
+baseurl = "http://skitube.pubstorm.site/"
+languageCode = "ja-jp"
+title = "SkiTube"
{% endhighlight %}

### categories、tags的なやつ

categories、tags がデフォルトで、その他にも定義できるようです。

Refer: [https://gohugo.io/taxonomies/usage/](https://gohugo.io/taxonomies/usage/)

{% highlight diff %}
diff --git a/config.toml b/config.toml
index 067912c..8794f8f 100644
--- a/config.toml
+++ b/config.toml
@@ -1,3 +1,8 @@
 baseurl = "http://skitube.pubstorm.site/"
 languageCode = "ja-jp"
 title = "SkiTube"
+
+[taxonomies]
+  category = "categories"
+  location = "locations"
\ No newline at end of file
{% endhighlight %}

### Postの作成

Postを作って、YouTube の動画を入れます。

<pre>
$ hugo new post/skiing-niseko-japan-2014-gopro-hd-hero-2-and-hero-3-black.md
</pre>

{% highlight diff %}
diff --git a/content/post/skiing-niseko-japan-2014-gopro-hd-hero-2-and-hero-3-black.md b/content/post/skiing-niseko-japan-2014-gopro-hd-hero-2-and-hero-3-black.md
new file mode 100644
index 0000000..a7ff8d3
--- /dev/null
+++ b/content/post/skiing-niseko-japan-2014-gopro-hd-hero-2-and-hero-3-black.md
@@ -0,0 +1,10 @@
++++
+date = "2016-10-05T11:14:37+09:00"
+title = "Skiing Niseko Japan 2014 | GoPro HD Hero 2 and Hero 3 Black"
+categories = [ "cool" ]
+locations = [ "niseko" ]
++++
+
+ニセコの雪質の良さが伝わってくる！
+
+{% raw %}{{< youtube PZHQvRVYJlk >}}{% endraw %}
\ No newline at end of file
{% endhighlight %}

`{% raw %}{{< youtube PZHQvRVYJlk >}}{% endraw %}` は、Hugo の Shortcodes を使っています。

Refer: [https://gohugo.io/extras/shortcodes/](https://gohugo.io/extras/shortcodes/)

### layout

`hugo new post/foo.md` コマンドで作られるファイルの雛形を作成することができます。

{% highlight diff %}
diff --git a/archetypes/default.md b/archetypes/default.md
new file mode 100644
index 0000000..769eeaf
--- /dev/null
+++ b/archetypes/default.md
@@ -0,0 +1,6 @@
++++
+date = ""
+title = ""
+categories = []
+locations = []
++++
\ No newline at end of file
{% endhighlight %}

### Analyticsを入れる

Analytics のコードを入れます。

Refer: [https://gohugo.io/extras/analytics/](https://gohugo.io/extras/analytics/)

{% highlight diff %}
diff --git a/config.toml b/config.toml
index ed71ea6..54f5ba2 100644
--- a/config.toml
+++ b/config.toml
@@ -2,6 +2,8 @@ baseurl = "http://skitube.pubstorm.site/"
 languageCode = "ja-jp"
 title = "SkiTube"
 
+googleAnalytics = "UA-54078547-5"
+
 [taxonomies]
   category = "categories"
   location = "locations"
\ No newline at end of file
{% endhighlight %}

### 書き出し

<pre>
$ hugo --theme=hugo_theme_robust
Started building site
0 draft content
0 future content
2 pages created
0 non-page files copied
5 paginator pages created
2 categories created
1 locations created
0 UA-54078547-5 created
0 tags created
in 86 ms
</pre>

`public` 以下に Staticファイルが作られます。

## あわせて読みたい

- [https://yet.unresolved.xyz/blog/2016/10/03/how-to-make-of-hugo-theme/](https://yet.unresolved.xyz/blog/2016/10/03/how-to-make-of-hugo-theme/)
