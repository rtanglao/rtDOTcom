---
layout: post
title: "Tailscale Funnel is a reverse proxy service complete with TLS cert, DNS, public IP address and HTTPS server that seems perfect for small, experimental software on the internet like snac2"
---
* [Discovered](http://rolandtanglao.com/2020/07/29/p1-blogthis-checkvist-list-links-to-blog/): Dec 9, 2022 16:57 [Introducing Tailscale Funnel · Tailscale](https://tailscale.com/blog/introducing-tailscale-funnel/) <-- OMG perfect, thanks! Now I really have to try Tailscale so I run experiments on localhost:randomport with a real cert and public address!!!!!!!!!! Thanks again! <-- QUOTE: `The second thing you can do is have your device’s Tailscale daemon itself terminate TLS. Then it can reverse proxy the HTTP requests to a local non-HTTPS webserver. That is, you run a webserver on localhost:8080 and we put it on the internet, complete with a public IP address, DNS, TLS cert, and HTTPS server. Now that’s a fun tunnel, if we do say so ourselves.`
* Perfect for trying out something like [snac2](https://codeberg.org/grunfink/snac2)? (fab ActivityPub server in C) so I can learn enough to re-implement it in a "better" :-)  language like Haskell or Rust?!?

### Previously

* April 2, 2020 [recent iPad + Airpods + mount = best combo for Zoom? <- From Several grumpy opinions about remote work at Tailscale](http://rolandtanglao.com/2020/04/02/p1-best-zoom-device-airpods-recent-ipad-remote-work-advice-tailscale/)
