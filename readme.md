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

## 変更内容(0.0.2予定)

### [CTRL]と[CAPS]キーの入れ替え

## 変更内容(0.0.1)

### 非商用限定の1chipMSXのMSX2相当BIOSのバグ修正版を組み込み

### MSXの標準日本語キーボードの全キーを内蔵キーボードで入力可能なように割当を変更

| OCBook.A | PS/2 | PS/2ScanCode | MSX |
| --- | --- | --- | --- |
| [Graph] | [F6] | 0B | [GRAPH] (6-2)-> [HOME] (8-1) |
| [`~] | [半/全] | 0E | [SELECT] (7-6)-> [￥｜] (1-4) |
| [(R)CTRL] | [Home] | E06C | [HOME] (8-1)-> [＼＿ろ] (2-5) |
| (V) | [PrtScr] | E07C | DisplayMode -> [STOP] (7-4) |
| (T) | [Pause] | E11477 | LedDebug? -> DisplayMode |

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
