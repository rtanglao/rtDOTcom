---
layout: post
title: "How to make Hugo work on WSL aka Windows Subystem for Linux"
---

## Pontifications
* change ```0.41``` to whatever the current version of Hugo is
* From [https://github.com/rtanglao/rt-making-wsl-and-windows-work-for-me/blob/master/README.md#04june2018-hugo](https://github.com/rtanglao/rt-making-wsl-and-windows-work-for-me/blob/master/README.md#04june2018-hugo) 

```bash
wget -O /tmp/hugo_0.41_Linux-64bit.deb https://github.com/spf13/hugo/releases/download/v0.41/hugo_0.41_Linux-64bit.deb
sudo apt install /tmp/hugo_0.41_Linux-64bit.deb
hugo version
Hugo Static Site Generator v0.41 linux/amd64 BuildDate: 2018-05-25T16:57:20Z
# cd to your hugo site top directory
cd themes
git clone https://github.com/halogenica/beautifulhugo.git beautifulhugo
```


