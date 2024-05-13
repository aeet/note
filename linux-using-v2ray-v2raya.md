---
title: "Linux using V2Ray & V2RayA"
date: "2023-11-09"
categories: 
  - "tinkering-with-my-linux"
  - "tossing-around"
tags: 
  - "linux"
  - "proxy"
  - "v2ray"
coverImage: "c53c811f880411ebb6edd017c2d2eca2-scaled.jpg"
---

# Intro

The materials used in the article can be found in the following links

- [https://github.com/v2fly/fhs-install-v2ray](https://github.com/v2fly/fhs-install-v2ray)
- [https://github.com/v2rayA/v2rayA](https://github.com/v2rayA/v2rayA)

# How to install

download the bash shell

```bash
curl -L https://raw.githubusercontent.com/v2fly/fhs-install-v2ray/master/install-release.sh >> install.sh
```

or download via proxy

```bash
curl -L -p http://host:port https://raw.githubusercontent.com/v2fly/fhs-install-v2ray/master/install-release.sh >> install.sh
```

run bash

```bash
bash ./install.sh
```

or run bash via proxy

```bash
bash ./install.sh -p http://host:port
```

the bash script will generate some file in your system

```bash
installed: /usr/local/bin/v2ray
installed: /usr/local/bin/v2ctl
installed: /usr/local/share/v2ray/geoip.dat
installed: /usr/local/share/v2ray/geosite.dat
installed: /usr/local/etc/v2ray/config.json
installed: /var/log/v2ray/
installed: /var/log/v2ray/access.log
installed: /var/log/v2ray/error.log
installed: /etc/systemd/system/v2ray.service
installed: /etc/systemd/system/v2ray@.service
```

enable v2ray service

```bash
sudo systemctl enable v2ray.service
sudo systemctl start v2ray.service
```

download the v2rayA via release page and install it [https://github.com/v2rayA/v2rayA/releases](https://github.com/v2rayA/v2rayA/releases)

enable v2rayA service

```bash
sudo systemctl enable v2rayA.service
sudo systemctl start v2rayA.service
```
