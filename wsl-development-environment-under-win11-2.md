---
title: "WSL development environment under Win11 - 2"
date: "2023-11-09"
categories: 
  - "tinkering-with-my-linux"
  - "tossing-around"
tags: 
  - "linux"
  - "wsl"
coverImage: "a05050278b4d45268de555032becdbb8-scaled.jpg"
---

# WSL development environment under Win11-2

# proxy

If you need a proxy, you can use the following script.

Be careful to change to your own port.

```bash
vim .zshrc / .bashrc

# and append that in your config

host_ip=$(cat /etc/resolv.conf |grep "nameserver" |cut -f 2 -d " ")
export HTTP_PROXY=$host_ip:7890
export HTTPS_PROXY=$host_ip:7890
export ALL_PROXY=http://$host_ip:7890
```

# oh-my-zsh

## zsh

```bash
sudo apt-get install zsh
chsh -s /usr/bin/zsh
```

## oh-my-zsh

Install ohmyzsh using wget or curl.

```bash
sh -c "$(curl -fsSL https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
or
sh -c "$(wget https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh -O -)"
```

## theme

i use the theme from [https://github.com/romkatv/powerlevel10k](https://github.com/romkatv/powerlevel10k).

install fonts at the first: [https://github.com/romkatv/powerlevel10k#fonts](https://github.com/romkatv/powerlevel10k#fonts)

clone it

```bash
git clone https://github.com/romkatv/powerlevel10k.git
mv powerlevel10k /home/{yourname}/.oh-my-zsh/custom/themes
```

and config it

```bash
vim ~/.zshrc

# choose the ZSH_THEME and input powerlevel10k/powerlevel10k
ZSH_THEME="powerlevel10k/powerlevel10k"

source ~/.zshrc
```

## plugins

the plugins home in `/home/{youname}/.oh-my-zsh/custom/plugins`

clone some plugins to this dir that from [https://github.com/zsh-users](https://github.com/zsh-users)

and config it into .zshrc like this

```bash
plugins=(
        git
        fzf
        zsh-autosuggestions
        zsh-completions
        zsh-history-substring-search
        zsh-syntax-highlighting
        zsh-wakatime
)
```

# homebrew

install: `/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"`

# neovim

`brew install neovim`

## pip2

```bash
sudo apt-get install python2
wget https://bootstrap.pypa.io/pip/2.7/get-pip.py
python2 get-pip.py
~/.local/bin/pip2 install neovim --user
```

## pip3

```bash
https://bootstrap.pypa.io/get-pip.py
python3 get-pip.py
~/.local/bin/pip3 install neovim --user
```

# lunarvim

## denpendencies

```bash
brew install ripgrep fd lazygit
```

## lunar

page: [https://www.lunarvim.org/01-installing.html#prerequisites](https://www.lunarvim.org/01-installing.html#prerequisites)

```bash
bash <(curl -s https://raw.githubusercontent.com/lunarvim/lunarvim/master/utils/installer/install.sh)
```

## lua

```bash
brew install lua luabind luarocks lua-language-server luajit luau lux lua@5.1 luaver lua@5.3
```

## go env

```bash
brew install go
```

## node env

```bash
brew install node
```

## java env

```bash
brew install openjdk openjdk@11 openjdk@8 maven gradle
```
