---
title: The importance of NVM for Node.js installation
tags:
  - Node.js
  - NVM
categories: JavaScript
abbrlink: 11132
date: 2018-02-27 02:30:23
---

An alternative to installing Node.js through apt is to use a specially designed tool called nvm, which stands for "Node.js version manager". Rather than working at the operating system level, nvm works at the level of an independent directory within your home directory. This means that you can install multiple, self-contained versions of Node.js without affecting the entire system.

Controlling your environment with nvm allows you to access the newest versions of Node.js and retain and manage previous releases. It is a different utility from apt-get, however, and the versions of Node.js that you manage through it are distinct from the distro-stable version of Node.js available from the Ubuntu repositories.

To start off, we'll need to get the software packages from our Ubuntu repositories that will allow us to build source packages. The nvm script will leverage these tools to build the necessary components:

```bash
sudo apt-get update
sudo apt-get install build-essential libssl-dev
```

Once the prerequisite packages are installed, you can pull down the nvm installation script from the project's GitHub page. The version number may be different, but in general, you can download it with curl:

```bash
curl -sL https://raw.githubusercontent.com/creationix/nvm/v0.33.8/install.sh -o install_nvm.sh
```

And inspect the installation script with nano:

```bash
nano install_nvm.sh
```

Run the script with bash:

```bash
bash install_nvm.sh
```

It will install the software into a subdirectory of your home directory at ~/.nvm. It will also add the necessary lines to your ~/.profile file to use the file.

To gain access to the nvm functionality, you'll need to log out and log back in again, or you can source the ~/.profile file so that your current session knows about the changes:

```bash
source ~/.profile
```

Now that you have nvm installed, you can install isolated Node.js versions.

To find out the versions of Node.js that are available for installation, you can type:

```bash
nvm ls-remote
```

As you can see, the newest LTS version at the time of this writing is v8.9.4. You can install that by typing:

```bash
nvm install 8.9.4
```

Usually, nvm will switch to use the most recently installed version. You can explicitly tell nvm to use the version we just downloaded by typing:

```bash
nvm use 8.9.4
```

When you install Node.js using nvm, the executable is called node. You can see the version currently being used by the shell by typing:

```bash
node -v
Output
v8.9.4
```

If you have multiple Node.js versions, you can see what is installed by typing:

```bash
nvm ls
```

If you wish to default one of the versions, you can type:

```bash
nvm alias default 8.9.4
```

This version will be automatically selected when a new session spawns. You can also reference it by the alias like this:

```bash
nvm use default
```

Each version of Node.js will keep track of its own packages and has npm available to manage these.

You can have npm install packages to the Node.js project's ./node_modules directory by using the normal format. For example, for the express module:

```bash
npm install express
```

If you'd like to install it globally (making it available to the other projects using the same Node.js version), you can add the -g flag:

```bash
npm install -g express
```

This will install the package in:

> ~/.nvm/node_version/lib/node_modules/package_name

Installing globally will let you run the commands from the command line, but you'll have to link the package into your local sphere to require it from within a program:

```bash
npm link express
```

You can learn more about the options available to you with nvm by typing:

```bash
nvm help
```
