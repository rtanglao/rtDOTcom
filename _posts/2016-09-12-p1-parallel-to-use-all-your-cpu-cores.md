---
layout: post
title: GNU Parallel to use all your CPU cores
---

## GNU Parallel is good stuff

```parallel convert -trim '{}' 'TRIMMED/{}' ::: *.png```

I think this default "don't forget to cite" message is hilarious but anyhow [I am happy to cite the GNU parallel Usenix paper aka O. Tange (2011): GNU Parallel - The Command-Line Power Tool,;login: The USENIX Magazine, February 2011:42-47.](https://www.usenix.org/system/files/login/articles/105438-Tange.pdf) :-)! :

```
Academic tradition requires you to cite works you base your article on.
When using programs that use GNU Parallel to process data for publication
please cite:

  O. Tange (2011): GNU Parallel - The Command-Line Power Tool,
  ;login: The USENIX Magazine, February 2011:42-47.

This helps funding further development; AND IT WON'T COST YOU A CENT.
If you pay 10000 EUR you should feel free to use GNU Parallel without citing.

To silence the citation notice: run 'parallel --citation'.
```




