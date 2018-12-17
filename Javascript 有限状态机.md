## Javascript 有限状态机

最近要在客服后台中添加一个操作卡状态的功能，看仓老师原来的代码逻辑，引入了有限状态机的概念。

### 客服后台中有限状态机的运用

分为三个部分，1. 有限状态机的定义； 2. 状态表；3. 状态机实例

#### 一、有限状态机的定义

```javascript
class FSM {
  constructor(config) {
    this.EVENT_LIST = [
      "getInitState",
      "beforeStateChange",
      "afterStateChange"
    ]
    this.init(config)
  }
  init(config) {
    // 获取 pubsubpro.js中的方法 
    //将当前状态设为pedding
    this.loadConfig(config) //载入状态表
  }
  getInitState() {
    //发布事件
    //触发getInitState事件
  }
  setState(state) {
    // 检查状态的有效性
    // 触发beforeStateChange，成功之后当前状态，并触发afterStateChange
  }
}
```

#### 二、状态表

```javascript
// 状态走向表Events
{
  	"A" : {
			"to" : [ "B" ]
		},
		"B" : {
			"to" : [ "A" ]
		},
}
// 状态静态表Status
{
  "A" : "未开启",
	"B" : "已开启",
	"AB" : "已发起开启漏话提醒",
	"BA" : "已发起关闭漏话提醒"
}
```

#### 三、 状态机实例

```javascript
new FSM(Events)
//绑定getInitState事件，执行初始化状态
//绑定beforeStateChange事件，接触原生事件绑定
//绑定afterStateChange事件，执行刷新页面，重新绑定事件
```



### Javascript State Machine 源码分析



#### 经典的继承

Javascript单一原型链的缺陷

```javascript
// Shape - 父类(superclass)
function Shape() {
  this.x = 0;
  this.y = 0;
}

// 父类的方法
Shape.prototype.move = function(x, y) {
  this.x += x;
  this.y += y;
  console.info('Shape moved.');
};

// Rectangle - 子类(subclass)
function Rectangle() {
  Shape.call(this); // call super constructor.
}

// 子类续承父类
// 说明： Object.create()方法创建一个新对象，使用现有的对象来提供新对象的____proto____
Rectangle.prototype = Object.create(Shape.prototype);
Rectangle.prototype.constructor = Rectangle;

var rect = new Rectangle();

console.log('Is rect an instance of Rectangle?',
  rect instanceof Rectangle); // true
console.log('Is rect an instance of Shape?',
  rect instanceof Shape); // true
rect.move(1, 1); // Outputs, 'Shape moved.'
```

#### ES6中的mixin式继承

mixin弥补了Javascript单一原型链的缺陷，可以实现类似于多重继承的效果。







