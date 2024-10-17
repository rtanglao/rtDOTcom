---
layout: post
title: "Count Thunderbird SUMO questions by week using a CSV file using mlr aka miller by 1st creating a unix time column w/strptime and then creating an iso_week column from the unix aka epoch time w/strftime (bonus: create a SQLite file using sqlite-utils)"
---
[Discovered](http://rolandtanglao.com/2020/07/29/p1-blogthis-checkvist-list-links-to-blog/): Sep 12, 2024 06:36  

1. Create column with unix epoch time from [ALLTIME/2024-yearly-thunderbird-questions.csv:](https://github.com/thunderbird/github-action-thunderbird-aaq/blob/main/ALLTIME/2024-yearly-thunderbird-questions.csv)

```bash
cd ../ALLTIME
mlr --csv put '$created_epoch = strptime($created, "%Y-%m-%d %H:%M:%S %z")' \
2024-yearly-thunderbird-questions.csv > created_epoch-2024-yearly-thunderbird-questions.csv
```
2. Create `created_epoch` with unix time and isoweek with `iso_week`
```bash
mlr --csv put '$created_epoch = strptime($created, "%Y-%m-%d %H:%M:%S %z")' \
then put '$iso_week = strftime($created_epoch, "%V")' \
../ALLTIME/2024-yearly-thunderbird-questions.csv > \
epoch_time_iso_week_2024-yearly-thunderbird-questions.csv
```
3. Count by iso_week
```bash
 mlr --csv count-distinct -f iso_week \
epoch_time_iso_week_2024-yearly-thunderbird-questions.csv
```
result:
```csv
iso_week,count
01,237
02,255
03,251
04,279
05,238
06,231
07,243
08,273
09,237
10,214
11,226
12,214
13,227
14,194
15,237
16,259
17,226
18,194
19,211
20,217
21,177
22,179
23,202
24,211
25,231
26,194
27,190
28,295
29,337
30,331
31,400
32,416
33,392
34,401
35,375
36,367
37,115
```
4. Create database file
```bash
cd ../SQLITE
sqlite-utils insert epoch_iso_week-2024-thunderbird-questions-only.db questions \
../ALLTIME/epoch_time_iso_week_2024-yearly-thunderbird-questions.csv --csv \
--detect-types
```

## Previously

*  March 1, 2020: [How to: retain selected fields and remove the rest in a CSV file using mlr aka miller](http://rolandtanglao.com/2020/03/01/p1-howto-mlr-miller-remov-fields-from-csv/)
