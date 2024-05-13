---
title: "Linux ranger"
date: "2023-10-03"
categories: 
  - "tinkering-with-my-linux"
  - "tossing-around"
tags: 
  - "linux"
coverImage: "e5c79b438f6544b1ac55ea167c5f28cd-scaled.jpg"
---

# installation

```
sudo apt install ranger
ranger --copy-config=all
```

# icon

[https://github.com/cdump/ranger-devicons2](https://github.com/cdump/ranger-devicons2)

```
git clone https://github.com/cdump/ranger-devicons2 ~/.config/ranger/plugins/devicons2
```

Add/change `default_linemode devicons2` in your `~/.config/ranger/rc.conf`
