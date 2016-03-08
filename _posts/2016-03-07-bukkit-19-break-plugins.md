---
layout: post
title: "Bukkit 1.9で使えなくなるAPI達"
description: "Bukkitが1.9になって使えなくなってしまうAPIを紹介します。使ってるプラグインも死にます。"
category: bukkit
tags: [bukkit, java, spigot]
---
{% include JB/setup %}

[Bukkit 1.9がリリース](https://www.spigotmc.org/threads/127186/)されてから少し経ちました。
今まで自分が確認出来た、使えなくなってしまうプラグインやAPIを説明します。

## Deprecatedになっていた２つのAPI

`Painting`のイベント(`Hanging`に移行)と、`ContainerBlock`(`InventoryHolder`に移行)が削除されました。
どちらも2012年には非推奨になっているのでそれほど大きな問題にはなっていないと思います。

## 強制的にUTF-8に

今までは環境に依存したCharsetが使われていましたが、1.9になってやっとUTF-8のみに統一されました。
英語圏の人だと、それほどマルチバイト文字を使う機会は多くないので問題無いかもしれませんが、
日本人としては、configにある日本語全てがマルチバイト文字文字であり、
Windows環境(Shift_JIS環境)を使っている人は対応する必要があります。

今まで、デフォルトのconfigを環境に依存したCharsetで保存するようになっていたプラグインも修正が必要です。

<blockquote class="twitter-tweet" data-lang="ja"><p lang="ja" dir="ltr">一応コメントをいれておくと、Bukkit 1.9 でファイルの読み書きが全環境UTF-8で統一されたので、WindowsだとShift-JISでconfig.yml を書くようなギミックを入れているプラグインは動作しなくなる可能性がある。</p>&mdash; うっちぃ (@ucchy99) <a href="https://twitter.com/ucchy99/status/706815048505667584">2016年3月7日</a></blockquote>
<blockquote class="twitter-tweet" data-lang="ja"><p lang="ja" dir="ltr">うちのプラグインは、WindowsだとShift-JISで読み書き、Mac・LinuxだとUTF-8で読み書きするような仕組みなので、Windowsで動作させると全滅するのです。<br>ここ、しゃむちゃんのプラグインのソース読んでパクってるところだったなぁ、そういえば。</p>&mdash; うっちぃ (@ucchy99) <a href="https://twitter.com/ucchy99/status/706816174927908864">2016年3月7日</a></blockquote>

## Soundが大幅変更

[SoundのEnumが書き直されました。](https://hub.spigotmc.org/stash/projects/SPIGOT/repos/bukkit/commits/7898a2a2d2d81308e73e9ed37725f53d7ad37bfc#src/main/java/org/bukkit/Sound.java)
その為、`Sound`を使っていた全てのプラグインが正常に動かなくなります。
`SpecialSource`等を使うことで、配布プラグインを更新することが出来るはずですが、
1.8以前のEnumの名前と1.9移行のEnumの名前を対応させるようなデータが必要なので少し面倒です。

<blockquote class="twitter-tweet" data-lang="ja"><p lang="ja" dir="ltr">HeadDictionary、クリック時にサウンド鳴らす処理なんてしてるから、1.9でエラー吐いている</p>&mdash; misterT (@misterT2525) <a href="https://twitter.com/misterT2525/status/707047823670247425">2016年3月8日</a></blockquote>
<blockquote class="twitter-tweet" data-lang="ja"><p lang="ja" dir="ltr">そういえば、1.8と1.9だとSoundのEnum変わったもんな...これ結構なプラグイン死んでるんじゃないか？</p>&mdash; misterT (@misterT2525) <a href="https://twitter.com/misterT2525/status/707048038028546049">2016年3月8日</a></blockquote>
<blockquote class="twitter-tweet" data-lang="ja"><p lang="ja" dir="ltr">これ見た時は最初「？？」ってなったよ... <a href="https://t.co/vvqMUBTlBE">pic.twitter.com/vvqMUBTlBE</a></p>&mdash; misterT (@misterT2525) <a href="https://twitter.com/misterT2525/status/707058130341892096">2016年3月8日</a></blockquote>

## Biomeの一部が変更

Soundと同じように[BiomeのEnumの一部が変更されていました。](https://hub.spigotmc.org/stash/projects/SPIGOT/repos/bukkit/commits/7898a2a2d2d81308e73e9ed37725f53d7ad37bfc#src/main/java/org/bukkit/block/Biome.java)

## 1.7より古い一部のメソッド

1.6以前の`getOnlinePlayers()`など、返り値が変わったりした一部のメソッドを使ったプラグインが動かなくなりました。
プラグインに対して手動で[マッピング](https://hub.spigotmc.org/stash/projects/SPIGOT/repos/craftbukkit/browse/deprecation-mappings.csrg)を適応することで、
ソースコードにアクセス出来ない(更新出来ない)プラグインも対応させることが出来ます。

## 最後に

間違っている点や、ここに載っていない点などを見つけた場合は、[私のTwitter@misterT2525](https://twitter.com/misterT2525)に報告してくれると助かります。

<script async src="//platform.twitter.com/widgets.js" charset="utf-8"></script>
