---
title: "標準アプリ ビューア"
author: "Mono Wireless Inc."
description: "標準アプリ ビューア"
---
# 標準アプリ ビューア

`Windows` `macOS` `Linux` `RasPi`

[App\_Twelite(標準アプリ)](https://mono-wireless.com/jp/products/TWE-APPS/App\_Twelite/)の[0x81コマンド](https://mono-wireless.com/jp/products/TWE-APPS/App\_Twelite/step3-81.html)を解釈します。

![](../../../../.gitbook/assets/img_viewer_std.png)

TWELITE無線マイコンにはApp\_Twelite(標準アプリ)またはApp\_Wingsを書き込んでおき、通信相手からのシリアルメッセージが表示されていることを確認してから使用します。

通信相手はApp\_Twelite(標準アプリ)で、標準アプリのボタンやアナログ入力の状態のメッセージ (0x81メッセージ) を受信すると、その内容を mwm5 のパーサーライブラリにより解釈して表示します。

| 操作         |                                     |
| ---------- | ----------------------------------- |
| \[ A ]     | 割当なし                                |
| \[ A ] 長押し | この画面を抜け、前メニューに戻る                    |
| \[ B ]     | フォントを変更します。                         |
| \[ B ] 長押し | テスト用のダミーデータによる画面表示を行います。            |
| \[ C ]     | 割当なし                                |
| \[ C ] 長押し | TWELITE 無線モジュールのリセットピンを制御し、リセットします。 |
| ESC        | ESCキーを入力することで、この画面を抜けます。            |
