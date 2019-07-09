---
layout: post
title: "How to setup github credential caching on Windows Linux subsystem"
---

## Pontifications
 
* Just one command from [How to use Git credential store on WSL (Ubuntu on Windows)?](https://stackoverflow.com/questions/45925964/how-to-use-git-credential-store-on-wsl-ubuntu-on-windows):

```bash
git config --global credential.helper cache
```

* I didn't have to change the timeout in ~/.gitconfig but just in case here's the line to add

```
[credential]
        helper = cache --timeout=144000
```
