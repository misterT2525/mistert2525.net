---
layout: post
title: "Bukkit1.9変更点まとめ"
description: "Bukkitが1.9になって変わった点に関してまとめています。"
category: bukkit
tags: [bukkit, java, spigot]
---
{% include JB/setup %}

BukkitのMinecraft 1.9版の開発がスタートしました。
1.8からの変更点をまとめていきます。
間違っている箇所など有りましたらツイッターで教えてください。

[現在の最新版(1.8.8)との差分](https://hub.spigotmc.org/stash/projects/SPIGOT/repos/bukkit/compare/diff?targetBranch=refs%2Fheads%2Fmaster&sourceBranch=refs%2Fheads%2F1.9&targetRepoId=11) |
[Minecraft1.9の変更点](http://minecraft-ja.gamepedia.com/1.9)

#### [`Painting*Event`の削除](https://hub.spigotmc.org/stash/projects/SPIGOT/repos/bukkit/commits/41a3f82c17d75416a4d75802188b170e8bf113fb)

2012年10月に`Hanging*Event`に置き換えられた後、非推奨になっていた`Painting*Event`が削除されました。
`Painting*Event`を使っていたプラグインは動作しなくなります。

#### [`ContainerBlock`の削除](https://hub.spigotmc.org/stash/projects/SPIGOT/repos/bukkit/commits/b2aefa586cd89d2ed985223f54354714a814dc5e)

2012年3月に`InventoryHolder`に置き換えられた後、非推奨になっていた`ContainerBlock`が削除されました。
`ContainerBlock`を使っていたプラグインは動作しなくなります。

#### [デフォルトで`UTF-8`を使用](https://hub.spigotmc.org/stash/projects/SPIGOT/repos/bukkit/commits/5b60dc50cf3f47939be988edf358572db6cea6d4)

`config.yml`などのコンフィグファイルを、全てUTF-8でロード、セーブするようになったようです。
自分もあまり理解出来ていないのですが、
今までWindows環境ではデフォルトで`Shift_JIS`でロード、セーブされていたコンフィグファイルなどが、
今後は必ず`UTF-8`でロード、セーブされるようになると理解しています。

#### [BoatAPIが非推奨に](https://hub.spigotmc.org/stash/projects/SPIGOT/repos/bukkit/commits/2360673e9a96f6a7e8d7414c8914b578ed5d1a89)

1.9でボードの仕様が大きく変化したため、今までのボートのAPIが非推奨になりました。

#### [MainHandとOffHandのAPI](https://hub.spigotmc.org/stash/projects/SPIGOT/repos/bukkit/commits/b25ddcf477fb80bbe3888571a7a4b926625b13b9)

1.9で、オフハンドが使えるようになったのでAPIが更新されました。
今までの`getItemInHand()`と`setItemInHand(ItemStack)`は非推奨になり、
MainHandとOffHand用に別々のメソッドとして追加されました。
また、`EquipmentSlot`には`OFF_HAND`が追加されました。

#### [ボスバーAPI](https://hub.spigotmc.org/stash/projects/SPIGOT/repos/bukkit/commits/c464ecaa563fe7f768df74420e4ace1be6c054a6)

1.9でボスバーの仕様が変更され、APIが追加されました。
以下の様にボスバーを作成することが出来るようです。

`Bukkit.createBossBar("Title", BarColor.PINK, BarStyle.SEGMENTED_12, BarFlag.PLAY_BOSS_MUSIC)`

#### [EntityにGlowingの状態を追加](https://hub.spigotmc.org/stash/projects/SPIGOT/repos/bukkit/commits/298c819f609cb68e9b4a8df56209446b3512c771)

1.9でGlowingという状態が実装されたため、APIが追加されました。
プレイヤーごとからの見た目を変更は出来ないようです。

#### [ParticleAPI](https://hub.spigotmc.org/stash/projects/SPIGOT/repos/bukkit/commits/cc17cf177617cb57951a405725cba59b5244acec)

パーティクルのAPIが追加されました。

#### [1.9で変わった部分への対応](https://hub.spigotmc.org/stash/projects/SPIGOT/repos/bukkit/commits/adafd12e9495aa4b839ed40930c61fe5fa0c36a0)

エンティティ、アイテム、サウンドなどを1.9用に変更されたようです。

#### [`Inventory#getLocation()`の追加](https://hub.spigotmc.org/stash/projects/SPIGOT/repos/bukkit/commits/4a2f5900611095e0c35fc838ae62606b23537cce)

インベントリがエンティティかブロックのものだった場合にLocationを返すメソッドが追加されました。
仮想インベントリなどLocationが存在しないInventoryの場合は`null`を返します。

#### [`PotionEffect`に色のGetterを追加](https://hub.spigotmc.org/stash/projects/SPIGOT/repos/bukkit/commits/2369bd410e3b2f8ccac90838ffb2eff4096746ec)

#### [`PotionEffectType.values()`に注意書きを追加](https://hub.spigotmc.org/stash/projects/SPIGOT/repos/bukkit/commits/525cb1674b1b26c43bdfd617070d3740fc0703e4)

順番や`null`が含まれる可能性に関する注意書きのようです。

#### [`PlayerFishEvent`に`BITE`状態の追加](https://hub.spigotmc.org/stash/projects/SPIGOT/repos/bukkit/commits/e159720a91b50d01410eea84650e9546f93421e4)

魚が引っ掛かったタイミングの状態のようです。

#### [木のAPIの修正](https://hub.spigotmc.org/stash/projects/SPIGOT/repos/bukkit/commits/29375a116ff7adaaf0f5bf4c9994f7aede75a0fe)

[バグ](https://hub.spigotmc.org/jira/browse/SPIGOT-1389)の修正

#### [かまどに`experience`のAPI](https://hub.spigotmc.org/stash/projects/SPIGOT/repos/bukkit/commits/ce26a2e06af5a8c0645d93ccd73d893fc2ef3c48)

getterとsetterが追加されたようです。
