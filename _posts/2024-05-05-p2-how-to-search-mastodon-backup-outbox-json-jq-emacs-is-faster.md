---
layout: post
title: "How to find old threads in outbox.json from your Mastodon archive using jq (lo-tech solution is better again i.e. always faster to edit and search using emacs or visual code)"
---
* UPDATE 2: how output a json file! output is in [filtered_id_content.json](https://github.com/rtanglao/devdilettante-backups/blob/main/2024-05-04-devdilettante-com-archive-20240505032936-7d3110aafe1a03f80e3db147600edd38/filtered_id_content.json)

  ```bash
  cd 2024-05-04-devdilettante-com-archive-20240505032936-7d3110aafe1a03f80e3db147600edd38/
  jq '.orderedItems | .[]  | {id: .object.id? | select (. !=null), content: .object.content? | select(. != null)}' outbox.json > filtered_id_content.json
```
* UPDATE1: how to display the `id` field so you can see the link to the toot:
```bash
jq '.orderedItems | .[]  | .object.id + " " + .object.content? | select(. != null)' /Users/roland/Documents/DEV_DILETTANTE_COM_MASTODON_BACKUPS/2024-05-04-devdilettante-com-archive-20240505032936-7d3110aafe1a03f80e3db147600edd38/outbox.json | grep wget
```
* which results in:
```
"https://devdilettante.com/users/roland/statuses/112341435858857502 <p>`wget --execute=&quot;robots = off&quot; --spider --force-html -r -l 0 $url 2&gt;&amp;1  | grep -e &#39;^--&#39;  | grep -e &#39;\\.\\(jpeg\\|mp3\\|png\\|gif\\|jpg\\) 2&gt;stderr_mp3_jpg_png_urls.txt&gt;_level_0_mp3_jpg_png_urls.txt` appears to get a list of URLs from a WordPress (or any?) website (via <a href=\"https://stackoverflow.com/questions/2804467/spider-a-website-and-return-urls-only\" target=\"_blank\" rel=\"nofollow noopener noreferrer\" translate=\"no\"><span class=\"invisible\">https://</span><span class=\"ellipsis\">stackoverflow.com/questions/28</span><span class=\"invisible\">04467/spider-a-website-and-return-urls-only</span></a> )</p>"
"https://devdilettante.com/users/roland/statuses/112343480523962150 <p>`cat _level_0_mp3_jpg_png_urls.txt | sed &quot;s/--  / /g&quot; | awk &#39;{ print $3 }&#39; | grep _photos | &gt; photo_urls.txt ; mkdir PHOTOS; cd !$ ; cat ../photo_urls.txt | xargs -n 1 wget `</p>"
"https://devdilettante.com/users/roland/statuses/112343502318371811 <p>replace `&#39;` with &#39;`&#39;` to keep bash and wget happy :-) (first `&#39;` occurs at line 410</p>"
"https://devdilettante.com/users/roland/statuses/112343520971736534 <p>`tail --lines=+411 ../photo_urls.txt| xargs -n 1 wget`</p>"
"https://devdilettante.com/users/roland/statuses/112346164952219195 <p>I will work on potential issue with commas and colons after i see how well httrack works.<br />Seems to be much better than wget.<br />Here&#39;s the magic :-) incantation:<br />`httrack <a href=\"http://www.barbandroland.com\" target=\"_blank\" rel=\"nofollow noopener noreferrer\" translate=\"no\"><span class=\"invisible\">http://www.</span><span class=\"\">barbandroland.com</span><span class=\"invisible\"></span></a> -W -O &quot;/Users/roland/Documents/BARB_AND_ROLAND_DOT_COM_BACKUPS/HTTRACK_BACKUP/barbandrolandbackup&quot; -%v -s0 +www.barbandroland.com/*.jpg`</p>"
```
* From [mastodon](https://devdilettante.com/deck/@roland/112389955186296998):  i couldn't find my `wget` thread from April 26th so I searched my Mastodon archive as follows to get it :-) : 

```bash
jq '.orderedItems | .[]  | .object.content? | \
select(. != null)'  \
/Users/roland/Documents/DEV_DILETTANTE_COM_MASTODON_BACKUPS/2024-05-04-devdilettante-com-archive-20240505032936-7d3110aafe1a03f80e3db147600edd38/outbox.json \
| grep wget
```
* so much yakshaving. it was actually faster to figure this out using Visual Code or emacs :-) on `outbox.json` and searching for `wget` but `jq` is a fun challenge for some value of `fun` :-) ?!?!?
* the aforementioned thread from April 2026, 2024  is here:
[https://devdilettante.com/@roland/112341435858857502](https://devdilettante.com/@roland/112341435858857502)

## Previously

* June 20, 2017: [How to minify JSON using jq](http://rolandtanglao.com/2017/06/20/p1-using-jq-to-minify-json/)        