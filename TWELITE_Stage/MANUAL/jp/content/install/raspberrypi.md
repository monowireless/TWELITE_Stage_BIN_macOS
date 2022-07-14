---
title: "RaspberryPi"
author: "Mono Wireless Inc."
description: TWELITE_Stage インストール (Raspberry Pi)
---

# RaspberryPi

`RasPi`  

TWELITE Stage アプリは Raspberry Pi で動作します。

* マウスとタッチスクリーンに対応します。
* ビルドツールチェインが付属しコンパイルも可能です。
* 実行形式はフレームバッファ版, X11版、フレームバッファ軽量版, X11軽量版の4種類です。軽量版は半透明エフェクトなどを省略しています。

{% hint style="warning" %}
お使いの RaspberryPi の OS 種別、バージョン、インストール状況によって動作しない場合や、再コンパイル等が必要になる場合があります。
{% endhint %}

## 環境

TWELITE STAGE は以下の環境で開発・動作確認しています。

* Hardware
  * Raspberry Pi 3 Model B
  * LCD Screen: Raspberry Pi Touch Display \(7"\)
* OS & distribution
  * Raspberry PI OS \(32bit\) Lite \(Version:August 2020\)


## 既知の問題・制限事項

* 1回目の起動で `/dev/serial0` の動作が失敗することがある。
* Raspberry Pi 4B では `/dev/serial0` の動作は未検証です。
* Raspberry Pi 4B ではタッチスクリーンの動作は未検証です。
* TWELITE STAGE への入力文字列が`/dev/tty1`上で動作してるシェルやgettyへ入力文字列がそのまま渡されます。`/dev/tty1`から起動することを推奨します。
* 他のインストールや動作のプログラム\(X11など\)に影響を受けることがあります。



## アーカイブの展開

ダウンロードしたアーカイブファイルは、パス名に空白や日本語などが含まれないフォルダに展開します。

以下ではRaspberry Piのホームフォルダに展開してます。

```text
$ cd /home/pi
$ unzip MWSTAGE2020_XX_YYYY.zip
```

### フォルダ構成

```text
../MWSTAGE
     TWELITE_Stage.run    TWELITE_Stage アプリ
     BIN/                 ファームウェアBINファイル
     MWSDK/               MWSDK ライブラリなど
     TWELITE_Stage/       TWELITE_Stage アプリ関連ファイル
```



## デバイスドライバ

TWELITE STAGE から MONOSTICK や TWELITE-R を認識するためには、ftdi\_sioモジュールをアンロードし、また、USBデバイスに対して読み書き権限が必要になります。

{% hint style="info" %}
USBデバイスのIDは以下のようになります。

* ベンダーID 0x0403
* プロダクトID 0x6001\(MONOSTICK,TWELITE R\) または 0x6015 \(TWELITE R2\) 
{% endhint %}

この設定を自動化するための udev の設定スクリプトを用意しています。`/etc/udev/rules.d` に定義をコピーして、設定をリロードしています。設定後は USB デバイスを抜き差ししてから `TWELITE_Stage.run` を実行してください。起動直後の画面で USB デバイスが表示されれば、設定が反映されています。



```text
$ cd ./MWSTAGE/TWELITE_Stage/INSTALL/ubuntu/
$ sudo ./set_udev_sudo.sh
```

定義ファイル（読みやすいように改行しています）

```text
ACTION=="add",
   ATTRS{idVendor}=="0403", ATTRS{idProduct}=="6001",
   MODE="0666",
   RUN+="/bin/sh -c 'rmmod ftdi_sio && rmmod usbserial'"
ACTION=="add",
   ATTRS{idVendor}=="0403", ATTRS{idProduct}=="6015",
   MODE="0666",
   RUN+="/bin/sh -c 'rmmod ftdi_sio && rmmod usbserial'"
```



## UARTについて

上述の環境では、`raspi-config` よりシリアルポートの設定をすることで `/dev/serial0` が利用可能になります。

```text
  $ sudo raspi-config

  メニューより
  "3 Interface Options    Configure connections to peripherals"
  →"P6 Serial Port Enable/disable shell messages on the serial connection"

  以下のようにログインシェルとしては利用しない、ハードウェアを有効化するを選択します。
  "Would you like a login shell to be accessible over serial?" -> <No>
  "Would you like the serial port hardware to be enabled?" → <Yes>
```



### 配線例

```text
 [TWELITE]               [RaspberryPi]
  GND  ------------------ Gound (#6,#9,#14,#20,#25,#30,#34,#39のいずれか)
  TXD(DIO6,DIP#10) ------ GPIO15/UART0 RXD (#10)
  PRG(SPIMISO,DIP#7) ---- GPIO23 (#16)
  RXD(DIO7,DIP#3) ------- GPIO14/UART0 TXD (#8)
  RST(RESETN,DIP#21) ---- GPIO22 (#15)
  VCC  ------------------ 3V3 (#1,#17のいずれか)
  SET(DIO12,DIP#15) ----- GPIO12 (#32)
```

* TWELITE, RaspberryPi ともに製造元のマニュアルを参照ください。
* DIP\# は TWELITE DIP のピン番号です。
* 上記配線は TWELITE 無線マイコンモジュールが安定稼働することを保証するものではありません。





## TWELITE Stage アプリの起動

* X11のデスクトップ上では動作しません。X11を終了しておきます。
* `TWELITE_Stage.run`を実行します。スクリーン画面上のTWELITE Stageアプリが表示されます。

### 留意事項

* マウスとタッチパネルに対応します。
* TWELITE Stage アプリ中で、入力した文字はコンソール画面にも表示される場合があります。





## その他

### /dev/dri

`TWELITE_Stage.run` 起動時に以下のエラーが出る場合があります。

```text
  "The path /dev/dri/ cannot be opened or is not available"
```

無視しても構いません。



### メモリ不足

ビルド時はCPU数が4以上の場合は、CPU数を一つ引いた値の並列コンパイルを実行します\(4コアなら3並列\)。場合によってはメモリ不足が発生するかもしれません。その場合は並列数を変更してください。



### RaspberryPi 4

{% hint style="warning" %}
この情報は十分な検証を行っていません。
{% endhint %}

以下の設定が必要です。OpenGL関連のドライバが有効にする必要があります。

* `raspi-config` の Advanced Settings → A2 GL Driver → G2 GL \(Fake KMS\) を選択する
* `libgles-dev` パッケージを導入しておく
* タッチスクリーンの動作は未検証です

