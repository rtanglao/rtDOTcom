---
layout: post
title: "Thanks to Jenny Bryan's gmailr tutorial, got emailing of my 3 week Firefox anti-virus mention graph working but flickr ignores the body"
---
# Pontifications

* Thanks to [Jenny Bryan's tutorial](https://github.com/jennybc/send-email-with-r) got gmailr working.
* Now my code, [plot-antivirus-mentions-by-3weeks.r](https://github.com/rtanglao/rt-kitsune-api/blob/master/VISUALIZATIONS/plot-antivirus-mentions-by-3weeks.r), emails images to flickr!
* Flickr appears to ignore my body text though dang!
* Here's how to invoke it:

```bash
Rscript ./plot-antivirus-mentions-by-3weeks.r FF61 2018 6 26 FF62 2018 9 5 yes
```

* and here's the output:

<a data-flickr-embed="true"  href="https://www.flickr.com/photos/roland/31743070337/in/datetaken-ff/" title="FF Desktop Antivirus 3 weeks antivirus-3weeks-FF61-2018-6-26-FF62-2018-9-5"><img src="https://farm5.staticflickr.com/4826/31743070337_1a4f9d214c.jpg" width="500" height="500" alt="FF Desktop Antivirus 3 weeks antivirus-3weeks-FF61-2018-6-26-FF62-2018-9-5"></a><script async src="//embedr.flickr.com/assets/client-code.js" charset="utf-8"></script>