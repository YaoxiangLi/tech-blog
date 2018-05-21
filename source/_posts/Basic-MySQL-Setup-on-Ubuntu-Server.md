---
title: Basic MySQL Setup on Ubuntu Server
tags:
  - MySQL
  - Ubuntu
  - Linux
categories:
  - MySQL
abbrlink: 1079
date: 2014-07-14 18:29:16
---

## Install MySQL on Ubuntu

It is pretty simple to install MySQL on Ubuntu:

```bash
sudo apt-get update
sudo apt-get install mysql-server
mysql_secure_installation
```

## Access the Database

Login to the database

```bash
mysql -u root -p
```

## Basic Usage

Show all the databases

```mysql
SHOW DATABASES;
```

Create a database

```mysql
CREATE DATABASE database_name;
SHOW DATABASES;
DROP DATABASE database_name;
USE database_name;
SHOW tables;
```
