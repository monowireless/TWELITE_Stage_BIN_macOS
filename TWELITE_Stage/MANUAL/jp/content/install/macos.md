---
title: "macOS"
author: "Mono Wireless Inc."
description: TWELITE_Stage インストール (macOS)
---

# macOS

`macOS`  

### 環境

以下の環境で開発しています。

* macOS 10.14 (Mojave, Intel)
* macOS 12.4 (Monterey, Apple Silicon)

### 追加的なインストールや警告ダイアログについて

* ダウンロードアーカイブには署名しておりません。実行時には、インターネットからダウンロードされたアプリケーションとしてセキュリティ警告が出る場合があります。
* TWELITE\_Stage をインストールしたパスからの実行許可を要求される場合があります。
* ビルド実行時に make ユーティリティのインストールダイアログが出る場合があります。
* ツールチェインにはコード署名がなされていますが、コード署名が正しく認証されない場合は、ビルドツールチェイン \(ba-elf-gcc など\) の実行形式一つずつについて、動作許可を求められる場合があります。

上記は TWELITE\_Stage の動作のためには許可を与えたり、インストール作業が必要になります。

#### 参考: make ユーティリティの手動インストール

※ OSバージョンの違いなどにより、別の手順で行う必要がある場合があります。

コマンドドライン \(bash\) にて、make を実行した時エラーが出る場合は XCode のインストールを行います。

```bash
$ xcode-select --install
```

インストール完了後、make を入力して以下のメッセージが出れば OK です。

```bash
$ make
make: *** No targets specified and no makefile found.  Stop.
```



### シリアルポートの取り扱いについて

MONOSTICKやTWELITE-R には FTDI社 \(https://www.ftdichip.com\) の FT232 シリーズの半導体が使用されています。利用するためにはデバイスドライバについて対処が必要になる場合があります。

TWELITE\_Stageを起動しても、シリアルポートが表示されない場合は、FTDI社のドライバをアンロード（無効に）する必要があります。以下の「参考」を参照ください。


#### 参考：FTDI社のユーティリティ

{% hint style="danger" %}
このユーティリティは当社のMONOSTICKやTWELITE-Rが挿入された時に、OS標準のデバイスドライバのロードを抑制するものですが、当社以外のデバイスに\(同じUSBのIDを持つもの\)対しても抑制します。
{% endhint %}

[https://www.ftdichip.com/Drivers/D2XX.htm](https://www.ftdichip.com/Drivers/D2XX.htm) より D2xxHelper をダウンロードして使用してください。当アーカイブ TWELITE\_Stage/INSTALL フォルダにも同じものを収録しています。



#### 参考：FTDI社デバイスドライバの手動アンロード

FTDI 関連のドライバをアンロードします。

```bash
$ sudo kextunload -b com.apple.driver.AppleUSBFTDI
```



