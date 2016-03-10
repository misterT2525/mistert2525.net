---
layout: post
title: "BungeeCordとは何か"
description: "BungeeCordとは何か、出来るだけ詳細に、簡単に説明する"
category:
tags: [java, minecraft, bungeecord]
---
{% include JB/setup %}

<div class="alert alert-danger" role="alert">
  <strong>注意事項</strong>
  この記事の内容を、筆者は保証しません。
  この記事は、出来るだけ簡単にそして詳細にBungeeCordとは何なのかを説明するために書かれました。
  使い方などを紹介するものではありません。
</div>

[BungeeCord][bungeecord]とは、[SpigotMC][spigotmc]による[Minecraft][minecraft]用のプロキシサーバーである。
BungeeCordは、指定された **実際のサーバー** (ここではSpigotやCraftBukkit等のサーバーを指す)とプレイヤーの間に設置され、
プレイヤーを切断させること無く別の実際のサーバーに移動させたりすることが出来る。

## 何をしてくれるか

### プレイヤーの認証

BungeeCordは、プレイヤーが実際にMinecraftを購入している正規のユーザーか確認してくれる(online-modeの場合)  
なので、実際のサーバーはoffline-mode(後述)でも、**online-modeのBungeeCordを経由していれば**、
非正規のユーザーが入ってくることはない。

### サーバー間移動

BungeeCordを使う大きな理由として、
プレイヤーが切断して別のサーバーにログインするという作業をしなくても、
別のサーバーに移動させることが出来る。
しかしこれは、接続先のサーバーがそのBungeeCordから接続されることを想定して設定している場合に限り、
関係ない他人のサーバーに繋げることが出来るわけではない。
そして、この機能を使い実際のサーバーを分けて、BungeeCord自体も複数に分けることで、
数万人規模のユーザーを同時に接続させているサーバーもある。

BungeeCordが、ユーザーを移動させる時には以下の様なことをしている。
また、ユーザーがBungeeCordにログインしてきた時に、
少し異なるが同じような方法で実際のサーバーに接続している。

1. 接続先のサーバーに、移動させるユーザーとしてログインする。  
   技術的に、online-modeのサーバーにユーザーとしてログインさせることは出来ないので、
   独自のIP Forwardingという技術(後述)を使って、移動させるユーザーの情報を送信している。
2. ログインに成功した場合は、ユーザーに対してワールドを移動したように見せかけて、
   移動先のサーバーの情報を送信する。
   またこの際に、移動元のサーバーの一部の情報(プレイヤーリストやスコアボード等)を、
   削除するように通知する。
3. 移動先のサーバーから送られてきている、ワールドやエンティティなどの様々な情報を、
   プレイヤーに転送する。  
   しかし、移動先のサーバーからはBungeeCordがクライアントだと思っているので、
   一部Entity ID等の問題があるので、それは書き換えて転送する。

## IP Forwarding

BungeeCordを使う場合、実際のサーバーはoffline-modeである必要がある。
offline-modeだとプレイヤーのUUID等はプレイヤーネームから生成されるので、
プレイヤーネームを変更された場合に問題が発生する。
またoffline-modeだとスキン等も反映されず、いろいろな問題がある。
そして、実際のサーバーからは、BungeeCordをクライアントとして処理されるので、
プレイヤーのIPアドレスもBungeeCordのものになり、IP BAN等も使えなくなってしまう。

その問題を解決するために使われるのがIP Forwardingだ。
これは、Spigot等の[IP Forwardingに対応するパッチ][spigot-patch]を適応されているサーバーで、
かつ設定でそれが有効になっている実際のサーバーに対して、
BungeeCordがプレイヤーの情報を送信する仕組みだ。

BungeeCordの`config.yml`内の`ip_forward`を有効にし、
Spigot又はそれのフォークでは、`spigot.yml`内の`bungeecord`を有効にした場合に利用出来る。
forgeやCraftBukkitサーバーとはこの機能は利用出来ないが、
バニラサーバーなら[VanillaCord][vanillacord]を使ってパッチを当てたサーバーなら利用出来る。

IP Forwardingでは、プレイヤーのIPアドレスとUUID、そして存在するならGameProfile(スキン等の情報)を、
BungeeCordから実際のサーバーに送信している。

## online-mode

何度も同じことを言っているがBungeeCordを使う場合、
実際のサーバーはoffline-modeである必要がある。
これをそのままにして、サーバーを運用すると、セキュリティーに問題があるため、対策をする必要がある。
具体的には、BungeeCordを動かしているホスト以外から接続出来ないようにする必要がある。

実際のサーバーとBungeeCordを同じホストで動かすのならば、
`server.properties`内の`server-ip`を`127.0.0.1`にすることで対策出来るだろう。
別のホストで動かすのならば、`iptables`等のファイヤーウォールを使って対策するべきだろう。
詳しくは[SpigotMCのページ][firewall-guide]を見るといいだろう。

対策をしなかったら、何が起きるのか。
簡単に説明すると、悪意のある人が他人に成りすましてログインすることが出来てしまう。

権限を持った運営に成りすましてログインしてきたらどうなるだろうか？
当然サーバーは荒らされたり、負荷を掛けられたり、サーバーを止められるかもしれない。

バックアップを取っておけばそんなの問題にならないし、対策するの面倒だしそのままでいいと思う人が居ないとは限らない。
でも、そんな身勝手なことは許されない。
セキュリティーに対して意識が無い人はサーバーやサービスを運用するべきではない。
もしも、プラグイン等に外部にアクセスするものが含まれていたとしたら、
攻撃者はそれを悪用して貴方のではない第三者のサーバーやサービスを攻撃する可能性だってある。

[spigotmc]: https://www.spigotmc.org/
[bungeecord]: https://www.spigotmc.org/go/bungeecord
[minecraft]: https://minecraft.net/
[spigot-patch]: https://hub.spigotmc.org/stash/projects/SPIGOT/repos/spigot/browse/CraftBukkit-Patches/0048-BungeeCord-Support.patch
[vanillacord]: https://www.spigotmc.org/resources/vanillacord.952/
[firewall-guide]: https://www.spigotmc.org/wiki/firewall-guide/
