---
layout: post
title: How to get R 3.2 working with iPython aka Jupyter and Yosemite
---
The following is in addition/complementary for Yosemite to the nice recipe at [How to Install R kernel for IPython Jupyter on Mac OS X Yosemite](http://www.datascienceriot.com/?p=589): 

    install_github(‘IRkernel/repr’) # inside R before installing the R display package
    brew install wget
    wget https://raw.githubusercontent.com/zeromq/cppzmq/master/zmq.hpp
    mv zmq.hpp /usr/local/include/
    ipython kernel spec install —replace —name ir —user /usr/local/Cellar/r/3.2.0/R.framework/Versions/3.2/Resources/library/IRkernel/kernelspec

