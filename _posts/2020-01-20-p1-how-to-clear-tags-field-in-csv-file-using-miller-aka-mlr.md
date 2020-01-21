---

layout: post
title: "How to clear a field in a CSV file using miller aka mlr"
---

# Pontifications

```bash
mlr --csv put '$tags=""' ff70-1st-four-weeks-url-tags.csv  > ff70-1st-four-weeks-url-blank-tags.csv
```
* The above miller / mlr command line clears the "tags" field



