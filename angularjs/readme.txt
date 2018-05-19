-----简单介绍

AngularJS 扩展了 HTML
AngularJS 通过 ng-directives 扩展了 HTML。
ng-app 指令定义一个 AngularJS 应用程序。
ng-model 指令把元素值（比如输入域的值）绑定到应用程序。
ng-bind 指令把应用程序数据绑定到 HTML 视图。
当网页加载完毕，AngularJS 自动开启。


-----命令列表

ng-app          声明angular的所有者
ng-init         初始化数据
ng-model        绑定标签名称到angular变量
ng-bind         绑定变量到html，意味着输出
ng-controller   声明控制器
ng-repeat
xxx-directive   自定义指令
ng-show
ng-options
ng-disabled
ng-hide
ng-include      包含文件，跨越要添加白名单

完整指令参考：https://www.runoob.com/angularjs/angularjs-reference.html

ng-model 指令也可以：

为应用程序数据提供类型验证（number、email、required）。
为应用程序数据提供状态（invalid、dirty、touched、error）。
为 HTML 元素提供 CSS 类。
绑定 HTML 元素到 HTML 表单。


-----表达式

AngularJS 表达式
AngularJS 表达式写在双大括号内：{{ expression }}。
AngularJS 表达式 很像 JavaScript 表达式：它们可以包含文字、运算符和变量。

实例 {{ 5 + 5 }} 或 {{ firstName + " " + lastName }}

-----模块

var app = angular.module('myApp', []);

-----控制器

app.controller('myCtrl', function($scope) {
    $scope.firstName= "John";
    $scope.lastName= "Doe";
});

-----遍历

<div data-ng-app="" data-ng-init="names=['Jani','Hege','Kai']">
  <p>使用 ng-repeat 来循环数组</p>
  <ul>
    <li data-ng-repeat="x in names">
      {{ x }}
    </li>
  </ul>
</div>

-----css

ng-model 指令基于它们的状态为 HTML 元素提供了 CSS 类：

ng-empty
ng-not-empty
ng-touched
ng-untouched
ng-valid: 验证通过
ng-invalid: 验证失败
ng-valid-[key]: 由$setValidity添加的所有验证通过的值
ng-invalid-[key]: 由$setValidity添加的所有验证失败的值
ng-pristine: 控件为初始状态
ng-dirty: 控件输入值已变更
ng-touched: 控件已失去焦点
ng-untouched: 控件未失去焦点
ng-pending: 任何为满足$asyncValidators的情况

<style>
input.ng-invalid {
    background-color: lightblue;
}
</style>

-----Scope

Scope(作用域) 是应用在 HTML (视图) 和 JavaScript (控制器)之间的纽带。
Scope 是一个对象，有可用的方法和属性。
Scope 可应用在视图和控制器上。

$scope代表控制器对象。

-----根作用域

所有的应用都有一个 $rootScope，它可以作用在 ng-app 指令包含的所有 HTML 元素中。
$rootScope 可作用于整个应用中。是各个 controller 中 scope 的桥梁。用 rootscope 定义的值，可以在各个 controller 中使用。

app.controller('myCtrl', function($scope, $rootScope) {
    $scope.names = ["Emil", "Tobias", "Linus"];
    $rootScope.lastname = "Refsnes";
});

-----过滤器/格式化

过滤器可以通过一个管道字符（|）和一个过滤器添加到表达式中。

--currency	格式化数字为货币格式。
--filter	从数组项中选择一个子集。
--lowercase	格式化字符串为小写。
--orderBy	根据某个表达式排列数组。
--uppercase	格式化字符串为大写。

<p>姓名为 {{ lastName | uppercase }}</p>
<p>总价 = {{ (quantity * price) | currency }}</p>

自定义过滤器

app.filter('reverse', function() { //可以注入依赖
    return function(text) {
        return text.split("").reverse().join("");
    }
});

-----服务

服务是一个函数或对象，可在你的 AngularJS 应用中使用。
AngularJS 内建了30 多个服务。

---$location
---$http
---$timeout
---$interval

app.controller('customersCtrl', function($scope, $location) {
    $scope.myUrl = $location.absUrl();
});

自定义服务

app.service('hexafy', function() {
    this.myFunc = function (x) {
        return x.toString(16);
    }
});
app.controller('myCtrl', function($scope, hexafy) {
    $scope.hex = hexafy.myFunc(255);
});

-----$http

$http 是 AngularJS 中的一个核心服务，用于读取远程服务器的数据。

--$http.get
--$http.head
--$http.post
--$http.put
--$http.delete
--$http.jsonp
--$http.patch

$http.get('/someUrl', config).then(successCallback, errorCallback);
$http.post('/someUrl', data, config).then(successCallback, errorCallback);

-----API

全局 API 函数使用 angular 对象进行访问。

--angular.lowercase()	转换字符串为小写
--angular.uppercase()	转换字符串为大写
--angular.isString()	判断给定的对象是否为字符串，如果是返回 true。
--angular.isNumber()	判断给定的对象是否为数字，如果是返回 true。

-----动画

AngularJS 提供了动画效果，可以配合 CSS 使用。
AngularJS 使用动画需要引入 angular-animate.min.js 库。

还需在应用中声明：
<body ng-app="ngAnimate">

-----依赖注入

依赖注入（Dependency Injection，简称DI）是一种软件设计模式，是指把一个元素注入到另一个对象环境中，使该元素
成为此对象环境的一部分。有点像在一个类中引入另一个包含各种元素的文件，这样文件中的元素就可以在类中使用。

AngularJS 提供很好的依赖注入机制。以下5个核心组件用来作为依赖注入：

--value
--factory
--service
--provider
--constant

App.value("defaultInput", 5);

-----路由

通过 AngularJS 可以实现多视图的单页Web应用（single page web application，SPA）。
AngularJS通过 # + 标记 帮助我们区分不同的逻辑页面并将不同的页面绑定到对应的控制器上

-----参考手册

https://www.runoob.com/angularjs/angularjs-reference.html


