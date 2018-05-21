---
title: Consolas Font On Ubuntu
categories: Linux
abbrlink: 41123
date: 2013-07-14 04:40:10
tags:
    - Linux
---
Consolas is not installed by default on Ubuntu, but we can get it.

```bash
sudo apt-get install font-manager
sudo apt-get install cabextract
```

Create a file named consolas.sh with following contents:

```bash
#!/bin/sh
set -e
set -x
mkdir temp
cd temp
wget http://download.microsoft.com/download/E/6/7/E675FFFC-2A6D-4AB0-B3EB-27C9F8C8F696/PowerPointViewer.exe
cabextract -L -F ppviewer.cab PowerPointViewer.exe
cabextract ppviewer.cab
```

Run it!

```bash
bash consolas.sh
```
