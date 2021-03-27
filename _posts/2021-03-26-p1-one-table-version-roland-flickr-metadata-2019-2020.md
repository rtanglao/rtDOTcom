---
layout: post
title: "My 2019 and 2020 flickr metadata: How To make a 1 table SQLite version"
---

See: [My 2019 and 2020 flickr data now available as a 2 table SQLite database. Next step:datasette real soon now :-)](http://rolandtanglao.com/2021/03/24/p1-roland-flickr-metadata-2019-2020-sqlite/)

```bash
cp 2019-roland-flickr-metadata.csv 2020-and-2019-roland-flickr-metadata.csv
tail -n +2 2020-roland-flickr-metadata.csv >> 2020-and-2019-roland-flickr-metadata.csv
csvs-to-sqlite 2020-and-2019-roland-flickr-metadata.csv -dt datetaken -dt dateupload\
-dt lastupdate one-table-roland2019-2020.db
```

* Then upload to dropbox or some other cloud storage because github doesn't like files larger than 50MB (the SQlite file is over 60MB)