---
title: Arch Linuxを使ってみた
published: 2022-09-01
description: 'Arch LinuxをメインOSとして使っていた時のメモ'
image: './arch_front.jpg'
tags: [Arch Linux, Linux, System]
category: 'Linux'
draft: false 
---

:::note[更新]
2024年8月12日
:::

Arch LinuxをメインOSとして使うプロジェクトです。

いまは勉強用ノーパソでArch Linux（手動インストール、Wayland、GNOME）を使っていますが、メインPCでは既にWindowsに戻しました。

勉強用ノートPCでは問題なく改変をしており、ぶいちゃも（PCモード）出先でやったりしています。

ここでは、このプロジェクトで発見した細かいことを記録します。

## インストール

### Wifi

Wifiの環境では *archinstall* を使っても予めに [*iwd*](https://wiki.archlinux.jp/index.php/Iwd) を使ってセットアップする必要があります。

詳しくはドキュメントに従ってください。

### archinstall

Arch Linuxをインストールするには手動インストールとarchinstall二つの方法があります。archinstallは便利のかわりにパスワードが平文で記録されると言われています。（未検証）公式Wikiで手動インストールする場合、Wikiだけでなく、ほかのチュートリアルと参照しながらインストールすると問題がある時に解決しやすくなります。ここでは、archinstallでインストールする方法を紹介します。

まず、同封の *archinstall* ではなく、先に *pacman -Syy* 、そして *pacman -S archinstall* をしてください。この *archinstall* のコマンドは同じですが同封のより若干使いやすいです。

設定を調整する時にいくつかの注意事項があります。

#### ドライブ

自作PC以外を使っている場合は、ドライブのすべてをフォーマットしないで、ファームウェアのパテーションを残してください。（将来Windowsに戻る時や中古パソコンとして売る時のため

#### グラボのドライバー

*「Nvidia」* オーペンソースドライバーは性能が若干落ちるため、proprietaryの方がおすすめです。Open Source Kernel Moduleはアルファのため安定性に問題があります。ノートパソコンのグラボに対応していないのでご注意ください。

> Intel + Nvidia を同時に使う場合、ブートローダーのパラメータに[ibt=off](https://wiki.archlinux.jp/index.php/NVIDIA#.E3.82.A4.E3.83.B3.E3.82.B9.E3.83.88.E3.83.BC.E3.83.AB)を追加する必要があります。具体はドキュメントを見てください。

#### サウンドドライバー

Pulseaudio と pipewire 両方とも使えます。もしインストールしたあとに音が出ない場合、追加パケージが必要です。pipewire の場合の一例は *pipewire-alsa* です。

#### ブートローダー

> 未更新

最近 Grub のアップデートでシステムが起動できなくなる報告がありますので、今の時点（2022年9月1日）では *systemd-boot* を使った方が良いでしょう。

### インストールしたあと

日本語を表示、入力するにはフォントとインプットメソッドが必要です、具体的にはドキュメントをご参照ください。

AUR を楽に使うために [*yay*](https://github.com/Jguer/yay) のような AUR ヘルパーを使った方が良いでしょう。

### VRChatを動かす

Steam で Proton Experimental を使うと、動画の再生が不安定なため、[Proton GE](https://github.com/GloriousEggroll/proton-ge-custom) がおすすめします。（ProtonGEでもよく再生ができない場合があるが、全くできないよりはましです）

ほかに、予め *gamemode* というパケージをインストールしてVRChatのパラメータに *gamemoderun %command%* を追加したら（私の環境では） FPS が 10% くらい高くなります。

ALVR を使う場合、Chromium を予めインストールする必要があります。そうしなければ、ALVRが起動時に落ちます。

> ゲーム内のスクショと写真ができないというバグがあるようです。

#### 内蔵グラフィックスのVRAMについて

Linuxでは、Intel iGPUではUnified Memory、AMD iGPUがgttを利用できます。これらの技術によってiGPUがメモリをそのままアクセスでき（上限が異なる）、メモリが十分である限りではiGPUのVRAM不足の心配がほぼないと思います。

### Unityでアバター改変

> テスト環境: Wayland / Gnome

Unityを使う前に *gconf* (AUR)というパケージをインストールしておく必要があります。 *gconf* がない場合、Unity 2022では高い頻度で固まり、オブジェクトの選択が一部できなくなります。Unity 2019はgconfがある場合でも起動できません。

> Unity 2022.3.22f1では、シェーダーが問題なく動作しますが、2019では以下の通りの問題がありました。

liltoon 2.3 - 2.12 カラー選択ツールを使うとUnityが固まります。 \
liltoon 3: シェーダーキーワードの数が超えているためアバターが表示されません(51/32)。 \
Sunao 1.6.1 テクスチャエラーになります。

## 最後に

Unity 2019のごろ、メインPCでは二回くらいArch Linuxをインストールしましたが、改変ができず断念しました。いまはその後購入した勉強用のノートPCにArch Linuxを入れて改変をしたりしています。

もしこのポストが参考になったら幸いです。