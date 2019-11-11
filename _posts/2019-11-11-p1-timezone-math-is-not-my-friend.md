---

layout: post
title: "Timezone math is not my friend :-)"
---

# Pontifications

* See the current version of [get-creator-answers-questions-for-arbitrary-time-period.rb](https://github.com/rtanglao/rt-kits-api2/blob/master/get-creator-answers-questions-for-arbitrary-time-period.rb) namely:

```ruby
    logger.debug "created from API:" + q["created"] + "<-- this is PST not UTC despite the 'Z'"
    # All times returned by the API are in PST not PDT and not UTC
    # All URL parameters for time are also in PST not UTC
    # See https://github.com/mozilla/kitsune/issues/3961 and
    # https://github.com/mozilla/kitsune/issues/3946
    # The above may change in the future if we migrate the Kitsune database to UTC
    created = Time.parse(q["created"].gsub("Z", "PST")) 
```

* and the associated issues, [3961](https://github.com/mozilla/kitsune/issues/3961) and [3946](https://github.com/mozilla/kitsune/issues/3946)

* And for posterity's sake :-) here's the current way to use  the Kitsune API (all of my other scripts that use the API are currently broken; maybe someday I'll fix them :-)  <--- this may change if we find the time to make Kitsune all UTC):

  ```bash
  cd /home/rtanglao/GIT/rt-kits-api2/201911
  ../get-creator-answers-questions-for-arbitrary-time-period.rb 2019 11 10 \
  2019 11 10
  ../print-desktop-en-us-all-oses-increasing-ids-time-url-title-content.rb \
  2019-11-10-2019-11-10-firefox-creator-answers-desktop-all-locales.csv markdown
  ```

  
