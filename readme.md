# OneChipBook-12 非公式日本語キーボードMSX2ファームウェア

## 概要

本プロジェクトはOneChipBook-12を日本語キーボードMSX2化する非公式FPGAファームウェアです。
無保障・無サポートのため、不具合があっても元プロジェクトなどへの報告はお控えください。

1chipMSXをベースにしたOCMPLDをさらに一部変更しています。
ビデオ出力など諸機能は十分に検証しておりません。

本FPGAファームウェアと組み込まれたMSX2相当のBIOSは非商用利用のみ再配布と利用が許されており、
権利者の許可なく販売はできません。
権利管理団体は1chipMSX販売時のMSXアソシエーションから、
MSXライセンシングコーポレーションに変更されております。

組み込み済みのBIOSはMSX2ですが、再現するハードウェアはMSX2+相当です。
レイドック2など一部のMSX2+用ソフトはそのまま動作するものと思われます。
OCMPLDにはSDカードからBIOSを読み込む仕組みがあるため、
SDカードにSDBIOSイメージを置くことでMSX2+化が可能です。

### 0.0.xR 日本語キーマップ

| OCBook.A  | PS/2       | PS/2ScanCode | MSX (0.0.xR)                  |
| --------- | ---------- | ------------ | ----------------------------- |
| (V)       | [PrtScr]   | E07C         | DisplayMode -> [STOP] (7-4)   |
| (T)       | [Pause]    | E11477       | LedDebug? -> DisplayMode      |
| [GRAPH]   | [F6]       | 0B           | [GRAPH] (6-2)-> [HOME] (8-1)  |
| [(R)CTRL] | [Home]     | E06C         | [HOME] (8-1)-> [＼＿ろ] (2-5) |
| [(L)CTRL] | [Ctrl]     | 14           | [CTRL] (6-1)-> [CAPS] (6-3)   |
| [CAPS]    | [CapsLock] | 58           | [CAPS] (6-3)-> [CTRL] (6-1)   |
| [`~]      | [半/全]    | 0E           | [SELECT] (7-6)-> [1!] (0-1)   |
| [1!]      | [1!]       | 16           | [1!] (0-1)-> [2"] (0-2)       |
| [2@]      | [2"]       | 1E           | [2"] (0-2)-> [3#] (0-3)       |
| [3#]      | [3#]       | 26           | [3#] (0-3)-> [4$] (0-4)       |
| [4$]      | [4$]       | 25           | [4$] (0-4)-> [5%] (0-5)       |
| [5%]      | [5%]       | 2E           | [5%] (0-5)-> [6&] (0-6)       |
| [6^]      | [6&]       | 36           | [6&] (0-6)-> [7'] (0-7)       |
| [7&]      | [7']       | 3D           | [7'] (0-7)-> [8(] (1-0)       |
| [8*]      | [8(]       | 3E           | [8(] (1-0)-> [9)] (1-1)       |
| [9(]      | [9)]       | 46           | [9)] (1-1)-> [0]  (0-0)       |
| [0)]      | [0]        | 45           | [0]  (0-0)-> [-=] (1-2)       |
| [-_]      | [-=]       | 4E           | [-=] (1-2)-> [^~] (1-3)       |
| [=+]      | [^~]       | 55           | [^~] (1-3)-> [￥｜] (1-4)     |

右[CTRL]は[FN]+[F3]のメニューで[HOME]に設定する前提

### 0.0.x 日本語キーマップ

| OCBook.A  | PS/2     | PS/2ScanCode | MSX (0.0.x)                   |
| --------- | -------- | ------------ | ----------------------------- |
| (V)       | [PrtScr] | E07C         | DisplayMode -> [STOP] (7-4)   |
| (T)       | [Pause]  | E11477       | LedDebug? -> DisplayMode      |
| [Graph]   | [F6]     | 0B           | [GRAPH] (6-2)-> [HOME] (8-1)  |
| [(R)CTRL] | [Home]   | E06C         | [HOME] (8-1)-> [＼＿ろ] (2-5) |
| [`~]      | [半/全]  | 0E           | [SELECT] (7-6)-> [￥｜] (1-4) |

右[CTRL]は[FN]+[F3]のメニューで[HOME]に設定する前提

### DIP-SW

| DIP-SW | 機能 | 説明 |
| ------ | ---- | ---- |
| 5 | カートリッジスロット2 | OFF:OneChipBook内部拡張スロット ON:ESE-MegaSCC |
| 6 | 日本語キーマップ | OFF:OneChipBook内蔵キーボード日本語版 ON:標準(外部キーボード用) |

FPGA側でキー割り当てを変更しているため外部PS/2キーボードを接続した場合も同様に割当が変更されてしまいます。
([Home]が[＼＿ろ]になってしまうなど)
外部キーボード接続時は DIP-SW 6 をONにして標準キーマップに戻しこの問題を回避します。

DIP-SW 5をONにした場合は OneChipBook内部拡張スロットが切り離されます。
ASCIIマッパーに変更したい場合は起動後にI/Oポートで切り替えます。


## 変更内容(0.0.2/0.0.2R)

### DIP-SW6でキーマップ切替

## 変更内容(0.0.1R)

### 左[CTRL]と[CAPS]キーの入れ替え

### 数字段のキーを回転


FPGA側でキー割り当てを変更しているため外部PS/2キーボードを接続した場合も同様に割当が変更されてしまいます。
([1]が[2]になってしまうなど)

## 変更内容(0.0.1)

### 非商用限定の1chipMSXのMSX2相当BIOSのバグ修正版を組み込み

### MSXの標準日本語キーボードの全キーを内蔵キーボードで入力可能なように割当を変更

右[CTRL]は[FN]+[F3]のメニューで[HOME]に設定する前提

FPGA側でキー割り当てを変更しているため外部PS/2キーボードを接続した場合も同様に割当が変更されてしまいます。
([Home]が[＼＿ろ]になってしまうなど)

### Led関係はZemmixNeo版相当、RGB出力は1chipMSX版相当に調整

## デバイスへの書き込み

Cyclone Iデバイスの開発には、
有料のQuartus II v13.0sp1 subscription editionか、
すでに正式にはダウンロードできない、
Quartus II v11.0sp1 web edition 以前が必要です。

コンパイル済みのコンフィグレーションデータをフラッシュメモリEPCS4に書き込むだけであれば、
最新バージョンのQuartus Prime LiteのProgrammer単体が適しています。

1. PCに最新バージョンのQuartus Prime LiteもしくはProgrammerをインストールする
2. PCのUSB端子にOneChipBook付属のUSB Blaster海賊品もしくは相当品を接続する
3. Programmerを起動する
4. 「Hardware Setup」ボタンをクリック
5. USB Blaster等が正常に認識されていれば「Avaiable hardware items」リストに表示される
6. 認識したUSB Blaster等をリストをダブルクリックするなりドロップダウンリストから選択するなりする
7. 「Close」ボタンで「Hardware Setup」画面を閉じる
8. ModeドロップダウンからActive Serial Programmingを選択する
9. file>openメニューで書き込みたい[pofファイル](https://github.com/uniabis/onechipbook_ocmpld_jp/releases)等を選択する
10. 「Program/Configure」列と「Verify」列の一番上の行をそれぞれチェックすると下も自動でチェックされる
11. OneChipBook前面の四角い10ピン端子にUSBブラスターのフラットケーブルを接続する
12. OneChipBookの電源を入れる
13. Programmerの「Start」ボタンをクリックする
14. Progress が「Erase」->「Program」->「Verify」と3回進行し成功すれば「100%(Successful)」となる
15. 安全のためOneChipBookの電源を切る
16. OneChipBook前面の四角い10ピン端子からUSBブラスターのフラットケーブルを取り外す

## ライセンス等

### OCMPLD

[history.msxplusplus.txt](https://raw.githubusercontent.com/uniabis/onechipbook_ocmpld_jp/refs/heads/master/history.msxplusplus.txt)(history.txtから改名)参照

### 1chipMSX

 emsx_top.hex
   ESE MSX-SYSTEM3 / MSX clone on a Cyclone FPGA (ALTERA)
   Revision 1.00

 Copyright (c) 2006 Kazuhiro Tsujikawa (ESE Artists' factory)
 Copyright (c) 2006 D4 Enterprise,Inc.
 Copyright (c) 2006 MSX association
 All rights reserved.

 Redistribution and use of this source code or any derivative works, are 
 permitted provided that the following conditions are met:

1. Redistributions of source code must retain the above copyright notice, 
   this list of conditions and the following disclaimer.

2. Redistributions in binary form must reproduce the above copyright 
   notice, this list of conditions and the following disclaimer in the 
   documentation and/or other materials provided with the distribution.

3. Redistributions may not be sold, nor may they be used in a commercial 
   product or activity without specific prior written permission.
   
   THIS SOFTWARE IS PROVIDED BY THE COPYRIGHT HOLDERS AND CONTRIBUTORS 
   "AS IS" AND ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED 
   TO, THE IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR 
   PURPOSE ARE DISCLAIMED. IN NO EVENT SHALL THE COPYRIGHT OWNER OR 
   CONTRIBUTORS BE LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL, 
   EXEMPLARY, OR CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT LIMITED TO, 
   PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES; LOSS OF USE, DATA, OR PROFITS;
   OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND ON ANY THEORY OF LIABILITY, 
   WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT (INCLUDING NEGLIGENCE OR 
   OTHERWISE) ARISING IN ANY WAY OUT OF THE USE OF THIS SOFTWARE, EVEN IF 
   ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.
