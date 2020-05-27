---
layout: post
title: "HowTo: Open a random 25% of support questions using shuf and awk and wsl-open" 
---

# Pontifications

* Here's how to open a random 25% of support questions using `shuf` and `awk` and `wsl-open`

```bash
grep -o 'https*://support.mozilla.org/questions/[^)]*' \
super-long-file-name-of-firefox-desktop-support-questions.md\
| shuf | awk 'NR % 4 == 0' | xargs -n 1 wsl-open
```
* `super-long-file-name-of-firefox-desktop-support-questions.md` is:`sorted-all-desktop-en-us-2020-05-26-2020-05-26-firefox-creator-answers-desktop-all-locales.md`
* `grep -o` just return the matching text
* `https*://support.mozilla.org/questions/[^)]*` since we're matching markdown links match until you encounter a `)`
* `%4 == 0` every 4th, isn't awk wonderful :-) ?
* `xargs -n 1` run the next command which in this case is `wsl-open` with 1 argument at a time