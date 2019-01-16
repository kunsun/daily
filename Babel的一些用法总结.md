# Babel的一些用法总结
平时使用Babel的时候，有很多功能没有注意。通过这篇文章深入研究一下不懂的地方。

## @babel/core
> Babel compiler core.  

## @babel/cli
> Babel comes with a built-in CLI which can be used to compile files from the command line.  
> In addition, various entry point scripts live in the top-level package at @babel/cli/bin. There is a shell-executable utility script, babel-external-helpers.js, and the main Babel cli script, babel.js.  

Babel内置CLI，可以用来compile files from the command line。这些scripts放置在在@babel/cli/bin中。

虽然可以全局安装，但是以locally的方式安装更好。

1. 可以保持@babel/cli的版本不一致
2. 让项目中没有隐含的依赖性，便于移植，易于安装。webpack-cli同理。

## @babel/preset-env
> @babel/preset-env is a smart preset that allows you to use the latest JavaScript without needing to micromanage which syntax transforms (and optionally, browser polyfills) are needed by your target environment(s). This both makes your life easier and JavaScript bundles smaller!  

是一个聪明的预制，可以仅仅配置项目所需的polyfill和transform。使得JS打包体积更小。

### useBuiltIns
> This option configures how @babel/preset-env handles polyfills.  

这个选项配置如何让@babel/preset-env 处理polyfills。

* `useBuiltIns: 'entry'`  则需要在应用的入口处引入@babel-polyfill。根据`target` 中浏览器的版本，将polyfills拆分，仅仅引入不支持的polyfills。
* `useBuiltIns: 'usage'`  **实验性的功能**  则不需要在webpack.config.js或者source中引入@babel/polyfill。自动分析文件中用到的新功能。
* `useBuiltIns: false`  或者没有useBuiltIns这个选项，则直接add @babel/polyfill在webpack.config.js的entry array 中。

## @babel/polyfill官方文档
> Babel includes a polyfill that includes a custom regenerator runtime and core-js.  

Babel包括两部分，regenerator runtime和core-js。旨在模拟完整的ES2015+环境，旨在用在App中而不是Library中。通过Babel可以使用Built-ins，如Promise和WeakMap。也可以使用静态方法，如Array.from和Object.assign。也可以使用实例方法，如Array.prototype.includes。还有generator functions。

## @babel/runtime
可以将重复的引用提取出来，inject 相关的helpers即可，如extends、promise等。@babel/runtime中就包含了这些helpers。

**缺点**： 不模拟实例方法，即内置对象原型上的方法，所以类似Array.prototype.find，无法通过babel-runtime使用。

### @babel/plugin-transform-runtime
@babel/plugin-transform-runtime可以自动提取出这些 injected helper。

```javascript
{
  "plugins": [
    [
      "@babel/plugin-transform-runtime",
      {
        "corejs": false,
        "helpers": true,
        "regenerator": true,
        "useESModules": false
      }
    ]
  ]
}
```

corejs可以设置为false或者2。如果是false则使用@babel/runtime，如果是2则使用@babel/runtime-corejs2，除了runtime中的helpers，另外含有Promise，Symbol等。

## Core-js
> @babel/polyfill IS core-js and regenerator-runtime for generators and async functions, it's just 2 lines, so if you load @babel/polyfill - you load the global version of core-js without ES proposals.  














#学习笔记