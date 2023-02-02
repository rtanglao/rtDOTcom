---
layout: post
title: "How I use ngrok to put datasette for my flickr 2020 photo metadata on the internet"
---
*  This is even more straightforward than using `ngrok` for SSH :-) ! 
```bash
ngrok http 8001 --subdomain ryt-ds-flickr \
--basic-auth="someuserid:somepassword"
```
(userid: `datasette` password: `rocks+2023` <-- remove the "+" sign :-) ) 

### Previously
* February 1, 2023: [How I use ngrok over SSH on my MacBook Air to edit my blog on my Surface Book 2](http://rolandtanglao.com/2023/02/01/p1-ngrok-ssh-surfacebook2-edit-blog/)
* May 15, 2022: [City of Vancouver accident data on Datasette lite at lite.datasette.io](http://rolandtanglao.com/2022/05/15/p1-city-vancouverbc-accident-data-datasette-lite/)