---
layout: post
tags : [r, rlang, jupyter, python]
title: How to correctly install jupyter
---

My [last howto install jupyter post](http://rolandtanglao.com/2015/05/17/p1-getting-r-3-2-working-in-jupyter-with-yosemite/) was out of date!

From the [jupyter notebook github repo](https://github.com/jupyter/notebook):

```bash
pip install --upgrade setuptools pip
git clone https://github.com/jupyter/notebook.git
cd notebook
pip install -r requirements.txt -e .
jupyter notebook
```