---
title: General settings on Mac
categories: Mac
abbrlink: 48869
date: 2018-03-12 16:20:11
tags:
    - Mac
    - System Tweak
---
Here are some tips on setting up a Mac for developers. (Avaliable for 10.13.3)

# System settings

## Reduce graphic effects

Go to System Preferences -- Accessibility -- Display, choose:

- "Reduce motion"
- "Reduce transparency".

Go to System Preferences -- Mission Control, turn dashoboard to "off".

## Enable three fingers drag and four fingers swipe

Go to System Preferences -- Trackpad -- Point & Click, enable "Tap to click".
Go to System Preferences -- Trackpad -- More Gestures -- Mission Control, enable "Swipe up with four fingers".

Go to System Preferences -- Accessibility -- Mouse & Trackpad -- Trackpad Options, enable "dragging with three fingers"

## Improve the dock showup speed

Open terminal and type in:

```bash
defaults write com.apple.dock autohide-delay -int 0
```

## Change default layout of launchpad display

For example, you can customize the rows and columns of the launchpad springboard, say, into 9 columns and 7 rows 

```bash
defaults write com.apple.dock springboard-columns -int 9
defaults write com.apple.dock springboard-rows -int 7
defaults write com.apple.dock ResetLaunchPad -bool TRUE; killall Dock
```

Or reset it to default columns and rows

```bash
defaults delete com.apple.dock springboard-rows
defaults delete com.apple.dock springboard-columns
defaults write com.apple.dock ResetLaunchPad -bool TRUE;killall Dock
```

# Development tools

## Install brew

```bash
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

## Using zsh shell

```bash
# Install
curl -L https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh | sh
# Create config file(Environment variables will be updated in .zshrc)
cp ~/.oh-my-zsh/templates/zshrc.zsh-template ~/.zshrc
# Using zsh
chsh -s /bin/zsh
```

## Enable vim syntax

```bash
vim ~/.vimrc
## appending following two lines
syntax on
set nu!
```
