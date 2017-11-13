---
layout: post
title: "Longterm Future of support at Mozilla? My ideas: easier markup, support from within mobile products, easier L10N, interactive chat"
---

## Pontifications

* **DISCLAIMER: These are just my personal thoughts, not future directions or even future research or even anywhere close to being fully fleshed out or committed and I don't speak for my Mozilla team or any other Mozilla team, I just wanted to get these out of my head**.
* [SUMO knowledge base markup](https://support.mozilla.org/en-US/kb/markup-cheat-sheet) seems ridiculously complicated.  Can we not simplify it? It is intimidating to have to grok [showfor](https://support.mozilla.org/en-US/kb/how-to-use-for) and all the other markup if you don't have a technical writer background. Can we not have for example different versions of the article instead of using ```showfor```? We are only supposed to support the last version and the last ESR of Firefox yet somehow we have markup from many other Firefox versions because overtime you end up having nested ```showoff``` which is a mess to maintain.
* Screenshots seem cumbersome and complicated as well. Can we not automate it for various languages?
* Tokenized L10N - Use strings aka "tokens" instead of markup to simplify localization and so we can use Pontoon. Or enhance Pontoon to handle article style localization.
* I believe folks should be able to ask support questions from Firefox via REST API from within Firefox (especially Mozilla's mobile products like Firefox Focus, Firefox for iOS and Firefox for Android) and other Mozilla products without launching the full site e.g. using Geckoview
* Interactive chat support would be great too. Not some crazy separate centralized chat server. But maybe peer to peer distributed? Is there not some way to do this with vetted volunteers 'office hours' who are available say for 30 minutes a week  in their time zones? Maybe book office hours inside the product itself for support?
* It would be great if volunteers could see who needs help on the support forum and in App Store reviews on Google Play and Apple's iOS Store, and external popular sites like Super User and Reddit and Campfirefox and geckozone. Some sort of dashboard for Mozilla support no matter where it happens on the Internet?
* It seems our support is behind the times when it comes to video. How can we keep the existing text and screenshot based KB articles but also add video on a timely basis?!? I don't know. I do know a non wordy, concise, helpful video takes a lot more work than text based documentation.
* All of the above are half baked :-) I should start from the user stories, right?