# macOS Setup 

My personal preferences for setting up a new macOS machine. 

This list contains setup for all the essential languages and tools for development.  

* [System Preferences](#system-preferences)
* [Terminals](#terminals)
* [Homebrew](#homebrew)
* [Git](#git)
* [Vim](#vim)
* [Python](#python)

## System Preferences

There are a couple of tweaks I like to make to the System Preferences that are especially helpful for development. Feel free to follow these, or to ignore them, depending on your personal preferences.

In **Apple Icon > System Preferences**:

* Trackpad > Tap to click
* Keyboard > Key Repeat > Fast (all the way to the right)
* Keyboard > Delay Until Repeat > Short (all the way to the right)

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

Check that git is installed in `/usr/local/bin/git`:

```
which git 
```

### Configuration 

Download the [.gitconfig](https://raw.githubusercontent.com/mrobillard/macos-setup/master/.gitconfig) file to your home directory:

```
cd ~
curl -O https://raw.githubusercontent.com/mrobillard/macos-setup/master/.gitconfig
```

Set up Git user (this will update your .gitconfig):

```
git config --global user.name "Your Name Here"
git config --global user.email "your_email@youremail.com"
```

Update the .gitignore file to ignore `.DS_Store` (a hidden macOS system file that's put in folders).

```
cd ~
curl -O https://raw.githubusercontent.com/mrobillard/macos-setup/master/.gitignore
git config --global core.excludesfile ~/.gitignore
```

## Vim  

I use two different Vim configurations. 

1. From my personal dotfiles my .vim setup, which is a little more heavily configured.

```

```

2. If I need something simple with some basic ammenities, [tpope](https://github.com/tpope/vim-sensible) created a sensible list of defaults. 

```
mkdir -p ~/.vim/pack/tpope/start
cd ~/.vim/pack/tpope/start
git clone https://tpope.io/vim/sensible.git
```

## Python 

macOS ships with a system version of Python, but I always install my own versions alongside of it to avoid messing with the system install that other applications rely on. 

Install `pyenv` with Homebrew:

```
brew install pyenv
```

After `pyenv` is installed, you should see instructions to add the following to your `.bash_profile` or `.zshrc`.

```
if command -v pyenv 1>/dev/null 2>&1; then eval "$(pyenv init -)"; fi
```

Install the following dependencies:

```
brew install openssl readline sqlite3 xz zlib

```

Install the most recent versions of Python2 and Python3. 

```
pyenv install --list
pyenv install 3.x.x
pyenv install 2.x.x
```

Confirm that you have the desired versions installed and that the default version (marked with a `*`) is the system version. 

```
pyenv versions
```

### Using Pyenv

To switch the shell version of Python, run:

```
pyenv shell 3.x.x
```

To set a local directory to your desired version of Python, run:

```
pyenv local 3.x.x
```

This will save the desired version in a `.python-version` file. Next time you enter the project's directory from a terminal, `pyenv` will automatically load that version for you.

### Anaconda 


