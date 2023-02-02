---
layout: post
title: "How I use ngrok over SSH on my MacBook Air to edit my blog on my Surface Book 2"
---
*  This is straightforward. I just use the [editing over ssh feature](https://code.visualstudio.com/docs/remote/ssh) to enter the SSH connection command (`ssh -i ~/.ssh/wsl2.pub roland@somehost.tcp.ngrok.io -p <someport>`) in Visual Studio Code (and of course I could always use emacs to edit over ssh which I've done for decades!).
* And I use the terminal feature to trigger a jekyll rebuild and then `surge` to upload my blog and git all in Visual Studio Code's terminal.
* Finally I have another ngrok tunnel running that maps port 4000 to port 80 to see the rendered draft version at: https://rytjekyll.ngrok.io/ (userid: `you` password: `rock+2023` <-- remove the "+" sign :-) ) I am not sure how long this will remain up (at least until mid February 2023) because I not sure I can afford to pay for ngrok but we'll see :-) 
* Super geeky :-) but then I can edit on any of my 3 laptops and 2 Raspberry Pis (including my MacBook Air) because this recipe will work on any computer that runs Visual Studio Code.
* Question: Does Typora or any other nice Markdown editor work over SSH? VS Code is fine but not nearly as nice as Typora! Maybe I should try my perennial favourite emacs's Markdown mode?

### Previously
* January 31, 2023: [How To get ngrok working with SSH on WSL](http://rolandtanglao.com/2023/01/31/p1-ngrok-ssh-wsl-var-run-nogin/)
* February 5, 2020: [Stowe Boyd Building A Zettelkasten (notes that are: atomic, autonomous, linked, explain why, your own words, links to references) In Typora](http://rolandtanglao.com/2020/02/05/p1-stowe-boyd-building-a-zettelkasten-typora/)