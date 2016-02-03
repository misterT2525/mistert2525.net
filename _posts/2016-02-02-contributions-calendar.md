---
layout: post
title: "Contributions Calendarを作った"
description: "指定されたgitリポジトリからContributions Calendarを生成するプログラムを作った"
category:
tags: [java, maven, git, github, gitlab]
---
{% include JB/setup %}

最近は、Privateな開発するときには無料でPrivateリポジトリが使い放題な[GitLab.com](https://gitlab.com/)を使っています。
ですが、GitLabのContributions Calendarはコミット単位ではなくpush単位だったりと、
いくつか不満があったので[GitHubのContributions Calendar](https://help.github.com/articles/viewing-contributions-on-your-profile-page/#contributions-calendar)に出来るだけ近いものを使いたかったので、
自分でGitHubを参考にして生成するプログラムを作りました。

<blockquote class="twitter-tweet" data-lang="ja"><p lang="ja" dir="ltr">1コマンドでこれを生成して公開出来るようになった <a href="https://t.co/lttwnAnCaG">pic.twitter.com/lttwnAnCaG</a></p>&mdash; misterT (@misterT2525) <a href="https://twitter.com/misterT2525/status/694219764567142401">2016, 2月 1</a></blockquote>
<script async src="//platform.twitter.com/widgets.js" charset="utf-8"></script>

ちなみに、プログラム、生成されたページ共に知り合いに見せる程度で、あまり大きく公開はしない予定です

## 仕様

* `repos` ディレクトリに、追跡したいリポジトリをclone&fetchしておく
* `mvn` コマンドを実行すると `exec:java` を利用してプログラムが実行され、htmlファイルがフォルダ内に書き出される
  * コミッターのタイムゾーン情報を元に生成している
  * テンプレートファイルを元に生成
  * カレンダー部分のsvgは、ほぼGitHubと同じ仕様
* [Bootstrap](http://getbootstrap.com/)をベースにデザイン
* GitHubのデザインに似せながら、cssをちょっと書き書き
* Bootstrapのtooltipを利用して、カーソルを当てるとコントリビューション数が表示されるように

## 気をつけたところ

### 出来るだけGitHubに似せる

もともと、GitHubのContributions CalendarのデザインでGitLabとかのリポジトリとかを見たいって事で作ったので

## 生成されるソースコードを綺麗に

テンプレートエンジンなどを使った場合に、生成されたソースコードのインデントが崩れてたりすることがあるので、出来るだけそういうことが無いようにしたいなと思って作りました
(そのせいで生成するソースコードが汚くなってしまい、かなりつらい)

## gistとbl.ocks.orgを使ってページを公開

生成されるファイルは、JavaScriptもCSSも埋め込まれた一つのhtmlファイルなので、[GitHub Gist](https://gist.github.com)と[bl.ocks.org](http://bl.ocks.org)という２つのサービスを利用して公開することにしました。
gistに `index.html` と言う名前でアップロードし、bl.ocks.orgで表示するだけなので、とても簡単に公開することが出来ました。
更新時はgistをcloneリポジトリに `index.html` を移動し、コミットしてpushすればすぐにbl.ocks.orgにも反映されるので、とても便利です。

## 最後に

これを作ったおかげでなんだかモチベーションが上がった気がする。
(適当な記事でごめんなさい)
