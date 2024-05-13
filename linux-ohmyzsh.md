---
title: "Linux ohmyzsh"
date: "2023-10-03"
categories: 
  - "tinkering-with-my-linux"
  - "tossing-around"
tags: 
  - "linux"
coverImage: "25694c0d899e4160a36fd77e8bf4830e.png"
---

# precondition

```
sudo apt install zsh
chsh -s /usr/bin/zsh
```

# ohmyzsh

```
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

# powerlevel10k

[https://github.com/romkatv/powerlevel10k](https://github.com/romkatv/powerlevel10k)

```
cd  ~/.oh-my-zsh/custom/themes
git clone https://github.com/romkatv/powerlevel10k
```

edit `.zshrc` and set `ZSH_THEME`

```
ZSH_THEME="powerlevel10k/powerlevel10k"
```

# plugins

[https://github.com/zsh-users](https://github.com/zsh-users) [https://github.com/wbingli/zsh-wakatime](https://github.com/wbingli/zsh-wakatime)

```
cd  ~/.oh-my-zsh/custom/plugins
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git  
git clone https://github.com/zsh-users/zsh-autosuggestions.git
git clone https://github.com/zsh-users/zsh-completions.git
git clone https://github.com/zsh-users/zsh-history-substring-search.git
git clone https://github.com/wbingli/zsh-wakatime.git
```

edit `.zshrc`

```
plugins=(
        git
        fzf
        zsh-syntax-highlighting
        zsh-autosuggestions
        zsh-completions
        zsh-history-substring-search
        zsh-wakatime
)
```
