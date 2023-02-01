---
layout: post
title: "How To get ngrok working with SSH on WSL"
---
*  Having lots of fun testing ngrok.As of today, here's how to get ngrok working with ssh from macOS to WSL
* 1\. Generate an SSH Key on your mac, let's call it `wsl2`. This key must have a passphrase or it won't work. Add it to the keychain.
* 2\. Copy the public key to the WSL machine e.g. using `croc` `croc ~/.ssh/wsl2.pub`
* 3\. Rename the nologin file to allow logins to WSL (Otherwise ssh will fail (it will be stuck on `Starting shell...` ):
```bash
sudo mv /var/run/nologin /var/run/2023-01-31-renamed-nologin
``` 
* 4\. start ngrok `ngrok tcp 22`
* 5\. SSH in e.g. `ssh -i ~/.ssh/wsl2.pub roland@somehost.tcp.ngrok.io -p <someport>`

### Previously
* Dec 2022: [Tailscale Funnel is a reverse proxy service complete with TLS cert, DNS, public IP address and HTTPS server that seems perfect for small, experimental software on the internet like snac2](http://rolandtanglao.com/2022/12/10/p1-tailscale-funnel-ideal-for-home-hosted-experimental-software/)
* Sep 2022: [Zack Scholl: croc Fast, simple, and e2e encrypted file transfer between any two computers. <- so many great CLI tools so little time. See 'Previously'](http://rolandtanglao.com/2022/09/04/p1-croc-fast-e2e-file-text-sharing-between-two-computers/)