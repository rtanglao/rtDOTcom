---
layout: post
title: "Interactive Multiple File Search and Replace using fd aka fdfind and sad instead of sed; use sd for just stdin replacement; also check out diff-so-fancy" 
---

*  tl;dr:  `fdfind . | sad "locale" "localBLAH" --pager 'delta -s'` <-- use `tab` to toggle select, `Y` to execute, `q` to quit without doing anything, affected files are printed to `stdout`

## Details: 

* `fdfind` is `fd` on macOS and other Unix systems. Ubuntu already has an `fd`command so the package is renamed on ubuntu:
  * [https://github.com/sharkdp/fd](https://github.com/sharkdp/fd)

* `sad`:
  * [https://github.com/ms-jpq/sad](https://github.com/ms-jpq/sad)

* The inspiration for `sad` was `sd` ("If you just want to edit the shell stream, I would recommend [`sd`](https://github.com/chmln/sd), it uses the same concept, but its more for in stream edits. `sad` was inspired by my initial usage of `sd`.":
  * [https://github.com/chmln/sd](https://github.com/chmln/sd) <-- Unlike sad, sd is NOT interactive

* Love the diffs from diffs-so-fancy:
  * [https://github.com/so-fancy/diff-so-fancy](https://github.com/so-fancy/diff-so-fancy)

* I have no idea how to use `vertico` in emacs. See "Original Checkvist" below :-)

## Original Checkvist

[Discovered](http://rolandtanglao.com/2020/07/29/p1-blogthis-checkvist-list-links-to-blog/): May 22, 2022 18:48 [Today in Command line Fun for Some Values of Fun™, combine `fzf` and `sad` to switch out your venerable but somewhat perilous sed or perl one-liner that recursively finds & replaces texts in files with a thing with a diff viewer that lets you preview what’s going to happen.](https://twitter.com/kjhealy/status/1528545478127779848) <-- **tl;dr**: `fd "blah*.rb" | sad "old text" "new text" --pager s` --> **QUOTE** from followup tweet: `Side note to @ftrain: yes, OBVIOUSLY one should just do this in Emacs with vertico and C-c s p foo C-; E C-c C-p :%s/foo/bar/g RET Z Z` --> `fdfind` on ubuntu --> `fdfind . | sad "locale" "localBLAH" --pager 'delta -s'` <-- use `tab` to toggle select, `Y` to execute, affected files are printed to `stdout`



### Previously and maybe even related

* April 2017 [sed to print selected lines, cut to get second field, open to open in web browser like Firefox](http://rolandtanglao.com/2017/04/10/p1-open-in-webbrowser-field2-first9lines/)        

