---
layout: post
title: "How I used httrack to backup my Wordpress blog barbandroland.com"
---

* [httrack](https://www.httrack.com/) backed up my wordpress blog barbandroland.com in 9 hours! [#Lucky](https://devdilettante.com/tags/Lucky) [#Thanks](https://devdilettante.com/tags/Thanks)! Magic incantation: 
```bash
httrack barbandroland.com -W -O \
"/Users/roland/Documents/BARB_AND_ROLAND_DOT_COM_BACKUPS/HTTRACK_BACKUP/barbandrolandbackup" \
-%v -s0 +www.barbandroland.com/*.jpg
```
where:
*  `-s0` means infinite depth
* ` %v` means  display on screen filenames downloaded (in realtime) (--display)


## Previously

* July 19, 2017: [use curl -O url\[1-455\].jpg to get multiple JPGs from a website and then convert to a PDF with preview](http://rolandtanglao.com/2017/07/19/p1-curl-to-get-multiple-jpgs-from-the-internet-and-convert-to-pdf/)         