---
layout: post
title: No I don't need'unsafe-eval' in the CSP Header for Google Analytics? But maybe for angular.js?
---

## Pontifications

In an earlier post I asked [Do I need 'unsafe-eval' in the CSP Header for Google Analytics?](http://rolandtanglao.com/2017/03/06/p1-csp-for-google-analytics/). The answer is no but I might need it for angular.js:

FROM [ngCsp angular documentation](https://docs.angularjs.org/api/ng/directive/ngCsp):

**QUOTE**
<blockquote>
You can specify which of the CSP related AngularJS features should be deactivated by providing a value for the ng-csp attribute. The options are as follows:<br />

  * no-inline-style: this stops AngularJS from injecting CSS styles into the DOM<br/>
  * no-unsafe-eval: this stops AngularJS from optimizing $parse with unsafe eval of strings

</blockquote>

**END QUOTE**
