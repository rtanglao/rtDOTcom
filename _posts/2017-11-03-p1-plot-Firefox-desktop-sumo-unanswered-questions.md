---
layout: post
title: "ggplot2 r bar graph of unanswered after 72 hours of Firefox desktop questions"
---

## Pontifications

* 1\. Using the CSV file from [the last blog post, MongoDB query to export Firefox unanswered questions into a CSV file,](http://rolandtanglao.com/2017/11/01/p1-mongodb-query-to-get-firefox-desktop-questions-not-answered-in-72-hours/):

```R
# Plot unanswered after 72 hours Firefox Desktop Questions April-October 2017 by day of week
csv_url = "https://raw.githubusercontent.com/rtanglao/sumo-questions/master/firefox_desktop_only_not_answered_in_72hours_id_created.csv"
unanswered_desktop_april_october_2017 = 
  read_csv(csv_url)
daynumber_of_week_abbrevDayName_hour <-
  unanswered_desktop_april_october_2017 %>% 
  rowwise() %>%
  mutate(daynumber_abbrevDayName = strftime(as.Date(created),'%u-%a',
         tz = "America/Vancouver")) %>% 
  rowwise() %>%
  mutate(hour = strftime(created,'%H',tz = "America/Vancouver"))
p = ggplot(data=daynumber_of_week_abbrevDayName_hour, aes(x=hour)) +
  geom_bar(stat="count")+
  facet_wrap(~ daynumber_abbrevDayName)
```

### Output

<a data-flickr-embed="true"  href="https://www.flickr.com/photos/roland/38067187296/in/dateposted-public/" title="absolute-number-SUMO-unanswered-questions-after72hours-per-hour-per-day"><img src="https://farm5.staticflickr.com/4576/38067187296_9c4050da5d.jpg" width="500" height="500" alt="absolute-number-SUMO-unanswered-questions-after72hours-per-hour-per-day"></a><script async src="//embedr.flickr.com/assets/client-code.js" charset="utf-8"></script>
