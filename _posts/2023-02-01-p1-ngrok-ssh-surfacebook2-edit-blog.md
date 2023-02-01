---
layout: post
title: "How I use ngrok over SSH on my MacBook Air to edit my blog on my Surface Book 2"
---
*  This is straightforward. I just use the [editing over ssh feature](https://code.visualstudio.com/docs/remote/ssh) to enter the SSH connection command (`ssh -i ~/.ssh/wsl2.pub roland@somehost.tcp.ngrok.io -p <someport>`) in Visual Studio Code (and of course I could always use emacs to edit over ssh which I've done for decades!).
* And I use the terminal feature to trigger a jekyll rebuild and then `surge` to upload my blog and git all in Visual Studio Code's terminal.
* Finally I have another ngrok tunnel running that maps port 4000 to port 80 to see the rendered draft version at: https://somejekyllsubdomainofmydraftblog.ngrok.io/
* Super geeky :-) but then I can edit on any of my 5 laptops (including my MacBook Air) because this recipe will work on any computer that runs Visual Studio Code.
* Question: Does Typora or any other nice SSH editor work over SSH? VS Code is fine but not nearly as nice as Typora!

### Previously
* January 31, 2023: [How To get ngrok working with SSH on WSL](http://rolandtanglao.com/2023/01/31/p1-ngrok-ssh-wsl-var-run-nogin/)