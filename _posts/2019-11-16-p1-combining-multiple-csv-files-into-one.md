---

layout: post
title: "HowTo: Concat multiple CSV Files into one using head and sed"
---

# Pontifications

* Combining multiple CSV files with the same headers is easy using `head -1` and `sed 1d`!

```bash
head -1 file1.csv > final.csv
for filename in $(ls file*.csv); do sed 1d $filename >> final.csv; done
```

