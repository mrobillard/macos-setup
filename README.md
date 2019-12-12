# macOS Setup 

My personal preferences for setting up a new macOS machine. 

This list contains setup for all the essential languages and tools for development.

* [System Preferences](#system-preferences)
* [Terminals](#terminals)
* [Homebrew](#homebrew)
* [Git](#git)
* [Vim](#vim)
* [Python](#python)
* [Node.js](#node.js)
* [Go](#go)
* [Ruby](#ruby)
* [Java](#java)
* [Julia](#julia)
* [Rust](#rust)
* [Docker](#docker)
* [AWS](#aws)
* [Heroku](#heroku)
* [PostgresSQL](#postgressql)
* [MongoDB](#mongodb)
* [Redis](#redis)
* [Elastic Search](#elasticsearch)
* [LaTeX](#latex)

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

1. From my personal [dotfiles](https://github.com/mrobillard/dotfiles), my .vim setup, which is a little more heavily configured.

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

The Anaconda/Miniconda distributions of Python come with many useful tools for scientific computing. For numerical and scientific computing, I prefer to use this distribution because its standard across the community. 

```
pyenv install miniconda3-x.x.x
```

Or

```
pyenv install anaconda3-x.x.x
```

After loading an Anaconda or Miniconda Python distribution into your shell, you can create conda environments (which are similar to virtualenvs):

```
pyenv shell miniconda3-x.x.x
conda create --name  mycondaproject
conda activate mycondaproject
```

I typically create two default environments for Py2 and Py3. 

Install the Jupyter Notebook (and any other packages), using:

```
conda install jupyter
```

Check that Jupyter installed properly:

```
jupyter notebook
```

Deactivate the environment, and return to the default Python version with:

```
conda deactivate
pyenv shell --unset
```

## Node.js 

The recommended way to install [Node.js](https://nodejs.org) is to use [nvm](https://github.com/nvm-sh/nvm) (Node Version Manager) which allows you to manage multiple versions of Node.js on the same machine.

Install nvm by copy-pasting the [install script command](https://github.com/nvm-sh/nvm#install--update-script) into your terminal.

Once that is done, open a new terminal and verify that it was installed correctly by running:

```
command -v nvm
```

View the all available stable versions of Node with:


```
nvm ls-remote --lts
```

Install the latest stable version with:


```
nvm install node
```

### npm

By default, installing Node also installs the package manager, npm.

## Go

Install Golang with brew:

```
brew install golang
```

### Setting up the Workspace 

Go has a different approach for managing code, so you'll need to set up a workspace. Add the following lines to your `.zshrc` (or `.bashrc`):

```
export GOPATH=$HOME/development/go-workspace # don't forget to change your path correctly!
export GOROOT=/usr/local/opt/go/libexec
export PATH=$PATH:$GOPATH/bin
export PATH=$PATH:$GOROOT/bin
```

To create your workspace, create the following directories:

```
mkdir -p $GOPATH $GOPATH/src $GOPATH/pkg $GOPATH/bin
```

Your workspace structure should look as follows:

`$GOPATH/src` : Where your Go projects / programs are located
`$GOPATH/pkg` : Contains all package objects
`$GOPATH/bin` : The home for compiled binaries 

## Ruby 

Ruby comes installed on Unix systems, but we don't want to run the risk of interfering with the system version. 

### Install 

The recommended way to install Ruby is to use rbenv, which allows you to manage multiple versions of Ruby on the same machine. You can install rbenv with Homebrew:

```
brew install rbenv
```

Add it to your `.zshrc` or `.bash_profile` and source the file:

```
eval "$(rbenv init -)"
```

## Java 

To install the latest version of Java, use:

```
brew install homebrew/cask/java 
```

## Julia 

Download the most current stable release from [here](https://julialang.org/downloads/) and install.

To call Julia from the command line, it needs to be accessible via your path. My preffered method is to symlink the binary to `/usr/local/bin` which is already in your `PATH` (update the version number appropriately):

```
ln -fs "/Applications/Julia-1.2.app/Contents/Resources/julia/bin/julia" /usr/local/bin/julia
```

Or you can add the application to your `PATH` directly:

```
PATH="/Applications/Julia-1.2.app/Contents/Resources/julia/bin/:${PATH}"
export PATH
```

## Rust 

Download and install the installation script:

```
curl https://sh.rustup.rs -sSf | sh
```

To configure your currnet shell, add Rust to your system path (_Note: This will be done automatically next time you login to a new shell_):

```
source $HOME/.cargo/env
```

To check that everything was installed correctly, run:

```
rustc --version
```

You should see output in the following format: `rustc x.y.z (abcabcabc yyyy-mm-dd)`

### Updating

To update Rust, run:

```
rustup update
```

## Docker 

Download the latest stable version of Docker for macOS [here](https://download.docker.com/mac/stable/Docker.dmg). After the application is installed, you'll be able to sign in to your Docker account. 

To check that everything was installed correctly, run the following:

```
docker version
docker-compose version
docker-machine version
```

## AWS

If you don't already, create an [AWS](https://aws.amazon.com/account/) account.

### CLI 

My preffered method is to install using pip3. You can also use cURL (instructions [here](https://docs.aws.amazon.com/cli/latest/userguide/install-macos.html)).

```
pip3 install awscli --upgrade --user
```

Verify that it was installed correctly: 

```
aws --version
```

Add an export command to the top of your shell's profile script and source the file:

```
export PATH=~/.local/bin:$PATH
```

## Heroku 

Make sure you have a [Heroku](https://www.heroku.com/) account. 

### Install CLI 

```
brew tap heroku/brew
brew install heroku
```

Login to your account:

```
heroku login 
```

## PostgresSQL

Install using Homebrew:

```
brew install postgresql
```

It will automatically add itself to Homebrew Services. Start it with:

```
brew services start postgresql
```

### pgAdmin

pdAdmin is an administration and development platform for PostgresSQL and can be downloaded [here](https://www.pgadmin.org/download/).

### GUI

My current favorite client is [TablePlus](https://tableplus.com/)

## MongoDB

Install using Homebrew:

```
brew install mongodb
```

Create a data directory for databases and make sure it's accessible:

```
mkdir -p /data/db
sudo chown -R `id -un` /data/db
```

## Redis 

To install [Redis](https://redis.io/), use Homebrew:

```
brew install redis
```

Start it through Homebrew Services with:

```
brew services start redis 
```

## Elastic Search 

### Install 

Elastic Search runs on Java, so make sure Java is installed:

```
java --version
```

If Java is not installed, use Homebrew to install Java8 (ElasticSearch _needs_ Java8):

```
brew cask install adoptopenjdk/openjdk/adoptopenjdk8
```

Next, install ES with Homebrew:

```
brew tap elastic/tap
brew install elastic/tap/elasticsearch-full
```

## LaTeX

There are two options to install LaTeX on macOS:

1. Install MacTeX with builtin editor(TexLive) - (2GB)
2. Install BasicTeX only (100MB) + your personal LaTeX editor

To install MacTex, as I typically do, download [here](http://www.tug.org/mactex/downloading.html).

### LaTeX

My editor of choice is [Texpad](https://www.texpad.com/).

