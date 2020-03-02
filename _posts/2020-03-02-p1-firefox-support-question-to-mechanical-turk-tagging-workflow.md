---
layout: post
title: "Firefox Support Question to CSV for tagging by Mechanical Turk Workflow"
---

# Pontifications

* 1\. figure out which Firefox question ids you want to use perhaps using the linux `shuf` command to get random ids and put them in a file e.g. `mturk-question-ids.txt`

* 2\.  get the content and title for those ids

* ```bash
  cat mturk-question-ids.txt | ./get-by-id-creator-answers-questions.rb
  ```

  which outputs sample file of the form `id-<first-id>-unixtime-<unixtime i.e. int-when-created>.csv`:

  e.g. [id-1279731-unixtime-1583100833-by-id-firefox-creator-answers-desktop-all-locales.csv](https://github.com/rtanglao/rt-kits-api2/blob/master/id-1279731-unixtime-1583100833-by-id-firefox-creator-answers-desktop-all-locales.csv) 

  which still has HTML in the content field (see the `<p>` tag in the following csv file output)
  
  ```bash
  mlr --csv cut -f title,content id-1279731-unixtime-1583100833-by-id-firefox-creator-answers-desktop-all-locales.csv 
  title,content
  Restore session doesn't work after update,"<p>I have a very high tab count, and when restoring Firefox I usually get the ""warning:unresponsive script"" pop up. I press continue, it pops up again, I press continue again, and my tabs are restored. All is well.
  However, when I restarted Firefox today, it updated, and rather than the unresponsive script box, I get a blank pop up. I cannot do anything, and my tabs cannot be restored.
  I tried a refresh and a clean install, but that does nothing.
  </p>"
  ````
  
* 3\. remove all the fields except title and content and parse out any HTML and create a CSV file with just title and content 

* ```bash
  ./print-all-questions-just-title-content.rb \
  id-1279731-unixtime-1583100833-by-id-firefox-creator-answers-desktop-all-locales.csv 
  ```

  which outputs a parsed csv file of form `title-parsed-content-<csv-filename>` 

  [title-parsed-content-id-1279731-unixtime-1583100833-by-id-firefox-creator-answers-desktop-all-locales.csv](https://github.com/rtanglao/rt-kits-api2/blob/master/title-parsed-content-id-1279731-unixtime-1583100833-by-id-firefox-creator-answers-desktop-all-locales.csv)
  :

  ```csv
  title,content
  Restore session doesn't work after update,"I have a very high tab count, and when restoring Firefox I usually get the ""warning:unresponsive script"" pop up. I press continue, it pops up again, I press continue again, and my tabs are restored. All is well.
  However, when I restarted Firefox today, it updated, and rather than the unresponsive script box, I get a blank pop up. I cannot do anything, and my tabs cannot be restored.
  I tried a refresh and a clean install, but that does nothing.
  "
  ```