---
layout: post
title: "To get csvs-to-sqlite to work, hardcode pandas dependency to 1.4.0"
---
* Oct 9, 2023 23:56 UPDATE:
  see https://github.com/simonw/csvs-to-sqlite/issues/88

  ```bash
  pip3 install 'pandas==1.4.0'
  # git clone from this repo and cd to that directory
  pip3 install -e .
  ```
  [Discovered](http://rolandtanglao.com/2020/07/29/p1-blogthis-checkvist-list-links-to-blog/): Nov 2, 2020. [What is the use case for `pip install -e`](https://stackoverflow.com/questions/42609943/what-is-the-use-case-for-pip-install-e) I installed csvs-to-sqlite from simon w by changing pandas dependency to be just `pandas` instead of `pandas~=0.25.0` in [setup.py](https://github.com/simonw/csvs-to-sqlite/blob/master/setup.py)

### Previously

* March 27, 2022: [2021  SUMO Firefox Desktop Support Questions in a SQLite file: 317 questions  on June 4, 2021 about Firefox look and feel changes in Firefox 89 (used  DB Browser for SQLite, csvstack, csvs-to-sqlite)](http://rolandtanglao.com/2022/03/27/p1-firefox-sumo-317-support-questions-2021-june4-firefox89-new-look-and-feel/)        
