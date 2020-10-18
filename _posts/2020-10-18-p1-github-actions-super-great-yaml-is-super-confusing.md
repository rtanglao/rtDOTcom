---
layout: post
title: "Github Actions are super powerful and yaml is super confusing"
---
*   (refer to my previous post: [Simon Willison:Git scraping: track changes over  time by scraping to a Git repository aka how to use github actions to  call an API every 20 minutes](http://rolandtanglao.com/2020/10/16/p1-simon-willison-git-scraping-how-to-use-github-actions-to-call-an-api-every-20-minutes/))
*   I want to read Firefox Desktop support questions every 15 minutes roughly so I can generate infographics every hour. To do this:
    *   I modified my trusty [get-creator-answers-questions-for-arbitrary-time-period.rb](https://github.com/rtanglao/rt-kits-api3/blob/main/get-creator-answers-questions-for-arbitrary-time-period.rb)  (compare with api2's [get-creator-answers-questions-for-arbitrary-time-period.rb](https://github.com/rtanglao/rt-kits-api2/blob/master/get-creator-answers-questions-for-arbitrary-time-period.rb) ) as follows:
        *   `awesome_print` is no longer maintained but there is a fork called `amazing_print` which I switched to.
        *   Fixed two long standing bugs that I just discovered : 1. [Kitsune issue 3686](https://github.com/mozilla/kitsune/issues/3686) didn't work for both PST and PDT so I wrote `KludgeTimeFromBogusZtoUTC(pst_in_utc_str)` 2. `updated` was wrongly using the uncorrected time!
    *   Created a github action, [getffquestions.yml](https://github.com/rtanglao/rt-kits-api3/blob/main/.github/workflows/getffquestions.yml) to run `get-creator-answers-questions-for-arbitrary-time-period.rb` every 15 minutes and create a CSV file using Ruby 2.7
*   In the process I found out that like Heroku in 2007 :-), you can create servers at will with Github actions and those servers can basically run anything on Windows, Mac or Linux!
*   I also learned that I dislike YAML :-) Too loosey goosey! For a good time try and figure out what ```|-``` means. This is just one of the many things that are vexing!
*   Next thing to do: create a second github action to create infographics using R or Ruby every hour

