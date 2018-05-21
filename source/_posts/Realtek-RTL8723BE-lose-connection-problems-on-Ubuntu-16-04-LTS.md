---
title: Realtek RTL8723BE wireless card lose connection problem on Ubuntu 16.04 LTS
categories: Linux
abbrlink: 7950
date: 2016-09-13 11:32:41
tags:
  - Linux
  - Wireless card
---
I was having these problem with rtl8723be on ubuntu 16.04.

I had to install new module for realtek wifi cards where they solved the constant disconnects:

install required packages

```bash
sudo apt-get install build-essential git
git clone new realtek wifi modules

git clone https://github.com/lwfinger/rtlwifi_new/
enter the directory

cd rtlwifi_new
build it

make
install

sudo make install
```

Now you can reboot or unload/load modules

unload modules

```bash
sudo modprobe -r rtl8723be
```

load new module

```bash
sudo modprobe rtl8723be
```

if it still doesn't work, try the solution from this post

```bash
echo "options rtl8723be fwlps=0" | sudo tee /etc/modprobe.d/rtl8723be.conf
```

Note: After each kernel update, you need to rebuild the modules. That is,

After every kernel update:

```bash
cd rtlwifi_new
```

Clean previous builds

```bash
make clean
```

Update git repository

```bash
git pull
```

Compile

```bash
make clean && make
```
Install

```bash
sudo make install
```

reboot or unload/load modules