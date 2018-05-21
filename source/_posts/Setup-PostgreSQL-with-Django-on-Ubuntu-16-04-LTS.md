---
title: Setup PostgreSQL with Django on Ubuntu 16.04 LTS
tags: 
    - Django
    - PostgreSQL
    - Web
categories: Databases
abbrlink: 40743
date: 2016-07-21 10:58:33
---

## Install the PostgreSQL

The Ubuntu's package repositories have the PostgreSQL packages, to install it:

```bash
sudo apt-get update
sudo apt-get install postgresql postgresql-contrib -y
```

Then you are able to check the status of the PostgreSQL service:

```bash
sudo service postgresql status
```

And return something like this:

```bash
● postgresql.service - PostgreSQL RDBMS
   Loaded: loaded (/lib/systemd/system/postgresql.service; enabled; vendor prese
   Active: active (exited) since Wed 2016-07-20 20:35:43 UTC; 1min 24s ago
 Main PID: 19535 (code=exited, status=0/SUCCESS)
   CGroup: /system.slice/postgresql.service

July 20 20:35:43 ip-172-31-18-239 systemd[1]: Starting PostgreSQL RDBMS...
July 20 20:35:43 ip-172-31-18-239 systemd[1]: Started PostgreSQL RDBMS.
July 20 20:35:48 ip-172-31-18-239 systemd[1]: Started PostgreSQL RDBMS.
```

## Access the database

By default, Postgres uses a concept called "roles" to handle in authentication and authorization.

Upon installation Postgres is set up to use ident authentication, which means that it associates Postgres roles with a matching Linux system account. If a role exists within Postgres, a Linux username with the same name will be able to sign in as that role.

So there are several ways to sign in:

- Switch to the postgres account created by the Postgres installaton procedure
- Access this postgres account with `sudo`
- Create a new role

### Switch to postgres account

Switch to the postgres user using:

```bash
sudo su - postgres
```

Or using:

```bash
sudo -i -u postgres
```

Then access a Postgres prompt:

```bash
psql
```

Type following to exit the Postgres prompt:

```postgres
\q
```

And exit the account:

```bash
exit
```

### Access this postgres account without switch to it

You can use `sudo -u UserA CommandA` to execute the `CommandA` as `UserA`, for example:

```bash
sudo whoami
>"Your current user name"
sudo -u postgres whoami
>postgres
```

So type:

```bash
sudo -u postgres psql
```

You will directly log into Postgres prompt.

### Create a new role to manage your database

#### Create a new role

By default installation, we only have a `postgres` role to regulate the database.

We can create new roles from the command line with the `createrole` command. The `--interactive` flag will prompt you for the necessary values.

You can logged in as the postgres account, then typing:

```bash
createuser --interactive
```

Or you can also type `sudo -u postgres` without switch to `postgres` like we said before:

```bash
sudo -u postgres createuser --interactive
```

Both will show something like the following:

```bash
Enter name of role to add: rogue
Shall the new role be a superuser? (y/n) y
```

#### Create a New Database

The Postgres authentication system makes is that there will be an database with the same name as the role being used to login, which the role has access to.

So if in the last section, we created a user called `rogue`, that role will attempt to connect to a database which is also called `rogue` by default. You can create the appropriate database with the createdb command.

If you are logged in as the postgres account, you would type something like:

```bash
createdb rogue
```

Or use `sudo` from none postgres account:

```bash
sudo -u postgres createdb rogue
```

#### Enter a Postgres prompt with the New Role

If you want to enter the Postgres prompt with the new role just created and type in:

```bash
sudo -u rogue psql
```

You will find a error:

```bash
sudo: unknown user: rogue
sudo: unable to initialize policy plugin
```

That is because to log in with ident based authentication, you'll need a Linux user with the same name as your Postgres role and database.

If you don't have a matching Linux user available, you can create one with the adduser command. You will have to do this from an account with sudo privileges (not logged in as the postgres user):

```bash
sudo adduser rogue
```

Once you have the appropriate account available, you can either switch over and connect to the database by typing:

```bash
sudo -i -u rogue
psql
```

Or, you can do this inline:

```bash
sudo -u rogue psql
```

You will be logged in automatically assuming that all of the components have been properly configured.

If you want your user to connect to a different database, you can do so by specifying the database like this:

```bash
psql -d postgres
```

Once logged in, you can get check your current connection information by typing:

```postgresql
rogue=# \conninfo
```

Output

```postgresql
You are connected to database "rogue" as user "rogue" via socket in "/var/run/postgresql" at port "5432".
```

This can be useful if you are connecting to non-default databases or with non-default users.

## Integreting with Django

After entering the postgres prompt, create a database for Django project:

```postgresql
CREATE DATABASE myproject;
```

```postgresql
CREATE USER myprojectuser WITH PASSWORD 'password';
```

Set encoding to UTF-8:

```postgresql
ALTER ROLE myprojectuser SET client_encoding TO 'utf8';
```

Give the database user access to database:

```postgresql
GRANT ALL PRIVILEGES ON DATABASE myproject TO myprojectuser;
```

Go back to Django virtual envrionment and install psycopg2

```bash
pip install django psycopg2
```
