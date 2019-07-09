---

layout: post
title: "GNU Parallel replacement string for filename without path and filetype is '{/.}'"
---

# Pontifications

* If you don't want the filepath and you don't want the filetype use ```{/.}``` which is the "Basename of input line without extension." according to the man page.

* example:

```bash
cd /home/roland/GIT/rt-mozlando2018-ksc/264x176
parallel convert {} -resize 264x176! 264x176-{/.}.png ::: ../ORIGINALS/*.jpg    
mkdir MONOCHROME ; cd !$
parallel convert {} -monochrome monochrome-{/.}.gif ::: ../*.png
```

* previous blog posts about parallel:  

  * [Use GNU Parallel instead of xargs to run a script on wildcards and a file that is a list of files](http://rolandtanglao.com/2017/06/15/p1-gnu-parallel-to-run-a-script-on-a-file-with-a-list-files-who-needs-xargs/)

  * [GNU Parallel to use all your CPU cores](http://rolandtanglao.com/2016/09/12/p1-parallel-to-use-all-your-cpu-cores/)