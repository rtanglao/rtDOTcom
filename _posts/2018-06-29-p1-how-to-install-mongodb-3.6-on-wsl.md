---
layout: post
title: "Mikeysax: How to install MongoDB 3.6 on Windows 10 Subsystem for Linux"
---

## Pontifications
* Mikeysax's gist: [From Install Mongo with WSL for Windows.](https://gist.github.com/Mikeysax/cc86c30903727c556bcce960f7e4d59b) 

**QUOTE**

```bash
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 2930ADAE8CAF5059EE73BB4B58712A2291FA4AD5
echo "deb [ arch=amd64,arm64 ] https://repo.mongodb.org/apt/ubuntu xenial/mongodb-org/3.6 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.6.list
sudo apt-get update
sudo apt-get install -y mongodb-org
```

This will install the most stable version of mongod, 3.6 at time of writing. If you want to install a different version please refer to the [link](https://docs.mongodb.com/manual/tutorial/install-mongodb-on-ubuntu/) above.

**END QUOTE**
