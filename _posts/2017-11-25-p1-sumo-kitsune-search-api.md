---
layout: post
title: "SUMO aka support.mozilla.org Kitsune search api"
---

## Pontifications

* [Unofficial Search API for support.mozilla.org's Kitsune platform](http://kitsune.readthedocs.io/en/latest/api.html)   that may go away at any day :-) to search for the word videos

```bash
curl -i "https://support.mozilla.org/api/2/search/suggest/"      -H "Content-Type: application/json"      -d '
{
   "q": "videos",
   "max_documents": 3,
   "max_questions": 0
}'
```

* response from server is:

```
HTTP/1.1 200 OK
Server: Apache
X-Backend-Server: support4.webapp.phx1.mozilla.com
Vary: X-Mobile,User-Agent
Cache-Control: no-cache, must-revalidate
Content-Type: application/json
Strict-Transport-Security: max-age=31536000
Public-Key-Pins: max-age=1296000; pin-sha256="r/mIkG3eEpVdm+u/ko/cwxzOMo1bk4TyHIlByibiA5E="; pin-sha256="WoiWRyIOVNa9ihaBciRSC7XHjliYS9VwUGOIud4PB18=";
Date: Wed, 22 Nov 2017 23:07:54 GMT
Expires: Thu, 19 Nov 1981 08:52:00 GMT
X-XSS-Protection: 1; mode=block
Pragma: no-cache
Transfer-Encoding: chunked
X-Content-Type-Options: nosniff
X-Robots-Tag: noodp
Set-Cookie: multidb_pin_writes=y; expires=Wed, 22-Nov-2017 23:08:09 GMT; httponly; Max-Age=15; Path=/
Allow: POST, OPTIONS, GET
X-Frame-Options: DENY
X-Cache-Info: not cacheable; request wasn't a GET or HEAD

{"documents":[{"id":15114,"title":"Download music, photos and videos","slug":"download-music-photos-and-videos","url":"/en-US/
...
```
etc

