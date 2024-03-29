---
layout: post
title: "WIP: q, xsv, graphext, dirtylittlesql, Tools for handling large CSV files from Simon Willison's mega replied to thread; CSV the universal data structure"
---
### Probably wrong thought :-)

[CSV is the universal data structure. Excel, Google Sheets & all those tools mentioned allow EVERYBODY  of all skill levels, software developers or not, to do what they want from simple analysis to full on visualization which is super great! #ProgrammingAndDataScienceForEveryBodyhttps://twitter.com/hashtag/ProgrammingAndDataScienceForEveryBody](https://twitter.com/rtanglao/status/1572659730111401989)

### CSV Tools Summary Table

* New to me :-) CSV Tools (except for [Tad which was documented yesterday](http://rolandtanglao.com/2022/09/20/p1-tad-fast-viewer-csv-parquet-sqlite-datasette-alternative/)) from the 1000 replies to Simon Willison's tweet: [If someone gives you a CSV file with 100,000 rows in it, what tools do you use to start exploring and understanding that data?](https://twitter.com/simonw/status/1572285367382061057)

* The github Markdown tables are much nicer! Until I get github flavoured markdown working here, check out [the tables in github](https://github.com/rtanglao/rtDOTcom/blob/master/_posts/2022-09-21-p1-tools-for-large-csv-files-simon-willison.md) which have thin lines around the table cells as they should!

  | Name                            | Tweet                                                        | Type                        | Notes                                                        |
  | ------------------------------- | ------------------------------------------------------------ | --------------------------- | ------------------------------------------------------------ |
  | Postgres                        | [[1]](https://twitter.com/fuzzychef/status/1572389081472208896), [[2]](https://twitter.com/fuzzychef/status/1572428556126556162) | Database                    | * Use COPY command, CSV data wrapper which lets you do CSV operations without even copying them which is good for folders<br /> |
  | awk, cut,  wc, grep, args,  etc | [[1](https://twitter.com/adambroach/status/1572512127629561856)] | classic Unix CLI text tools | * xargs & many classic tools don't work with embedded commas e.g. `1, "1,2,3", 2`<br /> * They also don't work with unicode and other non classic ASCII characters |
  | q                               |                                                              |                             |                                                              |
  | Tableau                         | [[1](https://twitter.com/rajko_rad/status/1572346412091969538)] | proprietary                 | * for plotting                                               |
  | xsv                             | [[1](https://twitter.com/dancow/status/1572286228371841026)] | cli tool                    | * `xsv and csvkit, to get a sense of the size and cardinality and consistency of the data before I bother opening it up in Excel or sqlite` |
  | csvkit                          |                                                              |                             |                                                              |
  | pandas in Python                | [[1](https://twitter.com/gusthema/status/1572318946115592195)] |                             | * [thread from Gus about a 5.7GB CSV file](https://twitter.com/gusthema/status/1456607188277936132) (read_csv in batches) |
  | visidata                        |                                                              |                             |                                                              |
  | dirtylittlesql                  |                                                              |                             |                                                              |
  | graphex                         |                                                              |                             |                                                              |
  | Julia and Duck                         |                                                              |                             |                                                              |
  | MySQL and phpMyAdmin | [[1](https://twitter.com/iamcal/status/1572332519927980034)] | | * from Carl Henderson who of course knows MySQL and PHP from flickr and many other things :-) |
  | Excel, Access, etc |  | | * Of course, not going to give any further details for these proprietary tools, left as an exercise to the reader :-) |
  | Spotfire, Tableau and other BI Tools | [[1](https://twitter.com/kimahlberg/status/1572330670374129667)] | | * Again not likely to use these tools :-) |
  | dask for Python | [[1](https://twitter.com/jc50000000/status/1572369962500587520)] | python library | * `How are there no mentions of dask? Like pandas but not shitty. Loads the data in chunks, doesn’t have to load it all into memory. Dask is the answer for all of them. [https://docs.dask.org/en/stable/](https://t.co/qB6GthUdco) If I can’t use python then redis on a high mem ec2 instance to do what i need and shutdown` |

### Programming language and other small code snippets

| Language/Tool                     | Tweet                                                        | Snippet                                                      | Notes |
| --------------------------------- | ------------------------------------------------------------ | ------------------------------------------------------------ | ----- |
| Datasette on Mac / CLI on Windows | [#](https://twitter.com/simonw/status/1572295332767371265)   | `sqlite-utils insert /tmp/data.db rows big.csv --csv  datasette /tmp/data.db` or open CSV in Datasette Mac Desktop app |       |
| Perl                              | [#](https://twitter.com/adambroach/status/1572510566572498944) | * `Use Parse::CSV rather than splitting on commas.`          |       |
| Perl                              | [#](https://twitter.com/benmschmidt/status/1572296810898812928) | Not sure what this does :-) : `perl -ne 'print if rand() < 1e-3 filename.csv` |       |
| Postgres                          | [#](https://twitter.com/turicas/status/1572345043712720899)  | `export DATABASE_URL="postgres://postgres:postgres@localhost:5432/postgres" rows pgimport --schema=:text: --input-encoding=utf-8 --dialect=excel myfile.csv[.gz` | .xz   |




### Previously

* Yesterday: [Tad:  A fast viewer for CSV and Parquet files and SQLite and DuckDb databases  that supports large files.  <-- Nice alternative to (in no order)  dirtylittlesql.com, graphext, knime, visidata, datasette, xsv, csvkit, R  tidyverse with arrow, python pandas / dask, as well as the traditional  grep / uniq / cut / sed / awk / sort / uniq etc   ](http://rolandtanglao.com/2022/09/20/p1-tad-fast-viewer-csv-parquet-sqlite-datasette-alternative/)        



