+++
title = "VMもBootCampも使わずにMacでxopsを動かす方法"
date = 2018-06-07T03:59:26+10:00
Description = "Macユーザーのみなさんに朗報です。"
image = "xopsmac.jpg"
tags = ["wine", "osx", "xops"]
categories = ["Japanese", "Development"]
archives = ["2018/06"]

+++
まず結論から言うと、[Wine](https://www.winehq.org/)というソフトを使います。
# Wineとは
>Wine (originally an acronym for "Wine Is Not an Emulator") is a compatibility layer capable of running Windows applications on several POSIX-compliant operating systems, such as Linux, macOS, & BSD. Instead of simulating internal Windows logic like a virtual machine or emulator, Wine translates Windows API calls into POSIX calls on-the-fly, eliminating the performance and memory penalties of other methods and allowing you to cleanly integrate Windows applications into your desktop.

要約すると、

- WineはVMでもエミュレーターでもないよ
- Windows APIコールをPOSIXコールに変換することで、Windowsアプリを動かすために必要最低限のリソースしか使わんよ

ということです。よくわからないですよね。僕もよくわかりません。

ただ確実に言えるのは、VMのようにWindowsのOSをまるごと動かしたり、BootCampを使っていちいちわざわざWindowsを立ち上げるよりも、
アプリだけ動かせたほうがパソコンへの負荷は低いし簡単ということです。

その上なんと**無料**だし、もう言うことないですね。

# インストール手順
今回は"Wine install"ってググって一番最初に出てきた[こちら](https://www.davidbaumgold.com/tutorials/wine-mac/#part-5:-run-windows-programs-using-wine)のサイトを参考にしました。

## 必要なもの
- homebrew

ない人は以下のコマンドを叩いてインストールしましょう。

```bash
ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"

```

## 手順
### 1. XQuartzをインストール

```bash
brew cask install xquartz

```

### 2. Wineをインストール

```bash
brew install wine

```

### 3. Xopsをダウンロード
[こちら](https://hp.vector.co.jp/authors/VA022962/xops/)から必要なファイルをダウンロードして解凍しましょう。
んで、
```bash
mv Downloads/dirname .wine/drive_c/Program\ Files/dirname
```
しておきます。

### 4. 実行
<!--
```bash
wine path_to_config
wine path_to_exe

```
GUIがほしいよって人は -->
```bash
winefile

```
このコマンドを叩くと一昔前のエクスプローラ的なGUIが出てきます。
C: > Program Files > xops096
と進んでまずはconfig.exeを実行し、Saveしましょう。
そしたら一旦Wineを再起動します。
すると、xops096ディレクトリ内にconfig.datが現れていると思います。
あとはxops096.exeを実行するだけです。

# 問題点

## wineコマンドだと起動しない
こんなエラーが吐かれます。
```bash
0009:fixme:win:EnumDisplayDevicesW ((null),0,0x33fa70,0x00000000), stub!
wine: Unhandled page fault on read access to 0x00000000 at address 0x414b4e (thread 0009), starting debugger...

```

## winefileでconfigを適用するにはいちいち再起動しなければならない？
config4xops05.exeを開いてSAVEしても、config.datは現れません。
一回Wineを終了して改めてwinefileすると、はじめて現れます。

## 音の設定
初期設定だと音が出ない可能性があります。
そんなときは、
```bash
winecfg

```
して、audioタブに行ってスピーカーを設定しましょう。

## Homeキーどうするよ
ほら、FPS視点で武器出したいじゃないすか。
そんなときは、**fn + ←**。

他にもこんなコマンドが使えました(オフライン)：

- fn + F1 視点変更
- fn + F2 画面表示変更
- fn + F5 + Enter 浮遊
- fn + F6 + Enter 装弾数増加
- fn + control + F12 リセット

オンラインでもコマンドの叩き方は基本的に同じ。はず。

# おまけ
https://askubuntu.com/questions/74690/how-to-install-32-bit-wine-on-64-bit-ubuntu

これ、やっとくとなんかいいらしいよ。
