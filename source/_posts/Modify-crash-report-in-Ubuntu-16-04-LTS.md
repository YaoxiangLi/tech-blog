---
title: Modify crash report in Ubuntu 16.04 LTS
categories: Linux
abbrlink: 28172
date: 2016-11-12 17:31:09
tags:
  - Linux
---

Sometimes the Ubuntu crash reports are annoying, so we can disable it by the following simple procedure:

```bash
sudo rm /var/crash/*

sudo vim /etc/default/apport
```

And set "enabled=0"