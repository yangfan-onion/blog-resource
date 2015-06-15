title: "Issue about AngularJS executing controller twice"
date: 2015-05-31 15:46:55
tags:
---
{% blockquote AngularJS https://docs.angularjs.org/api/ng/directive/ngController AngularJS docs - ngController %}
Note that you can also attach controllers to the DOM by declaring it in a route definition via the $route service. A common mistake is to declare the controller again using ng-controller in the template itself. This will cause the controller to be attached and executed twice.
When you use ngRoute with the ng-view directive, the controller gets attached to that dom element by default. So you will not need to attach it again in the template.
{% endblockquote %}

When you use ngRoute with the ng-view directive, the controller gets attached to that dom element by default. So you will not need to attach it again in the template.

今天做AngularJS路由的时候遇到了一个问题,controller里面的方法执行了两次,后来google时发现了原因,大意是: 

{% codeblock %}
    //路由里面已经绑定了一次controller
    .when('/repo-top', {
        templateUrl: 'views/repo-top.html',
        controller: 'RepoTopCtrl'
    })

    //在模板上面不需要再次绑定了
    //<div ng-controller="RepoTopCtrl">custom content</div>
    <div>custom content</div>
{% endcodeblock %}

