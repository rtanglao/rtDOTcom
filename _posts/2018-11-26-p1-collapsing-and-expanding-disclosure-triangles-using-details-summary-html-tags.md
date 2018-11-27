---
layout: post
title: "HTML tags <details> and <summmary> can be used for expand/collapse with disclosure triangles"
---
## Pontifications

* following up on [Checkvist seems like a great omnioutliner on the web cross platform replacment except for html export which doesn't implement expand and collapse unlike omnioutliner](http://rolandtanglao.com/2018/11/25/p1-checkvist-webapp-for-outlining-good-so-far/):
  * Not sure if this works outside of github, i.e. if i need CSS but the following markdown from [collapsible markdown](https://gist.github.com/joyrexus/16041f2426450e73f5df9391f7f7ae5f) works on github

```md
## collapsible markdown?

<details><summary>CLICK ME</summary>
<p>

#### yes, even hidden code blocks!

```python
print("hello world!")
\`\`\`


</p>
</details>
```
  * sounds like I or somebody else could easily (ha! for some definition of easy!) write a script to take checkvist markdown and convert it to "collapsible html"
  
### Other links with potential clues

* [https://github.com/dear-github/dear-github/issues/166](https://github.com/dear-github/dear-github/issues/166)
* [https://stackoverflow.com/questions/32814161/how-to-make-spoiler-text-in-github-wiki-pages/39920717#39920717](https://stackoverflow.com/questions/32814161/how-to-make-spoiler-text-in-github-wiki-pages/39920717#39920717)
* [https://stackoverflow.com/questions/31562552/collapsible-header-in-markdown-to-html](https://stackoverflow.com/questions/31562552/collapsible-header-in-markdown-to-html)
