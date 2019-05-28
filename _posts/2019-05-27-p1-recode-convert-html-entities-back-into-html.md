---
layout: post
title: "recode is a handy linux command line utility to convert text with html escaped entites like & lt to <"
---

# Pontifications

* See [recode github](https://github.com/rrthomas/recode/) site! And [a recode question on stack overflow](https://stackoverflow.com/questions/5929492/bash-script-to-convert-from-html-entities-to-characters) where i learned the following incantation :-)

```bash
cat try2-2116-27may2019-test-api-stdout.txt | \
recode html..ascii  > try2-2116-27may2019-test-api-stdout.html
