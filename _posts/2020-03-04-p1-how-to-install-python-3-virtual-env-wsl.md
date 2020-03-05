---
layout: post
title: "How to install python 3.7 into a python virtualenv on WSL"
---

# Pontifications

* This leaves the pre-installed python alone! And I think this will work on any Linux not just in a distro on WSL!

```bash

sudo apt update
sudo apt install software-properties-common
sudo add-apt-repository ppa:deadsnakes/ppa

sudo apt install python3.7

virtualenv -p /usr/bin/python3.7 ~/PYTHON3.7/canosp_python_37
cd canosp_python_37/bin
source activate
```