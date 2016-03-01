---
layout: post
title: "Bukkit1.9変更点まとめ"
description: "Bukkitが1.9になって変わった点に関してまとめています。"
category: bukkit
tags: [bukkit, java, spigot]
---
{% include JB/setup %}

Bukkit 1.9がリリースされました。
1.8からの変更点をまとめていきます。
間違っている箇所など有りましたらツイッターで教えてください。

[Minecraft1.9の変更点](http://minecraft-ja.gamepedia.com/1.9)

## 削除されたAPI

以下のAPIはBukkit1.9で削除されます。
その為、そのAPIを使っていたプラグインはBukkit1.9以降のサーバーでは動作しなくなります。

### [Painting*Event](https://hub.spigotmc.org/stash/projects/SPIGOT/repos/bukkit/commits/41a3f82c17d75416a4d75802188b170e8bf113fb)

2012年10月に、`Hanging*Event`に置き換えられ、非推奨になっていました。

* PaintingBreakByEntityEvent
* PaintingBreakEvent
* PaintingEvent
* PaintingPlaceEvent

### [ContainerBlock](https://hub.spigotmc.org/stash/projects/SPIGOT/repos/bukkit/commits/b2aefa586cd89d2ed985223f54354714a814dc5e)

2012年3月に、`InventoryHolder`に置き換えられ、非推奨になっていました。

## 非推奨になったAPI

以下のAPIはBukkit1.9で非推奨になります。
そのAPIを使っていたプラグインはBukkit1.9のサーバーでも動作しますが、不安定になる可能性があります。
また、将来的に削除される可能性がある為、開発者は代わりになるAPIへの以降をするべきです。

### [Boat](https://hub.spigotmc.org/stash/projects/SPIGOT/repos/bukkit/commits/2360673e9a96f6a7e8d7414c8914b578ed5d1a89)

Minecraft1.9でボートの仕様が変わったため、今までのAPIは非推奨になります。

### [ItemInHand](https://hub.spigotmc.org/stash/projects/SPIGOT/repos/bukkit/commits/b25ddcf477fb80bbe3888571a7a4b926625b13b9)

Minecraft1.9でOffHandが追加されたため、`ItemInHand`は非推奨になります。
Bukkit1.9では、`ItemInHand`は`ItemInMainHand`と同じ動作になりますが、
将来的に削除される可能性がある為、`ItemInMainHand`と`ItemInOffHand`に移行するべきです。

## 変更されたAPI

### [UTF-8](https://hub.spigotmc.org/stash/projects/SPIGOT/repos/bukkit/commits/5b60dc50cf3f47939be988edf358572db6cea6d4)

今までは、環境で設定されたCharsetを使っていたコンフィグファイルなどが、必ずUTF-8を使うように変更されるようです。
確認出来ていませんが、今までShift_JIS環境で動かしていたサーバーで、
コンフィグファイルにマルチバイト文字が含まれている場合にUTF-8に変更しないと文字化け等が発生する可能性があります。
また、今までjarファイル内のコンフィグファイルにマルチバイト文字を含んでいた場合に、
環境で設定されたCharsetに変換してpluginsフォルダに保存するようにしていたプラグインなどにも影響する可能性があります。

### [Tree](https://hub.spigotmc.org/stash/projects/SPIGOT/repos/bukkit/commits/53330e8c39afd318532f477d6e0e07add4ab8ace)

[バグ(SPIGOT-1389)](https://hub.spigotmc.org/jira/browse/SPIGOT-1389)の修正のようです。

## 追加されたAPI

### [MainHand OffHand](https://hub.spigotmc.org/stash/projects/SPIGOT/repos/bukkit/commits/b25ddcf477fb80bbe3888571a7a4b926625b13b9)

Minecraft1.9でOffHandが追加されたため、追加されます。

### [BossBar](https://hub.spigotmc.org/stash/projects/SPIGOT/repos/bukkit/commits/c464ecaa563fe7f768df74420e4ace1be6c054a6)

Minecraft1.9でボスバーの仕様が変更されたため、追加されます。
以下の様にボスバーを作成することが出来るようです。

```
Bukkit.createBossBar("Title", BarColor.PINK, BarStyle.SEGMENTED_12, BarFlag.PLAY_BOSS_MUSIC)
```

### [Glowing](https://hub.spigotmc.org/stash/projects/SPIGOT/repos/bukkit/commits/298c819f609cb68e9b4a8df56209446b3512c771)

Minecraft1.9で`Glowing`というEntityの状態が追加されたため、追加されます。

### [DamageCause.FLY_INTO_WALL](https://hub.spigotmc.org/stash/projects/SPIGOT/repos/bukkit/commits/c633591e52e0ecd4f4d146ebd8231659b4b87479)

### [Merchant](https://hub.spigotmc.org/stash/projects/SPIGOT/repos/bukkit/commits/972b9fea86022c4136504fbd3ac9c00070b96baa)

### [Particle](https://hub.spigotmc.org/stash/projects/SPIGOT/repos/bukkit/commits/cc17cf177617cb57951a405725cba59b5244acec)

### [Attribute](https://hub.spigotmc.org/stash/projects/SPIGOT/repos/bukkit/commits/159053bc7585980583ee76354e1a40448cb45d75)

### [CauldronLevelChangeEvent](https://hub.spigotmc.org/stash/projects/SPIGOT/repos/bukkit/commits/5ffd23921010df307d30533473ef3c7e85fc5ad6)

### [PlayerFishEvent.State.BITE](https://hub.spigotmc.org/stash/projects/SPIGOT/repos/bukkit/commits/e159720a91b50d01410eea84650e9546f93421e4)

### [FurnaceRecipe experience](https://hub.spigotmc.org/stash/projects/SPIGOT/repos/bukkit/commits/ce26a2e06af5a8c0645d93ccd73d893fc2ef3c48)

### [Inventory#getLocation()](https://hub.spigotmc.org/stash/projects/SPIGOT/repos/bukkit/commits/4a2f5900611095e0c35fc838ae62606b23537cce)

### [PotionEffect#getColor()](https://hub.spigotmc.org/stash/projects/SPIGOT/repos/bukkit/commits/2369bd410e3b2f8ccac90838ffb2eff4096746ec)

### [PrepareAnvilEvent](https://hub.spigotmc.org/stash/projects/SPIGOT/repos/bukkit/commits/56ac4a8769e1bed2b86cf28bc9e653740ef01251)
