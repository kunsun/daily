## Generator研究与改进

telecom-fe-generator是组内用来初始化项目的工具库。

想要通过研究Vue Cli与 create-react-app的构建思想，来完成generator的升级。

这是一个很有意义的工作，需要花费几天的时间来做。



### Todo

- [ ] 新增.gitignore文件
- [ ] 增加less的配置



### 计划

- [ ] 完成vue cli的研究  day 1
- [ ] 完成create-react-app   day 1
- [ ] 编写新的generator  day 2

### 备用计划

如果需要花很长的时间做这个事情，那么就可以先直接使用create-react-app完成项目开发，之后再做优化。

### Vue Cli

研究Vue Cli的配置，找到改进点。

#### 配置

##### 1. 项目config.js

```js
module.exports = {
  outputDir: 'dist1', // 输出目录
  baseUrl: undefined,  // 应用的部署地址
  assetsDir: undefined, // 资源目录
  runtimeCompiler: undefined, // 是否启用运行时编译
  productionSourceMap: undefined,
  parallel: undefined, // 超过一个CPU时，可以启动多线程并行编译
  css: {
    modules: true,   // 是否启用CSS module
    sourceMap: true,  // 是否抽取source map
    extract: false  // 是否抽取extract
  }
}
```

##### 2. eslint配置



#### 命令

集成到了vue-cli-service这个库中。

有以下命令：

1. serve (必做)
2. build （比做）
3. lint
4. inspect

##### serve

--open 在服务启动时打开浏览器

--copy 在服务器启动时将url复制到剪切板

--mode 制定环境模式

--host 指定host

-- port 制定port

-- https 使用https

##### build

##### inspect



### 云平台的脚手架

1. 用webpack-dev-server统一实现代理

2. 自带goku配置项



### 用到的库

* chalk: 粉笔，用来美化终端的字符串样式
* semver:  语义化版本控制模块
* slash:  Convert Windows backslash paths to slash paths，转换windows的路径
* commander: 命令行界面工具

#### commander研究

optionMissingArgument是一个函数，









































