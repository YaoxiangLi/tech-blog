---
title: Initial Server Setup for Ubuntu 16.04
tags:
  - Ubuntu
  - Linux
  - Server
  - SSH
categories: Ubuntu
abbrlink: 4167
date: 2016-05-12 23:11:44
---

When you first create a new Ubuntu 16.04 server, there are a few configuration steps that you should take early on as part of the basic setup. This will increase the security and usability of your server and will give you a solid foundation for subsequent actions.

## Step One — Root Login

The root user is the administrative user in a Linux environment that has very broad privileges. Because of the heightened privileges of the root account, you are actually discouraged from using it on a regular basis. This is because part of the power inherent with the root account is the ability to make very destructive changes, even by accident.

```bash
ssh root@your_server_ip
```

## Step Two — Create a New User

Once you are logged in as root, we're prepared to add the new user account that we will use to log in from now on.

This example creates a new user called "ubuntu", but you should replace it with a username that you like:

```bash
adduser ubuntu
```

## Step Three — Root Privileges

ow, we have a new user account with regular account privileges. However, we may sometimes need to do administrative tasks.

To avoid having to log out of our normal user and log back in as the root account, we can set up what is known as "superuser" or root privileges for our normal account. This will allow our normal user to run commands with administrative privileges by putting the word sudo before each command.

To add these privileges to our new user, we need to add the new user to the "sudo" group. By default, on Ubuntu 16.04, users who belong to the "sudo" group are allowed to use the sudo command.

As root, run this command to add your new user to the sudo group (substitute the highlighted word with your new user):

```bash
usermod -aG sudo sammy
```

## Step Four — Add Public Key Authentication (Recommended)

The next step in securing your server is to set up public key authentication for your new user. Setting this up will increase the security of your server by requiring a private SSH key to log in.

### Generate a Key Pair

If you do not already have an SSH key pair, which consists of a public and private key, you need to generate one. If you already have a key that you want to use, skip to the Copy the Public Key step.

To generate a new key pair, enter the following command at the terminal of your local machine (ie. your computer):

```bash
ssh-keygen
```

Assuming your local user is called "localuser", you will see output that looks like the following:

```bash
ssh-keygen output
Generating public/private rsa key pair.
Enter file in which to save the key (/Users/localuser/.ssh/id_rsa):
```

Hit return to accept this file name and path (or enter a new name).

Next, you will be prompted for a passphrase to secure the key with. You may either enter a passphrase or leave the passphrase blank.

This generates a private key, id_rsa, and a public key, id_rsa.pub, in the .ssh directory of the localuser's home directory. Remember that the private key should not be shared with anyone who should not have access to your servers!

### Copy the Public Key

After generating an SSH key pair, you will want to copy your public key to your new server. We will cover two easy ways to do this.

If your local machine has the ssh-copy-id script installed, you can use it to install your public key to any user that you have login credentials for.

Run the ssh-copy-id script by specifying the user and IP address of the server that you want to install the key on, like this:

```bash
ssh-copy-id ubuntu@your_server_ip
```

## Step Five — Disable Password Authentication (Recommended)

Now that your new user can use SSH keys to log in, you can increase your server's security by disabling password-only authentication. Doing so will restrict SSH access to your server to public key authentication only. That is, the only way to log in to your server (aside from the console) is to possess the private key that pairs with the public key that was installed.

To disable password authentication on your server, follow these steps.

As root or your new sudo user, open the SSH daemon configuration:

```bash
sudo nano /etc/ssh/sshd_config
```

Find the line that specifies PasswordAuthentication, uncomment it by deleting the preceding #, then change its value to "no". It should look like this after you have made the change:

```bash
PasswordAuthentication no
```
