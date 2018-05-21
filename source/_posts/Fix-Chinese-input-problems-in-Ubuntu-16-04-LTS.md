---
title: Fix Chinese input problems in Ubuntu 16.04 LTS
categories: Linux
abbrlink: 8205
date: 2016-10-29 11:03:01
tags:
    - Linux
---
The Chinese input is unabled by default in Ubuntu 16.04 LTS, type the following commands to install fcitx:

```bash
sudo apt install fcitx fcitx-googlepinyin fcitx-table-wbpy fcitx-pinyin fcitx-sunpinyin
```

- System Setting -- Language Support -- Keyboard input method system -- fcitx
- Restart your system
- Fcitx -- Configure -- deselect the show current language search "Google Pinyin", you are all set! Press Ctrl + Space to toggle between Chinese and English.