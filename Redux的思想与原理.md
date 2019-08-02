# Redux的思想与原理

### 用到的函数式编程的知识

#### 柯里化函数curry

好处：

* 避免了给一个函数传入大量的参数
* 降低耦合度和代码冗余，便于复用

#### 代码组合

`const compose = (f, g) => (x) => f(g(x));`

通过这样函数之间的组合，可以大大增加可读性





### applyMiddleWare



### createStore



