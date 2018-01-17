---
title: Scrapyを使ってURLを再帰的に辿り、サイトまるごとスクレイピングする
categories: scrapy
---

## 何をするの？

Scrapy を使って [http://tsmsogn.github.io/](http://tsmsogn.github.io/) の各ページのタイトルを取得します。

## そもそもScrapyって？

> Scrapy is a fast high-level web crawling and web scraping framework, used to crawl websites and extract structured data from their pages. It can be used for a wide range of purposes, from data mining to monitoring and automated testing.

とあるように、クローリング・スクレイピングする Python 製のフレームワークです。

## Let's scraping

### Scrapyをインストール

```
$ pip install scrapy
```

### プロジェクトを作成する

```
$ scrapy startproject tsmsognScrapy
$ cd tsmsognScrapy
```

### Spiderを作成

```
$ scrapy genspider tsmsogn tsmsogn.github.io
```

### データの出力データフォーマットを定義

ここでは `URL`、`HTTPステータスコード` と `タイトル` を抽出するのでそのためのデータファーマットを定義します

```
$ cat tsmsognScrapy/items.py
# -*- coding: utf-8 -*-

# Define here the models for your scraped items
#
# See documentation in:
# https://doc.scrapy.org/en/latest/topics/items.html

import scrapy


class TsmsognscrapyItem(scrapy.Item):
    # define the fields for your item here like:
    url = scrapy.Field()
    status = scrapy.Field()
    title = scrapy.Field()
```

### Spiderに動作を定義

[http://tsmsogn.github.io/](http://tsmsogn.github.io/) の各ページのリンクを辿って、 各ページの `URL`、`HTTPステータスコード` と `タイトル` をスクレイピングするようにします。

```
$ cat tsmsognScrapy/spiders/tsmsogn.py
# -*- coding: utf-8 -*-
import scrapy
from tsmsognScrapy.items import TsmsognscrapyItem


class TsmsognSpider(scrapy.Spider):
    name = 'tsmsogn'
    allowed_domains = ['tsmsogn.github.io']
    start_urls = ['http://tsmsogn.github.io/']

    def parse(self, response):
        self.logger.info("Scraping: " + response.url)

        item = TsmsognscrapyItem()
        item['url'] = response.url
        item['status'] = response.status
        item['title'] = response.selector.xpath('//title/text()').extract_first()
        yield item

        for href in response.xpath('//a/@href').extract():
            url = response.urljoin(href)
            yield scrapy.Request(url, callback=self.parse)

```

### スクレイピング結果をUTF-8で出力する

デフォルではスクレイピング結果が Unicode だったので、`tsmsognScrapy/settings.py` に `UTF-8` で出力するように変更します。

```
$ echo "FEED_EXPORT_ENCODING='utf-8'" >> tsmsognScrapy/settings.py
```

### 実行

```
$ scrapy crawl tsmsogn -o result.json
```

### ここにおいてあります

[https://github.com/tsmsogn/scrapy_getting_started](https://github.com/tsmsogn/scrapy_getting_started)
