## React Context 

React 16.3更新了Context API，接下来对[官方文档](https://reactjs.org/docs/context.html)做一个翻译。

>  Context提供了一种通过组件树传递数据的方法，而不需要通过props层层传递。

传统的React App，数据通过props自上而下传递，但是对于UI主题、本地化配置等很多组件都会用到的属性来说，这种方法过于笨重。Context就是用来简化这种场景的。

[TOC]

### 什么时候用Context

Context 设计的初衷是用来全局的分享数据，例如当前登录用户、主题、语言。例子：下面的代码通过props传递一个theme的属性。

```javascript
class App extends React.Component {
  render() {
    return <Toolbar theme="dark" />;
  }
}

function Toolbar(props) {
  // The Toolbar component must take an extra "theme" prop
  // and pass it to the ThemedButton. This can become painful
  // if every single button in the app needs to know the theme
  // because it would have to be passed through all components.
  return (
    <div>
      <ThemedButton theme={props.theme} />
    </div>
  );
}

class ThemedButton extends React.Component {
  render() {
    return <Button theme={this.props.theme} />;
  }
}
```

如果用Context，就可以避免使用中间元素传递props

```javascript
// Context lets us pass a value deep into the component tree
// without explicitly threading it through every component.
// Create a context for the current theme (with "light" as the default).
const ThemeContext = React.createContext('light');

class App extends React.Component {
  render() {
    // Use a Provider to pass the current theme to the tree below.
    // Any component can read it, no matter how deep it is.
    // In this example, we're passing "dark" as the current value.
    return (
      <ThemeContext.Provider value="dark">
        <Toolbar />
      </ThemeContext.Provider>
    );
  }
}

// A component in the middle doesn't have to
// pass the theme down explicitly anymore.
function Toolbar(props) {
  return (
    <div>
      <ThemedButton />
    </div>
  );
}

class ThemedButton extends React.Component {
  // Assign a contextType to read the current theme context.
  // React will find the closest theme Provider above and use its value.
  // In this example, the current theme is "dark".
  static contextType = ThemeContext;
  render() {
    return <Button theme={this.context} />;
  }
}
```

### 使用Context之前

当需要在多个不同嵌套等级的Compnent中使用某些数据的时候，Context才会被派上用场。需要谨慎的使用，因为使用Context会让组件的复用变得更难。



