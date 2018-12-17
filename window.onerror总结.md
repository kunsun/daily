## window.onerror总结

Tab: ***错误监控***  

> `error`事件的[事件处理程序](https://developer.mozilla.org/zh-CN/docs/Web/Guide/Events/Event_handlers)。针对各种目标的不同类型的错误触发了 Error 事件：
>
> - 当**JavaScript运行时错误**（包括语法错误）发生时，[`window`](https://developer.mozilla.org/zh-CN/docs/Web/API/Window)会触发一个[`ErrorEvent`](https://developer.mozilla.org/zh-CN/docs/Web/API/ErrorEvent)接口的`error`事件，并执行`window.onerror()`。
>
> - 当一项资源（如[`<img>`或[`<scrip>`**加载失败**，加载资源的元素会触发一个[`Event`](https://developer.mozilla.org/zh-CN/docs/Web/API/Event)接口的`error`事件，并执行该元素上的`onerror()`处理函数。这些error事件不会向上冒泡到window，不过（至少在Firefox中）能被单一的[`window.addEventListener`](https://developer.mozilla.org/zh-CN/docs/Web/API/Window/addEventListener)捕获。
>
>   引用自： [MDN](https://developer.mozilla.org/zh-CN/docs/Web/API/GlobalEventHandlers/onerror)





> 在使用过程中的体会：onerror主要用来捕获预料之外的错误，而try-catch则可以用在预知情况下监控特定错误，两种形式结合使用更加高效。
>
> **try/catch 不利于性能优化**
>
> 在V8（其他JS引擎也可能出现相同情况）函数中使用了try/catch语句不能够被V8编译器优化。
>
>
>
> 引用自：https://github.com/joeyguo/blog/issues/13



### **Javascript错误**

1. 错误信息（error message）：错误信息是一个字符串用来描述代码除了什么问题。
2. 追溯栈（stack trace）：追溯栈用来记录JS错误具体出现在代码中的位置。

### **抛出错误**

1. 浏览器自身解析JS代码出错
2. 自发抛出，eg：throw new Error()

### **捕获错误**

####  window.onerror

```javascript
window.onerror = funtion(message, url, line, col, error) {
    console.log('err message: ' + message)
}
```

```javascript
window.addEventListener('error', function(event) {
    console.log('err message: ' + event.message)
})
```



第五个参数Error对象兼容性有问题，2013年加入规范中的，对于早期的浏览器版本可能不支持。

> **Chrome 是唯一一个能够通过window.onerror检测到其他源上面的文件错误的浏览器，要么将其过滤掉，要么为其设置合适的跨域头信息**



## 谷歌分析

analytics.js:

```javascript
<script>
(function(i,s,o,g,r,a,m){i['GoogleAnalyticsObject']=r;i[r]=i[r]||function(){
(i[r].q=i[r].q||[]).push(arguments)},i[r].l=1*new Date();a=s.createElement(o),
m=s.getElementsByTagName(o)[0];a.async=1;a.src=g;m.parentNode.insertBefore(a,m)
})(window,document,'script','https://www.google-analytics.com/analytics.js','ga');

ga('create', 'UA-XXXXX-Y', 'auto');
ga('send', 'pageview');
</script>
```

