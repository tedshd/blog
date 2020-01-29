---
layout: post
title: 'Maker - GH60 RevCHN'
date: 2015-05-02
comments: true
categories: [keyboard, maker]
---
## Maker - GH60 RevCHN

![2015-01-23 00.20.57.jpg](http://user-image.logdown.io/user/3170/blog/3202/post/262828/D9JyzdoQberA9w8jKbMc_2015-01-23%2000.20.57.jpg)

拿了這板子有段時間了

一開始有試著用 Windows 刷 layout 進去, 但一直失敗(應該跟 Windows 不合吧

但直到前一陣子有人分享用 Mac 刷, 這真是太好了, 終於可以開工了

經過漫長的收集材料加焊接(詳情請見 [GH-60 刷刷刷~開發月誌?](http://tysh310246.blogspot.tw/2015/05/gh-60.html))

廢話不多說

### Install crosspack & dfu-programmer

利用 homebrew 安裝

```shell
brew install Caskroom/cask/crosspack-avr
```

```shell
brew install dfu-programmer
```

### git clone Firmware

[tmk_keyboard_custom](https://github.com/kairyu/tmk_keyboard_custom)

```shell
git clone https://github.com/kairyu/tmk_keyboard_custom.git
```

### Modify Config

進到拉下來的 `tmk_keyboard_custom` 目錄, 再進到 gh60 的目錄

```shell
cd keyboard/gh60
```

```shell
vim config.h
```

找到 `#define CONFIG_H`

在底下加上 `#define GH60_REV_CHN`

```shell
vim Makefile
```

註解或刪掉下面的

```shell
KEYMAP_IN_EEPROM_ENABLE = yes # Read keymap from eeprom
```

### Check Device

接上 gh60

```shell
system_profiler SPUSBDataType
```

會顯示

```shell
...
GH60:

          Product ID: 0x6060
          Vendor ID: 0xfeed
          Version: 0.01
          Speed: Up to 12 Mb/sec
          Manufacturer: geekhack
          Location ID: 0x14100000 / 14
          Current Available (mA): 500
          Current Required (mA): 100
...

```

然後按一下背面的按鈕後, 在下一次 `system_profiler SPUSBDataType`

會抓到

```shell
...
ATm32U4DFU:

          Product ID: 0x2ff4
          Vendor ID: 0x03eb  (Atmel Corporation)
          Version: 0.00
          Serial Number: 1.0.0
          Speed: Up to 12 Mb/sec
          Manufacturer: ATMEL
          Location ID: 0x14100000 / 15
          Current Available (mA): 500
          Current Required (mA): Unknown (Device has not been configured)
...
```

要是這個狀態才能刷分位進去

### Update Firmware

先刷 poker layout 試試

```shell
make dfu
```

開始刷到下列訊息出現代表成功

```shell
...
Creating load file for Flash: gh60_lufa.hex
avr-objcopy -O ihex -R .eeprom -R .fuse -R .lock -R .signature gh60_lufa.elf gh60_lufa.hex
dfu-programmer atmega32u4 erase --force
Erasing flash...  Success
Checking memory from 0x0 to 0x6FFF...  Empty.
dfu-programmer atmega32u4 erase
Checking memory from 0x0 to 0x6FFF...  Empty.
Chip already blank, to force erase use --force.
dfu-programmer atmega32u4 flash gh60_lufa.hex
Checking memory from 0x0 to 0x6A7F...  Empty.
0%                            100%  Programming 0x6A80 bytes...
[>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>]  Success
0%                            100%  Reading 0x7000 bytes...
[>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>]  Success
Validating...  Success
0x6A80 bytes written into 0x7000 bytes memory (95.09%).
dfu-programmer atmega32u4 reset
```

如果出現

```shell
avr-gcc: command not found
```

代表 AVR 的環境變數沒加進去

開 `.zshrc` 或 `.bashrc`

加入

```shell
#AVR
PATH="/usr/local/CrossPack-AVR/bin:$PATH"
```

再重啟 terminal 後重刷

測試鍵盤 layout 輸入 [keyboard test page](http://tedshd.github.io/keyboard_test_page/)

### Custom Layout

需要兩個 tool

[keyboard-layout-editor (KLE)](http://www.keyboard-layout-editor.com)

[TMK Keymap Generator (TKG)](http://www.enjoyclick.org/tkg/)

layout editor 產生 keymap raw data 再丟到 keymap generator 產生 .c

以下為我設計的 layout


* [Default](http://www.keyboard-layout-editor.com/#/layouts/f5090521ca5239e85d1f2663c18fd9b5)

* [Function layer](http://www.keyboard-layout-editor.com/#/layouts/cdb94b80ee1a27a733b98b06aeda4c94)

Function layer 是 fn 組合鍵用的

keymap generator 的設定

* Keyboard - GH60 (RevCHN)
* Layer Mode - Normal
* Number of Layers - 2
* Layer0 - Default
* Layer1 - Function layer
* Fn - Layer action > Momentary layer 1

這裡要注意 layer 的層級 [PTT - GH60 上手第一回](https://www.ptt.cc/bbs/Key_Mou_Pad/M.1390542876.A.073.html)

Fn `Momentary` layer 1 的意思就是當 fn 按下時是 layer 1 的 keymap, 但不按 fn 時就關掉 layer1

這試了好久...

下載 .c 檔後, 把名字改成 **`keymap_tkg.c`**

丟到 gh60 目錄後執行

```shell
make KEYMAP=tkg dfu
```

就 ok 了

Finish

![2015-05-02 18.45.33.jpg](http://user-image.logdown.io/user/3170/blog/3202/post/262828/CpjyWNMTjWocrq5fRfsV_2015-05-02%2018.45.33.jpg)

![2015-05-02 18.45.54.jpg](http://user-image.logdown.io/user/3170/blog/3202/post/262828/dyInnZqtQPW7Xyhj1hjp_2015-05-02%2018.45.54.jpg)

[Refer - 在 Mac OSX 上編譯 GH60 RevCHN Firmware](http://blog.dm4.tw/blog/2015/03/17/build-gh60-revchn-on-mac/)
