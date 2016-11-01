---
title: pyenvをインストールした時の備忘録
layout: post
date: '2016-11-01 11:21:34'
categories: python
---

YouTube の API を叩きたくてチュートリアルを眺めていると、クライアントの実装が Python でした。使うついでに、折角なので pyenv を使って、Python のバージョンを切り替えられる環境を整えました。その時の備忘録です。

## System

- OS X EI Capitan

## Installation

Homebrew 経由でインストールします。

<pre>
$ brew install pyenv
$ cat ~/.zprofile
export PATH=$HOME/.pyenv/shims:$PATH

if which pyenv > /dev/null; then
    eval "$(pyenv init -)";
fi
$ source ~/.zprofile
</pre>

## Usage

見た感じ rbenv と同じような使い方です。`help` を見れば大体わかります。

インストールできるバージョンを検索

<pre>
$ pyenv install --list
</pre>

バージョン指定して、インストール

<pre>
$ pyenv install 2.7.11
</pre>

使用するバージョンを指定

<pre>
$ pyenv versions
* system (set by /Users/foo/.pyenv/version)
  2.7.11
$ pyenv local 2.7.11
$ pyenv versions    
  system
* 2.7.11 (set by /Users/foo/.python-version)
</pre>

pip（Python のパッケージマネージャ）を使って、`google-api-python-client` をインストール

<pre>
$ pip install --upgrade google-api-python-client
pyenv: pip: command not found

The `pip' command exists in these Python versions:
$ pyenv shell 2.7.11
$ pip install --upgrade google-api-python-client
</pre>

## Reference Sites

- [https://developers.google.com/api-client-library/python/start/installation](https://developers.google.com/api-client-library/python/start/installation)
- [https://github.com/yyuu/pyenv/issues/411](https://github.com/yyuu/pyenv/issues/411)