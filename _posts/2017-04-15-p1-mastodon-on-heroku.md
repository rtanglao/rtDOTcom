---
layout: post
title: How to deploy mastodon on heroku - use the deploy button?!?
---

## Pontifications

* I still don't understand Heroku's pricing model.
* [Official docs which state you can't do reply mastodon  on free dynos](https://github.com/tootsuite/documentation/blob/master/Running-Mastodon/Heroku-guide.md): ```Running on Heroku's hobby Dynos and free add-on tiers has limited testing purposes and is not recommended in production. ```
* [Boris: Notes on running your own Mastodon instance on Heroku](https://medium.bmannconsulting.com/notes-on-running-your-own-mastodon-instance-on-heroku-864cf5949d21) based on [Ash Furrow's Running Mastodon on Heroku](https://ashfurrow.com/blog/running-mastodon-on-heroku/)
* [The toot from Boris](https://mastodon.frontierfoundry.co/@boris/3):
```
@rtanglao Answering your question from FB ;) The Heroku guide on the Mastodon site is very high level and not step by step. There is a bunch of setup that needs to be done with Mailgun - DNS, MX records, Mailgun verification and Mastodon + Heroku config. Start with the "Deploy to Heroku" and go from there. Likely best done as an "install fest" with a group of us.
```