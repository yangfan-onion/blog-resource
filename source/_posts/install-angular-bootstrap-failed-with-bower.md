title: "install angular-bootstrap failed with bower"
date: 2015-05-28 16:01:41
coverImage: cover.png
coverHideInPost: true
tags:
---
今天使用bower安装[angular-boostrap](https://github.com/angular-ui/bootstrap)模块,安装完成之后, 往AngularJS应用里面注入模块的时候出错, 报错如下
{% codeblock %}
    Uncaught Error: [$injector:modulerr] Failed to instantiate module wechatEnterpriseFrontApp due to:
    Error: [$injector:modulerr] Failed to instantiate module ui.bootstrap due to:
    Error: [$injector:nomod] Module 'ui.bootstrap' is not available! You either misspelled the module name or forgot to load it. If registering a module ensure that you specify the dependencies as the second argument.
    http://errors.angularjs.org/1.4.0/$injector/nomod?p0=ui.bootstrap
        at REGEX_STRING_REGEXP (http://127.0.0.1:9000/bower_components/angular/angular.js:68:12)
        at http://127.0.0.1:9000/bower_components/angular/angular.js:1953:17
        at ensure (http://127.0.0.1:9000/bower_components/angular/angular.js:1877:38)
        at module (http://127.0.0.1:9000/bower_components/angular/angular.js:1951:14)
        at http://127.0.0.1:9000/bower_components/angular/angular.js:4338:22
        at forEach (http://127.0.0.1:9000/bower_components/angular/angular.js:336:20)
        at loadModules (http://127.0.0.1:9000/bower_components/angular/angular.js:4322:5)
        at http://127.0.0.1:9000/bower_components/angular/angular.js:4339:40
        at forEach (http://127.0.0.1:9000/bower_components/angular/angular.js:336:20)
        at loadModules (http://127.0.0.1:9000/bower_components/angular/angular.js:4322:5)
    http://errors.angularjs.org/1.4.0/$injector/modulerr?p0=ui.bootstrap&p1=Err…2F%2F127.0.0.1%3A9000%2Fbower_components%2Fangular%2Fangular.js%3A4322%3A5)
        at REGEX_STRING_REGEXP (http://127.0.0.1:9000/bower_components/angular/angular.js:68:12)
        at http://127.0.0.1:9000/bower_components/angular/angular.js:4361:15
        at forEach (http://127.0.0.1:9000/bower_components/angular/angular.js:336:20)
        at loadModules (http://127.0.0.1:9000/bower_components/angular/angular.js:4322:5)
        at http://127.0.0.1:9000/bower_components/angular/angular.js:4339:40
        at forEach (http://127.0.0.1:9000/bower_components/angular/angular.js:336:20)
        at loadModules (http://127.0.0.1:9000/bower_components/angular/angular.js:4322:5)
        at createInjector (http://127.0.0.1:9000/bower_components/angular/angular.js:4248:11)
        at doBootstrap (http://127.0.0.1:9000/bower_components/angular/angular.js:1625:20)
        at bootstrap (http://127.0.0.1:9000/bower_components/angular/angular.js:1646:12)
    http://errors.angularjs.org/1.4.0/$injector/modulerr?p0=wechatEnterpriseFro…F%2F127.0.0.1%3A9000%2Fbower_components%2Fangular%2Fangular.js%3A1646%3A12)
{% endcodeblock %}

[解决方案](https://github.com/angular-ui/bootstrap/issues/2246)

{% codeblock %}
    //The problem seems to be occurring because of the concatenation.

    //In Index.html if you separate out ui-bootstrap-tpls.js

        <!-- build:js(.) scripts/vendor2.js -->
        <script src="bower_components/angular-bootstrap/ui-bootstrap-tpls.js"></script>
        <!-- endbuild -->
    //And in your root bower.json add

    ...
    "overrides": {
      "angular-bootstrap": {
        "main": []
      }
    }
    ...
    //Everything will work just fine and, for the most part, your files are uglified. Obviously this is just a workaround.
{% endcodeblock %}