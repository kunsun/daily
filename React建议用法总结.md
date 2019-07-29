# React建议用法总结

### 受控与不受控

* 受控：用props传入数据的话，因为组件被父级传入的props控制，组件可以被认为是受控。
* 非受控：数据只保存在组件内部的state的话，是非受控组件，因为外部没办法直接控制state。

### 常用的生命周期方法

#### componentDidMount()

可以调用setState，它将触发额外渲染，但此渲染发生在浏览器更新Dom之前。不会被用户感知，但是会导致性能问题。

这个方法比较适合添加订阅，如果添加了订阅，请不要忘记在componentWillUnmount里取消订阅。

#### componentDidUpdate(prevProps, prevState, snapshot)

会在更新后被立即调用，首次渲染不会执行此方法。

当组件更新后，可以在此处对DOM进行操作。如果你对更新后的props进行了比较，也可以选择在此处进行网络请求。

#### componentWillUnmount()

会在组件卸载及销毁之前调用，执行必要的清理操作：如清除timer，取消网络请求或清除在componentDidMount()中创建的订阅等

### 不常用的生命周期方法

#### shouldComponentUpdate(nextProps, nextState)

当props或state发生变化时，shouldComponentUpdate()会在渲染执行之前被调用。

> React.PureComponent并未实现shouldComponentUpdate()，可以在props和state较为简单时，才使用React.PureComponent，或者在深层数据结构发生变化时调用forceUpdate()来确保组件被正确地更新。
>
> 此外，React.PureComponent中的shouldCompnentUpdate()将跳过所有子组件树的prop更新。因此，请确保所有的子组件也都是"纯"的组件。

我们不建议在shouldComponentUpdate()中进行深层比较或使用JSON.stringify()，这样非常影响效率，且会损坏性能。

#### static getDerivedStateFromProps(props, state)

存在的唯一目的：让组件在 **props 变化**时更新 state，即state的值在任何时候都取决于props。

getDerivedStateFromProps会在调用render方法之前调用，并且在初始挂载及后续更新时都会被调用。应该返回一个对象来更新state，如果返回null则不更新任何内容。

派生状态会导致代码冗余，并使组件难以维护。确保已熟悉这些简单的代替方案：

* 如果想在prop更改时，执行副作用，如数据提取与动画，请改用componentDidUpdate
* 如果想在prop更改时，重新计算某些数据，请使用memoization helper代替
* 如果想在prop更改时，"重置"某些state，请考虑完全受控或使用key使组件完全不受控代替。

##### 派生state的常见bug

* 直接复制props到state
* 在props变化后修改state

共同点在于：任何数据，都要保证只有一个数据来源，而且避免直接复制它

##### 建议的模式

* 删除组件里的state，让组件成为完全可控的组件，最好为轻量的函数组件
* 有key的非可控组件，让组件自己储存一个临时的state，加上key可以使React在key更新时创建一个新的组件。

设计组件时，重要的是确定组件是受控组件还是非受控组件。

对于不受控组件，当你想在prop变化时重置state的话，可以选择一下集中方式：

1. **建议：**重置内部所有的初始state，使用key属性
2. 其他选项：
   1. 仅更改某些字段，观察特殊属性的变化
   2. 使用ref调用实例方法

getDerivedStateFromProps会在调用render方法之前调用，并且在初始挂载及后续更新时都会被调用。

> getDerivedStateFromProps是一个高级复杂的功能，应该保守使用，这个再怎么重申也不过分。

### 用法建议

#### 请求数据

在componentDidiMount中，而非componentWillMount中

#### 根据props更新state

* 使用getDerivedStateFromProps(nextProps, prevState)
* getDerivedStateFromProps是一个static方法，意味着拿不到实例的this

> 静态方法，使用的数据不依赖类的实例

#### state变化时触发请求

在生命周期中由于state的变化触发请求，componentDidUpdate

#### props更新引起的副作用

componentDidUpdate(prevProps)

#### props更新时重新请求

getDerivedStateFromProps

