---
title: "Linux installation lunarvim"
date: "2023-10-03"
categories: 
  - "tinkering-with-my-linux"
  - "tossing-around"
tags: 
  - "linux"
coverImage: "c00dafdb5ab847aea5b5a03bd457c6bf-scaled.jpg"
---

# precondition

## pip

### pip2

```
sudo apt-get install python2
wget https://bootstrap.pypa.io/pip/2.7/get-pip.py
python2 get-pip.py
~/.local/bin/pip2 install neovim --user
```

### pip3

```
wget https://bootstrap.pypa.io/get-pip.py
python3 get-pip.py
~/.local/bin/pip3 install neovim --user
```

### env

```
export PATH=$PATH:/home/cui/.local/bin
```

## dependencies

### fd

[https://github.com/sharkdp/fd?tab=readme-ov-file#on-ubuntu](https://github.com/sharkdp/fd?tab=readme-ov-file#on-ubuntu)

```
sudo apt install fd-find
```

### lazygit

[https://github.com/jesseduffield/lazygit?tab=readme-ov-file#ubuntu](https://github.com/jesseduffield/lazygit?tab=readme-ov-file#ubuntu)

```
LAZYGIT_VERSION=$(curl -s "https://api.github.com/repos/jesseduffield/lazygit/releases/latest" | grep -Po '"tag_name": "v\K[^"]*')
curl -Lo lazygit.tar.gz "https://github.com/jesseduffield/lazygit/releases/latest/download/lazygit_${LAZYGIT_VERSION}_Linux_x86_64.tar.gz"
tar xf lazygit.tar.gz lazygit
sudo install lazygit /usr/local/bin
```

### ripgrep

```
sudo apt install ripgrep
```

### fzf

```
sudo apt install fzf
```

## neovim

[https://github.com/neovim/neovim/wiki/Installing-Neovim](https://github.com/neovim/neovim/wiki/Installing-Neovim)

```
sudo apt install cmake
git clone https://github.com/neovim/neovim.git
cd neovim
make CMAKE_BUILD_TYPE=RelWithDebInfo
sudo make install
```

## nodejs

[https://github.com/nvm-sh/nvm?tab=readme-ov-file#installing-and-updating](https://github.com/nvm-sh/nvm?tab=readme-ov-file#installing-and-updating)

```
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.5/install.sh | bash
nvm install 16.19.0
nvm use 16.19.0
```

## rust

[https://www.rust-lang.org/tools/install](https://www.rust-lang.org/tools/install)

```
curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh
```

# installation

[https://www.lunarvim.org/zh-Hans/docs/installation](https://www.lunarvim.org/zh-Hans/docs/installation)

```
LV_BRANCH='release-1.3/neovim-0.9' bash <(curl -s https://raw.githubusercontent.com/LunarVim/LunarVim/release-1.3/neovim-0.9/utils/installer/install.sh)
```
