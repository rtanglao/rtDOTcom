---
layout: post
title: "Part 2B Got NLTK working with Firefox 55 SUMO support questions! Now what? Sentiment?"
---

## Pontifications

See [Part 2A Get Firefox 55 first 3weeks' words in preparation for NLTK -ngram-analysis](http://rolandtanglao.com/2018/01/26/p1-part2a-get-firefox55-first-3weeks-words-in-preparation-for-nltk-ngram-analysis/)

* 1\. Here's how I invoked the code:

```bash
python/print-ngram-from-file.py ff55.08August2017.28august2017.1st.3weeks.title.content.txt
```

* 2\. Here's the code, [print-ngram-from-file.py](https://github.com/rtanglao/sumo-questions/blob/master/python/print-ngram-from-file.py)

```python
#!/usr/local/bin/python3
import nltk, re, pprint
from nltk import word_tokenize
from nltk import bigrams, trigrams
import fileinput
raw = ""
for line in fileinput.input():
    raw += line.rstrip()
    raw += ' '
tokens = word_tokenize(raw)
tokens_bigrams = bigrams(tokens)
print (list(tokens_bigrams))
```
