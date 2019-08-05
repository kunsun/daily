# Redux的思想与原理

## 用到的函数式编程的知识

#### 柯里化函数curry

好处：

* 避免了给一个函数传入大量的参数
* 降低耦合度和代码冗余，便于复用

#### 代码组合

`const compose = (f, g) => (x) => f(g(x));`

通过这样函数之间的组合，可以大大增加可读性

## Redux 构造

### 1. createStore

#### dispatch

接收的action参数，是个对象，而不是方法。

调用dispatch的时候只能一个个调用，调用前需要判断isDispatching的状态。

#### subscribe

添加到监听数组中，添加到下一次dispatch时才会生效的数组

### 2. combineReducers

reducer负责状态的管理，在实际使用中，应用的状态时可以分成多个模块的。

combineReducers返回一个函数，这个函数是多个模块函数的结合者。

### 3. applyMiddleWare

reducer是一个纯函数，如果需要处理副作用，就需要中间件了。参数是中间件数组middlewares。

1. 返回一个函数： createStore => (...args) => { }
2. 返回具体的加强函数：(...args) => {}， 可以加强createStore，加强后的createStore函数可以改造原有的dispatch方法。



## redux-thunk

1. 返回中间件函数：({dispatch, getState})  => next => {}，这个函数需要传入store的dispatch与getState
2. 返回改造函数：next => action => {}，next指的是改造前的dispatch
3. 返回改造后的dispatch方法：action => {}，action中传入store的dispatch与getState











