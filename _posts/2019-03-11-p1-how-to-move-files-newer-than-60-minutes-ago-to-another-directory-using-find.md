---
layout: post
title: "How to move files newer than 60 minutes ago to another directory"
---

# Pontifications

* See [Move files to another directory which are older than a date](https://serverfault.com/questions/505949/move-files-to-another-directory-which-are-older-than-a-date)

```bash
find .  -maxdepth 1 -mmin -60 -name '*.jpg' -exec mv "{}" ../NEON2_ORIGINALS \;
```