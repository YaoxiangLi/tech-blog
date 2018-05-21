---
title: Change GRUB boot order for Ubuntu 16.04 LTS and Windows 10 dual boot
categories: Linux
abbrlink: 40789
date: 2016-09-21 10:03:20
tags:
    - Linux
---
GRUB Customizer is an easy, GUI way to change the GRUB boot order, without having to edit system files manually.

To install it, we first need to add the repository:

```bash
sudo add-apt-repository ppa:danielrichter2007/grub-customizer -y
sudo apt-get update && sudo apt-get install grub-customizer -y
```

At the end of the installation, we start GRUB customizer with:

```bash
sudo grub-customizer
```

Then modify the boot order manually.