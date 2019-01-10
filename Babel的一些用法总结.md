# Babel的一些用法总结
平时使用Babel的时候，有很多功能没有注意。通过这篇文章深入研究一下不懂的地方。

## 官方文档
> Babel includes a polyfill that includes a custom regenerator runtime and core-js.  

Babel包括两部分，regenerator runtime和core-js。通过Babel可以使用Built-ins，如Promise和WeakMap。也可以使用静态方法，如Array.from和Object.assign。也可以使用实例方法，如Array.prototype.includes。还有generator functions。

### 与@babel/preset-env一起使用
* `useBuiltIns: 'usage'`  则不需要在webpack.config.js或者source中引入@babel/polyfill。
* `useBuiltIns: 'entry'`  则需要在应用的入口处引入@babel-polyfill
* `useBuiltIns: false`  或者没有useBuiltIns这个选项，则直接add @babel/polyfill在webpack.config.js的entry array 中。


## Core-js
> @babel/polyfill IS core-js and regenerator-runtime for generators and async functions, it's just 2 lines, so if you load @babel/polyfill - you load the global version of core-js without ES proposals.  














#学习笔记