---
title: Ubuntu 16.04 LTS & Windows 10 dual boot time zone difference
categories: Linux
abbrlink: 56303
date: 2016-12-09 08:32:13
tags:
    - Linux
---
For users who dual boot Ubuntu 16.04 and Windows, you may find the clock time is off that causes time differences after you reboot and switch between the two systems. Here’s how to fix it.

Ubuntu maintains the hardware clock (RTC, real time clock) in universal time (UTC) by default while Windows maintains the clock in local time, thus causing time conflicts between Ubuntu and Windows.

To fix it, either set Ubuntu to maintain RTC in local time or make Windows uses UTC.

1. Disable UTC and use Local Time in Ubuntu:

In previous Ubuntu editions, you can edit the config file /etc/default/rcS to disable UTC.

In Ubuntu 16.04, open terminal (Ctrl+Alt+T) and run the command below instead:

```bash
timedatectl set-local-rtc 1 --adjust-system-clock
```

To check out if your system uses Local time, just run:

```bash
timedatectl
```

Finally restart and switch to Windows, adjust system clock time if need and done.

2. Make MicroSoft Windows uses UTC:

Another way to fix this issue is doing the following changes in Windows, Windows 10, in the case below:

- First if you’ve switched to local time in Ubuntu, run command in Ubuntu terminal to use back UTC:

```bash
timedatectl set-local-rtc 0
```

- Restart and select boot into Windows 10, when you’re in, do:

go to Start Menu, search for and launch cmd as Administrator.
When the command console opens, paste below command to create a DWORD value to the registry:
> Reg add HKLM\SYSTEM\CurrentControlSet\Control\TimeZoneInformation /v RealTimeIsUniversal /t REG_DWORD /d 1

For 64-bit Windows, use a QWORD value instead:

> Reg add HKLM\SYSTEM\CurrentControlSet\Control\TimeZoneInformation /v RealTimeIsUniversal /t REG_QWORD /d 1