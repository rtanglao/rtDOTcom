---
layout: post
title: Using the OS X "find" command and avoiding "not a file" errors
---


## Pontifications

```sh
find . -type f -exec echo {} \; | grep "custom.node-browser"
```

searches for the string ```custom.node-browser``` in files (NOT directories) (not sure why we need the whole ```-exec echo {} \;``` dance (is this an OS X / BSD thing?)!