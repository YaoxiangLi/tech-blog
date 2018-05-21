---
title: Create swap file on Linux
categories: Linux
abbrlink: 52606
date: 2015-06-25 16:27:18
tags:
    - Linux
---
Swap is space on a disk that is reserved to be used as virtual memory. When a Linux server runs out of memory, the kernel can move inactive processes into swap to make room for active processes in the working memory.

A swap partition is not present on Cloud Servers by default, but swap can be added to a server by allocating a swap file. The performance of a swap file is similar to that of a swap partition while making it easier to control the swap size without repartitioning a volume. How aggressively the server will use this swap space can be controlled by modifying the system’s swappiness value.

The steps below discuss the creation of a swap file on Linux and modifying the system swappiness value.

How do I add swap?
To add 1GB of swap to your server, for example, follow these steps:

Create the file to be used for swap.

```bash
sudo fallocate -l 1G /mnt/1GB.swap
```

If fallocate fails or is not installed, run the following command.

```bash
sudo dd if=/dev/zero of=/mnt/1GB.swap bs=1024 count=1048576
```

Format the file for swap.

```bash
sudo mkswap /mnt/1GB.swap
```

Add the file to the system as a swap file.

```bash
sudo swapon /mnt/1GB.swap
```

Add this line to the end of `/etc/fstab` to make the change permanent.

```bash
/mnt/1GB.swap  none  swap  sw 0  0
```

To change the swappiness value edit `/etc/sysctl.conf` and add the following line.

```bash
vm.swappiness=10
```

Start with a value of 10 and increase if needed. A typical default value for swappiness is 60. The higher the number (up to 100), the more often swap is utilized.

How much swappiness affects performance depends on how your memory is being used, so experiment to find an optimal value. At 0 the swap file will only be used when the system runs completely out of memory. Higher values let the system swap idle processes out to allow the system to free memory for disk caching, potentially improving overall system performance.

Check that the swap file was created.

```bash
sudo swapon -s
```

Reboot the server to ensure that the changes go into effect.

Note: By following these instructions on a newly created Rackspace server, the resulting swap file is world-readable. To prevent the file from being world-readable, you should set up the correct permissions on the swap partition/file by running the following command to change the permission:

```bash
sudo chmod 600 /mnt/1GB.swap
```

In most cases, the only user that needs access to the swap partition is the root user.
