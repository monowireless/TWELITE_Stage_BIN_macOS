---
title: "Windows"
author: "Mono Wireless Inc."
description: TWELITE_Stage インストール (Windows10)
---

# Windows

`Windows` 

### 環境

以下の環境で開発しています。

* Windows10 バージョン 1903
* VisualStudio 2019 \(32bit ビルド\)


### 動作に必要要件

* FTDI 社の FT232 シリーズが動作するようにデバイスドライバのインストールが必要な場合があります。MONOSTICK や TWELITE-R が認識できていない場合は、[https://www.ftdichip.com](https://www.ftdichip.com) より D2XX ドライバを導入してみてください。
* **Visual Studio 2019 の  Visual C++ 頒布可能コード**（ランタイムライブラリ）が必要になる場合があります。アプリケーションの起動時にエラーが出て起動しない場合は、本パッケージで再配布する **TWELITE\_Stage¥INSTALL¥VC\_redist.x86.exe** またはマイクロソフト社のウェブサイトから入手して、インストールしてください。配布バイナリは 32bit です。

