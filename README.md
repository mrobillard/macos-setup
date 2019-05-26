# macOS Setup 

My personal preferences for setting up a new macOS machine. 

This list contains setup for all the essential languages and tools for development.  

* [System Preferences](#system-preferences)
* [Terminals](#terminals)
* [Homebrew](#homebrew)
* [Git](#git)
* [Docker](#docker)

## System Preferences

There are a couple of tweaks I like to make to the System Preferences that are especially helpful for development. Feel free to follow these, or to ignore them, depending on your personal preferences.

In Apple Icon > System Preferences:

Trackpad > Tap to click
Keyboard > Key Repeat > Fast (all the way to the right)
Keyboard > Delay Until Repeat > Short (all the way to the right)

## Terminals

My primary (and favorite) terminal is iTerm2. Hyper is a pretty cool terminal project still under active development not a bad alternative. There are instances where I prefer it, but as of time of writing, there's still a noticable level of feature disparity. 

### iTerm2

The latest release of iTerm2 can be found [here](https://www.iterm2.com/downloads.html).

### Hyper

The lastest release of Hyper can be found [here](https://hyper.is/#installation).

## Homebrew

Homebrew is the standard package manger for macOS. 

### XCode Developer Tools 

The XCode Developer Tools are a collection of compilers and also a dependency for Homebrew. 

```
xcode-select --install
```

### Install

Install Homebrew by copy-pasting the installation command from the [Homebrew homepage](https://brew.sh/):

```
/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
```

Check install:

```
brew doctor
```

### Homebrew Services 

Homebrew Services is an extension of Homebrew that launches services (i.e. database) when you start your computer so you don't have to manually. This automatically installs itself the first time you run it, so all you need to do is add a service.

```
brew services start <formula>
```

## Git 

macOS comes with a system version of Git, but I always prefer to install my own for easy upgrades and to avoid interfering with the pre-installed version. 

```
brew install git
```

## Docker 
