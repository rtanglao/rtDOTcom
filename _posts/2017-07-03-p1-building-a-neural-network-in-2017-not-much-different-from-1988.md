---
layout: post
title: Building a neural network in 9 lines of Python code in 2017, not much better than 1989 -- except for better libraries, more RAM, more CPUs, more data but the same algorithms, what am I missing?
---

## Pontifications

* [Building a neural network in 2017 in 9 lines of Python code](https://medium.com/technology-invention-and-more/how-to-build-a-simple-neural-network-in-9-lines-of-python-code-cc8f23647ca1?imm_mid=0f4065&cmp=em-prog-na-na-newsltr_20170701) is not much better than 1989 (at least the ones I looked at back in the 80s) -- except for better libraries, more RAM, more CPUs, more data but the same algorithms, what am I missing?
* In the unlikely (haha as if ) event medium and github disappear and/or go evil, here are the 9 lines:

```python
from numpy import exp, array, random, dot
training_set_inputs = array([[0, 0, 1], [1, 1, 1], [1, 0, 1], [0, 1, 1]])
training_set_outputs = array([[0, 1, 1, 0]]).T
random.seed(1)
synaptic_weights = 2 * random.random((3, 1)) - 1
for iteration in xrange(10000):
    output = 1 / (1 + exp(-(dot(training_set_inputs, synaptic_weights))))
    synaptic_weights += dot(training_set_inputs.T, (training_set_outputs - output) * output * (1 - output))
print 1 / (1 + exp(-(dot(array([1, 0, 0]), synaptic_weights))))
```