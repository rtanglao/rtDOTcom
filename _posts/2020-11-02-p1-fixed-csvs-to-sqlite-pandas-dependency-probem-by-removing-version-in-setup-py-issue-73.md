---
layout: post
title: "csvs-to-sqlite, outdated pandas dependency in setup.py? issue 73"
---

* Please refer to previous post: [Create a SQLite database from a kitsune question CSV file](http://rolandtanglao.com/2020/05/18/p1-kitsune-questions-csv-to-sqlite/)        
* From [What is the use case for `pip install -e`](https://stackoverflow.com/questions/42609943/what-is-the-use-case-for-pip-install-e) I successfully installed [csvs-to-sqlite](https://github.com/simonw/csvs-to-sqlite) from Simon Willison by changing the pandas dependency to be just `pandas` instead of `pandas~=0.25.0` in [setup.py](https://github.com/simonw/csvs-to-sqlite/blob/master/setup.py) as follows:
  * from github, download the latest tar file of csvs-to-sqlite and untar it
  * edit setup.py to remove the pandas version
  * cd to the directory with the unzipped tar file
  * `pip install -e .`
  * And presto it installed and seems to work!
* I filed issue 73 for this: [outdated pandas dependency in setup.py? #73](https://github.com/simonw/csvs-to-sqlite/issues/73)
