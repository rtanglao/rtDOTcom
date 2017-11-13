---
layout: post
title: Publishing to gh-pages from Travis CI using ssh deploy keys, good for GitBook!
---

## Pontifications

* In[ Publishing to gh-pages from Travis CI](https://soledadpenades.com/2017/06/29/publishing-to-gh-pages-from-travis-ci/) the fab Sole writes (I need to write a book in [Gitbook](https://www.gitbook.com/) using this :-), right?!?!!) :

**QUOTE**

<blockquote>

"<br />
Good news: there are SSH deploy keys. They work very similarly to GitHub’s SSH keys per user, but they will be valid for only that repository… which means that people that get access to the token do not get immediate access to all of your other repositories. And they are indeed finely grained, compared to the personal access token.<br /><br />

I learnt all of this from this fantastic gist by Domenic Denicola (and many commenters). I didn’t want to copy and paste and edit his script though, I wanted a better way that didn’t involve me going back to the gist each time I wanted to set up a project like this. Luckily someone had had the same idea and had written the gh-pages-travis npm module.<br /><br />

With that and my newly acquired understanding of what was going on, I managed to set up my automatically published to gh-pages repository, imaginatively named publish-and-cron.<br /><br />

If you want to do the same thing, you could use this as a skeleton repo. Instead of just generating an index.html in output, you could generate your entire static blog there, or any other thing that you want to publish from source code. There is still a bit of set up involved, as creating the keys and all that is not automated, but the basic pieces are in place. Instructions for creating the keys and the rest are all in the README, I’m not going to replicate them here O:-)<br /><br />

We’re using this for the new Firefox Developer Tools technical docs, which are written in Markdown and rendered with GitBook.<br />
"<br />

</blockquote>

**END QUOTE**