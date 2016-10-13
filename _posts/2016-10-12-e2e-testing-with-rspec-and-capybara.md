---
title: RSpec + Capybaraを使って外部サイトのE2Eテストを行うテンプレートを作った
layout: post
date: '2016-10-12 10:42:28'
categories: ruby
---

## TL;DR

- [poltergeist](https://github.com/teampoltergeist/poltergeist) を使って PhantomJS が扱える
- それによって、外部サイトのテストや JavaScript のテストができる
- テストの雛形を作りました -> [https://github.com/tsmsogn/e2e-testing-with-rspec-and-capybara](https://github.com/tsmsogn/e2e-testing-with-rspec-and-capybara)

## やったこと

`bundle` や `rspec` コマンドの使い方をいつも忘れるのでメモしておきます。

### bundle使ってgem管理

<pre>
$ mkdir foo && cd foo
$ bundle init
$ cat Gemfile
# A sample Gemfile
source "https://rubygems.org"

# gem "rails"
group :development, :test do
  gem 'rspec'
  gem 'capybara'
  gem 'capybara-webkit'
  gem "poltergeist"
end
$ bundle install
</pre>

テストすることが目的のプロジェクトなのに、`development` と `test` の時だけ RSpec などの gem をインストールするのは変な気がしますが、とりあえずこのままで。

### テスト作成

<pre>
$ rspec --init
$ cat spec/test_spec.rb 
require 'spec_helper'
require 'capybara/rspec'
require 'capybara/poltergeist'

Capybara.javascript_driver = :poltergeist
Capybara.register_driver :poltergeist do |app|
  Capybara::Poltergeist::Driver.new(app, js_errors: true, timeout: 30)
end

Capybara.configure do |config|
  config.run_server = false
  config.default_driver = :poltergeist
  config.app_host = 'http://tsmsogn.github.io'
end

describe '/', type: :feature do
  subject { page }
  before { visit('/') }

  it 'Title' do
    expect(page).to have_title 'u.find.any?'
  end
end
$ bundle exec rspec
.

Finished in 5.31 seconds (files took 1.9 seconds to load)
1 example, 0 failures

</pre>

いいみたいです。

### rakeでテストが走るように

Travis CI ではデフォルトで `rake` が実行されるので、その際にテストが走るように Rakefile を書きます。

<pre>
$ cat Rakefile 
require 'rspec/core/rake_task'

RSpec::Core::RakeTask.new(:spec)

task :default => :spec
$ rake
.

Finished in 4.6 seconds (files took 1.27 seconds to load)
1 example, 0 failures

</pre>

おｋみたいです。

## Todo

- Ruby >= 2.0.0, < 2.2.2 対応