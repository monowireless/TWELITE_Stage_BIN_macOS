---
title: "ログ機能"
author: "Mono Wireless Inc."
description: "ログ機能"
---
# ログ機能

`Windows` `macOS` `Linux` `RasPi` 

TWELITE 無線マイコンとのシリアル通信のログを記録することができます。

### ログの開始 

`Windows` `macOS` `Linux` `RasPi`

TWELITE 無線マイコンとのシリアル通信のログを記録することができます。

Alt(Cmd)+Lキーを押します。

![](<../.gitbook/assets/../.gitbook/assets/img_help_ovrly.png>)



### ログ記録の終了

ログ記録中にもう一度 Alt(Cmd) + L キーを押します。

![](<../.gitbook/assets/img_logging_fin.png>)

ログの記録が終了し、その時のログファイルがOS標準の方法(Windowsならメモ帳、macOS ならコンソール)で開かれます。

※ RaspberryPi ではログファイルの保存のみで開く機能はありません。



### ログの記録

TWELITE 無線マイコンから受信した文字列→そのまま記録されます

TWELITE 無線マイコンに送信した文字列→１文字ずつWindowsの場合は `｢ ｣`, macOS/Linux/RaspBerryPiは `« »` で囲って記録します。

例えば`«t»`とある場合はキーボードから`t`を入力したことを意味します。


### ログ記録のフォルダとファイル名

`Windows` `macOS` `Linux` `RasPi`

`{TWELITE STAGE APP の実行形式のあるフォルダ}/log` にログ開始時の日時を元にしたファイル名で保存されます。

`Alt(Cmd)`+`Shift`+`L` を押すことで、そのフォルダを開きます。

![](<../.gitbook/assets/img_logging_folder.png>)



