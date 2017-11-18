---
layout: post
title: "Everything built on insecure non verified software layers will break at some point because you will be forced to refactor or modify those insecure non verified layers in a non backwards compatible way"
---

## Pontifications

* Following up from [yesterday where the nice analogy was made by Aaron Klotz that WebExtensions are privileged user applications](http://rolandtanglao.com/2017/11/16/p1-Aaron-Klotz-Legacy-extensions-like-kernel-modules/) in Firefox, somebody pointed me to [a great comment from Yogic on Hacker News on fixing things in a large piece of software like Firefox which has a large amount of add-ons built on insecure, unverified software](https://news.ycombinator.com/item?id=15696184) 
    * (tl;dr Everything built on [insecure non verified software layers](http://rolandtanglao.com/2017/03/01/p1-themes-like-uis-are-something-users-unfortunately-cant-really-control-without-secure-reliable-components/) will break at some point because you will be forced to refactor or modify those insecure non verified layers in a non backwards compatible way to make them better perhaps even [secure](http://rolandtanglao.com/2016/12/17/p1-software-is-hard-no-clean-separation-or-componentization/) :-) ! )

**QUOTE**

<blockquote>

Consider the necessary steps:<br /><br />

1. realize that an internal API is broken;<br /><br />

2. come up with a new non-broken API;<br /><br />

3. port all the internal code using the non-broken API;<br /><br />

4. add a compatibility layer between the broken API and the non-broken API;<br /><br />

5. check all the existing add-ons to find out which ones use the broken API;<br /><br />

6. hope you didn't forget any add-on;<br /><br />

7. attempt to get in touch with all the add-on developers;<br /><br />

8. repeat 7. many, many times, until you are sure that the add-on developers that do not respond have simply abandoned their add-on;<br /><br />

9. negotiate a transition plan with the add-on developer with whom you have managed to get in touch;<br /><br />

10. land the patch that you have written now 3-4 months ago;<br /><br />

11. maintain both the broken API and the non-broken API (and their tests) for ~1 year, until you are reasonably sure that all add-on developers who intend to migrate have done so;<br /><br />

12. maintain (and test) a downgrade path for people who switch between versions of Firefox;<br /><br />

13. finally land your code;<br /><br />

14. realize that you still have accidentally broken some add-ons and people are (rightfully) unhappy because "Firefox broke my add-on";<br /><br />

15. it's 18 months since you wrote your 2-lines patch, you can finally get rid of the dead code and tests and move to something else.<br /><br />

</blockquote>

**END QUOTE**

[Read the whole thing](https://news.ycombinator.com/item?id=15696184)!