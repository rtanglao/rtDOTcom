---
layout: post
title: "WIP: q, xsv, graphext, dirtylittlesql, Tools for handling large CSV files from Simon Willison's mega replied to thread"
---
### CSV Tools Summary Table

* New to me :-) CSV Tools (except for [Tad which was documented yesterday](http://rolandtanglao.com/2022/09/20/p1-tad-fast-viewer-csv-parquet-sqlite-datasette-alternative/)) from the 1000 replies to Simon Willison's tweet: [If someone gives you a CSV file with 100,000 rows in it, what tools do you use to start exploring and understanding that data?](https://twitter.com/simonw/status/1572285367382061057)

  | Name     | Tweet                                                        | Type     | Notes                                                        |
  | -------- | ------------------------------------------------------------ | -------- | ------------------------------------------------------------ |
  | Postgres | [[1]](https://twitter.com/fuzzychef/status/1572389081472208896), [[2]](https://twitter.com/fuzzychef/status/1572428556126556162) | Database | * Use COPY command, CSV data wrapper which lets you do CSV operations without even copying them which is good for folders<br />* |
  |          |                                                              |          |                                                              |
  |          |                                                              |          |                                                              |

### Programming language and other small code snippets

| Language/Tool                     | Tweet                                                      | Snippet                                                      | Notes |
| --------------------------------- | ---------------------------------------------------------- | ------------------------------------------------------------ | ----- |
| Datasette on Mac / CLI on Windows | [#](https://twitter.com/simonw/status/1572295332767371265) | `sqlite-utils insert /tmp/data.db rows big.csv --csv  datasette /tmp/data.db` or open CSV in Datasette Mac Desktop app |       |
|                                   |                                                            |                                                              |       |
|                                   |                                                            |                                                              |       |




### Previously

* Yesterday: [Tad:  A fast viewer for CSV and Parquet files and SQLite and DuckDb databases  that supports large files.  <-- Nice alternative to (in no order)  dirtylittlesql.com, graphext, knime, visidata, datasette, xsv, csvkit, R  tidyverse with arrow, python pandas / dask, as well as the traditional  grep / uniq / cut / sed / awk / sort / uniq etc   ](http://rolandtanglao.com/2022/09/20/p1-tad-fast-viewer-csv-parquet-sqlite-datasette-alternative/)        



