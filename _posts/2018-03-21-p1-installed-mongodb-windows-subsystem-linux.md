---
layout: post
title: "Installed MongoDB on Windows Subsystem for Linux"
---

## Pontifications
 
* I installed ongoDB on Windows Subsystem for Linux by following [Rob Aird's Setting Up Windows for Web Development](https://blog.cloudboost.io/setting-up-windows-for-web-development-28483d245a82)
* Specifically using the following commands (make sure quotes are plain ole double quotes i.e. ```"``` and not fancy open and closing quotes

    ```bash
    sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 0C49F3730359A14518585931BC711F9BA15703C6
    echo "deb [ arch=amd64,arm64 ] http://repo.mongodb.org/apt/ubuntu xenial/mongodb-org/3.4 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-3.4.list
    sudo apt-get update
    sudo apt-get install mongodb #(this will install an old version, but is seemingly necessary for reasons unknown)
    sudo apt-get install -y mongodb-org  #(this installs the newest version)
    ```

* To start mongodb:

```bash
sudo service mongodb start
```