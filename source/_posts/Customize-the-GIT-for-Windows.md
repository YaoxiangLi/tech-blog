---
title: Customize the GIT for Windows
categories: Git
abbrlink: 7740
date: 2017-01-17 09:13:41
tags:
    - Git
---
How to customize The Git For Windows Bash Shell Prompt

The Git for Windows Bash prompt is set using a configuration shell script named git-prompt.sh that can be found in the following directory:
> C:\Program Files\Git\etc\profile.d\

To remove the "MINGW64" you need to remove the following two lines

> PS1="$PS1"'\[\033[35m\]' # change to purple 
> PS1="$PS1"'$MSYSTEM ' # show MSYSTEM

I like to also change the first PS1 line which sets the title by removing the

$TITLEPREFIX:

and replacing it with

Bash Prompt (Git for Windows) =>

Also remove two places of PS1="$PS1"'\n' for no new line.