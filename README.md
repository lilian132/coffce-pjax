# Coffce-PJAX

## 介绍
Coffce-PJAX是一个简单的PJAX库，通过简单的配置，既可将所有a标签替换为AJAX请求。支持缓存及在各个页面之间传递参数。正常浏览器上使用HTML5 History API，低版本浏览器使用Hash，兼容IE8~IE11，Chrome，Firefox等。

## 用法
####简单配置：
``` javascript
// 引入pjax，也可以使用window.CoffcePJAX
var pjax = require("coffce-pjax");

pjax.init({
    // 替换新页面内容的容器
    container: "body",
    // 是否在低版本浏览器上使用Hash
    hash: true
});
```
####高级配置:
``` javascript
var pjax = require("coffce-pjax");
pjax.init({
    // 各个执行阶段的过滤函数，返回false则停止pjax执行
    filter: {
        // 用来过滤不想转换成ajax请求的a标签
        selector: function(a){},
        // 过滤返回的内容
        content: function(info){/*info.title info.html*/},
        // (未完成)缓存过滤
        cache: null
    },
    // 各个阶段的自定义函数，将替换默认实现
    custom: {
        // 自定义更换页面函数，可以在此实现动画替换
        append: function(html, container){},
        // (未完成)自定义发送请求函数
        ajax: null
    },
    // 要替换内容的容器，可为选择器字符串或DOM对象
    container: "body",
    // 是否在前进后退时开启本地缓存功能，使用SessionStorage
    cache : true,
    // 是否对低版本浏览器启用hash方案
    hash: false,
    // 是否允许跳转到当前相同页面，相当于刷新
    same: true,
    // (未完成)服务器是否支持，为true时表示服务器将根据HTTP头coffce-pjax返回片段HTML，为false时表示服务器将返回整个页面html，由插件内部获取需要片段
    serverSupport: false,
    // 调试模式，console.log调试信息
    debug: false
});
```

## 接口
####对外接口：
接口      | 描述
----------|----------
pjax.init(config) | 初始化，参数见上面[用法]
pjax.turn(url, data, callback) | 跳转到[url]，[data]表示要带到新页面的参数，在callback或者xhrSuccess事件里接收，跳转完成触发[callback]回调
pjax.on(type, listener) | 监听事件，见下表
pjax.off(type) | 移除监听
pjax.trigger(type, args) | 手动触发事件
pjax.destroy | 注销pjax插件

#### 事件类型：
类型 | 参数 | 描述
-----|------|------
xhrBegin | { url, fnb, data} | 
xhrSuccess | { url, fnb, data} | 
xhrEnd | { url, fnb, data} | 
xhrError | { url, fnb, data} | 


## 注意
作者很懒，没有经过详细的测试，使用需自己小心。
