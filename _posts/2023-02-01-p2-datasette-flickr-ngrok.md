---
layout: post
title: "How I use ngrok to put datasette for my flickr 2020 photo metadata on the internet"
---
*  This is even more straightforward than using `ngrok` for SSH :-) ! 
```bash
datasette granian roland-flickr-2020.db
# And then in another terminal tab:
ngrok http 8001 --subdomain ryt-ds-flickr \
--basic-auth="someuserid:somepassword"
```
* Here's the url for those who want to check it out: <https://ryt-ds-flickr.ngrok.io/> (userid: `datasette` password: `rocks+2023` <-- remove the "+" sign :-) ) 
* NB: I am not sure how long this will remain up (at least until mid February 2023) because I am not sure I can afford to pay for ngrok but we’ll see :-)

### Previously
* February 1, 2023: [How I use ngrok over SSH on my MacBook Air to edit my blog on my Surface Book 2](http://rolandtanglao.com/2023/02/01/p1-ngrok-ssh-surfacebook2-edit-blog/)
* May 15, 2022: [City of Vancouver accident data on Datasette lite at lite.datasette.io](http://rolandtanglao.com/2022/05/15/p1-city-vancouverbc-accident-data-datasette-lite/)