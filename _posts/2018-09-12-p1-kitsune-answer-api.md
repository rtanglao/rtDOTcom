---
layout: post
title: "Kitsune aka support.mozilla.org answer API"
---

## Pontifications

* Like the [kitsune question API](http://rolandtanglao.com/2018/09/13/kitsune-question-api/), this was discovered by me in [jscher2000's myq.html code](https://github.com/jscher2000/My-SuMo-Questions/blob/master/myq.html)! Couldn't find any official docs but maybe there are some docs?!?!
* sample answer API code: [https://github.com/rtanglao/rt-kitsune-api/blob/master/answerTestAPI.rb](https://github.com/rtanglao/rt-kitsune-api/blob/master/answerTestAPI.rb)  
  * sample API json response: [https://github.com/rtanglao/rt-kitsune-api/blob/master/sampleAnswerTestAPIoutput.md](https://github.com/rtanglao/rt-kitsune-api/blob/master/sampleAnswerTestAPIoutput.md) 
* API is:```https://support.mozilla.org/api/2/answer/?format=json&id=<question_id>``` 
  * where ```<question_id>``` is an integer question id! 