---
layout: post
title: "How to get links to images and audio files using wget on a Wordpress blog: barbandroland.com aka a tale of trial and error and httrack was better in this case :-)"
---
* tl;dr: `httrack` appeared to get 200 more images and do a full backup so I abandoned `wget` and used it instead see the previous post: [How I used httrack to backup my Wordpress blog barbandroland.com](http://rolandtanglao.com/2024/04/29/p1-backup-wordpress-blog-httrack/)        
* 1\. from [mastodon on devdilettante.com](https://devdilettante.com/@roland/112341446232283984)
```bash
wget --execute="robots = off" --spider --force-html -r -l 0 \
$url 2>&1  | grep -e '^--'  | \
grep -e '\.\(jpeg\|mp3\|png\|gif\|jpg\) \
2>stderr_mp3_jpg_png_urls.txt \
>_level_0_mp3_jpg_png_urls.txt
```
* The above command line snippet appears to get a list of URLs from a WordPress (or any?) website (via https://stackoverflow.com/questions/2804467/spider-a-website-and-return-urls-only )

* 2\. the two spaces throws off awk so remove one of the spaces and proceed :-)
```bash
cat _level_0_mp3_jpg_png_urls.txt | \
sed "s/--  / /g" | awk '{ print $3 }' \
| grep _photos `
```
* 3\. Get the photos
```bash
`cat _level_0_mp3_jpg_png_urls.txt | \
sed "s/--  / /g" | awk '{ print $3 }' | \
grep _photos | > photo_urls.txt ; \
mkdir PHOTOS; cd !$ ; cat ../photo_urls.txt | \
xargs -n 1 wget `
```
* 4\. replace `'` with '`'` to keep bash and wget happy :-) (first `'` occurs at line 410
```bash
tail --lines=+411 ../photo_urls.txt| xargs -n 1 wget
```
* 5\. of course that leads to the next layer of the onion :-)
```
--2024-04-27 08:31:40--  http://www.barbandroland.com/_photos/Thu,%20Jul%2029,%202004%2006:30:16%20PM.jpg
Resolving www.barbandroland.com (www.barbandroland.com)... 64.91.252.138
Connecting to www.barbandroland.com (www.barbandroland.com)|64.91.252.138|:80... connected.
HTTP request sent, awaiting response... 404 Not Found
2024-04-27 08:31:41 ERROR 404: Not Found. <-- what is wrong wtih the URL? do commas need to be URL encoded?
```
* 6\. Ultimately this led to a dead-end. `httrack` appeared to get 200 more images and do a full backup so I abandoned `wget`

## Previously

* April 29, 2024:  [How I used httrack to backup my Wordpress blog barbandroland.com](http://rolandtanglao.com/2024/04/29/p1-backup-wordpress-blog-httrack/)        