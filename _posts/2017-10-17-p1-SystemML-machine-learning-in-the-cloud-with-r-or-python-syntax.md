---
layout: post
title: "SystemML: Cloud scale Machine Learning with R or Python syntax and Jupyter Notebooks"
---

## Pontifications

* From Thejesh's amazing [Getting started with SystemML](https://thejeshgn.com/2017/10/17/getting-started-with-systemml/):

<blockquote>
SystemML was created in 2010 by researchers at the IBM Almaden Research Center, it’s a high-level declarative machine learning language which comes in two flavors R-lang syntax type and Python syntax type. It was designed to make machine learning algorithms written in R-lang or Python to scale using distributed computing. Without SystemML programmers will have to rewrite the algorithms in Scala or Java to scale, which is such a waste of time. Given my preferred programming language is Python. SystemML is a blessing in disguise.<br /><br />

Now one can write the machine learning algorithm in DML (R-lang flavor) or PyDML (Python flavor) . DML/PyDML scripts can be run on Spark, on Hadoop, or in Standalone mode. Here we will experiment first in standalone mode and next Spark.<br /><br />

SystemML also exposes a MLContext API using which SystemML can be accessed from a Jupyter Notebook via Python. So if you or your team is used to notebooks then no problem, you can use the same code experimented at scale. This is my favorite way to experiment as well. We will try to explore this too.

</blockquote>