---
layout: post
title: "How to use cURL to send HTML email with Gmail | Change(b)log"
---

* [Discovered](http://rolandtanglao.com/2020/07/29/p1-blogthis-checkvist-list-links-to-blog/) Mar 19, 2024 07:02 [How to use cURL to send HTML email with Gmail | Change(b)log](https://zgadzaj.com/development/how-to/use-curl-to-send-html-email-with-gmail) <-- suitable for a github action --> **QUOTE**: `curl --ssl-reqd \
  --url 'smtps://smtp.gmail.com:465' \
  --user 'username@gmail.com:password' \
  --mail-from 'username@gmail.com' \
  --mail-rcpt 'john@example.com' \
  --upload-file mail.txt`

## Previously
* January 9, 2021: [Thanks to Jenny Bryan's gmailr tutorial, got emailing of my 3 week Firefox anti-virus mention graph working but flickr ignores the body](http://rolandtanglao.com/2019/01/09/p1-gmailr-jenny-bryan-tutorial-flickr-ignores-body/)
