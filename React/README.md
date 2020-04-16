# react

<details>
<summary>React 生命周期讲解</summary>

## 组件生命周期 - 创建阶段(Mounting)

* 特点：该阶段的函数只执行一次

### constructor()

* 作用：获取`props`和初始化`state`
* 说明：通过 `constructor()` 的参数`props`获取
* 设置`state`和`props`

```js
class Greeting extends React.Component {
  constructor(props) {
    // 获取 props
    super(props)
    // 初始化 state
    this.state = {
      count: props.initCount
    }
  }
}

// 初始化 props
// 语法：通过静态属性 defaultProps 来初始化props
Greeting.defaultProps = {
  initCount: 0
};
```

### componentWillMount()

* 说明：组件被挂载到页面之前调用，其在`render()`之前被调用，因此在这方法里同步地设置状态将不会触发重渲染
* 注意：无法获取页面中的DOM对象
* 注意：可以调用`setState()`方法来改变状态值
* 用途：发送ajax请求获取数据

```js
componentWillMount() {
  console.warn(document.getElementById('btn')) // null
  this.setState({
    count: this.state.count + 1
  })
}
```

### render()

* 作用：渲染组件到页面中，无法获取页面中的DOM对象
* 注意：不要在`render`方法中调用 `setState()` 方法，否则会递归渲染
* 原因说明：状态改变会重新调用`render()`，`render()`又重新改变状态

```js
render() {
  console.warn(document.getElementById('btn')) // null

  return (
    <div>
      <button id="btn" onClick={this.handleAdd}>打豆豆一次</button>
      {
        this.state.count === 4
        ? null
        : <CounterChild initCount={this.state.count}></CounterChild>
      }
    </div>
  )
}

```

### componentDidMount()

* 组件已经挂载到页面中
* 可以进行DOM操作，比如：获取到组件内部的DOM对象
* 可以发送请求获取数据
* 可以通过 `setState()` 修改状态的值
* 注意：在这里修改状态会重新渲染

```JS
componentDidMount() {
  // 此时，就可以获取到组件内部的DOM对象
  console.warn('componentDidMount', document.getElementById('btn'))
}
```

## 组件生命周期 - 运行阶段（Updating）

* 特点：该阶段的函数执行多次
* 说明：每当组件的`props`或者`state`改变的时候，都会触发运行阶段的函数

### componentWillReceiveProps()

* 说明：组件接受到新的`props`前触发这个方法
* 参数：当前组件`props`值
* 可以通过 `this.props` 获取到上一次的值
* 使用：若你需要响应属性的改变，可以通过对比`this.props和nextProps`并在该方法中使用`this.setState()`处理状态改变
* 注意：修改`state`不会触发该方法

```JS
componentWillReceiveProps(nextProps) {
  console.warn('componentWillReceiveProps', nextProps)
}
```

### shouldComponentUpdate()

* 作用：根据这个方法的返回值决定是否重新渲染组件，返回`true`重新渲染，否则不渲染
* 优势：通过某个条件渲染组件，降低组件渲染频率，提升组件性能
* 说明：如果返回值为`false`，那么，后续`render()`方法不会被调用
* 注意：这个方法必须返回布尔值！！！
* 场景：根据随机数决定是否渲染组件

```js
// - 参数：
//   - 第一个参数：最新属性对象
//   - 第二个参数：最新状态对象
shouldComponentUpdate(nextProps, nextState) {
  console.warn('shouldComponentUpdate', nextProps, nextState)

  return nextState.count % 2 === 0
}

```

### componentWillUpdate()

* 作用：组件将要更新
* 参数：最新的属性和状态对象
* 注意：不能修改状态 否则会循环渲染

```js
componentWillUpdate(nextProps, nextState) {
  console.warn('componentWillUpdate', nextProps, nextState)
}
```

### render() 渲染

* 作用：重新渲染组件，与`Mounting`阶段的`render`是同一个函数
* 注意：这个函数能够执行多次，只要组件的属性或状态改变了，这个方法就会重新执行

### componentDidUpdate()

* 作用：组件已经被更新
* 参数：旧的属性和状态对象

```js
componentDidUpdate(prevProps, prevState) {
  console.warn('componentDidUpdate', prevProps, prevState)
}
```

## 组件生命周期 - 卸载阶段（Unmounting）

* 组件销毁阶段：组件卸载期间，函数比较单一，只有一个函数，这个函数也有一个显著的特点：组件一辈子只能执行依次！
* 使用说明：只要组件不再被渲染到页面中，那么这个方法就会被调用（ 渲染到页面中 -> 不再渲染到页面中 ）

### componentWillUnmount()

* 作用：在卸载组件的时候，执行清理工作，比如

* 清除定时器
* 清除`componentDidMount`创建的DOM对象

</details>

<details>
<summary>React state和setState和事件绑定</summary>

## state和setState

* 注意：使用 `setState()` 方法修改状态，状态改变后，React会重新渲染组件
* 注意：不要直接修改`state`属性的值，这样不会重新渲染组件！！！
* 使用：1 初始化`state` 2 `setState`修改`state`

```js
  // -------------- 初始化 state --------------
  this.state = {
    count: props.initCount
  }
}

componentWillMount() {
  // -------------- 修改 state 的值 --------------
  // 方式一：
  this.setState({
    count: this.state.count + 1
  })

  this.setState({
    count: this.state.count + 1
  }, function(){
    // 由于 setState() 是异步操作，所以，如果想立即获取修改后的state
    // 需要在回调函数中获取
  });

  // 方式二：
  this.setState(function(prevState, props) {
    return {
      counter: prevState.counter + props.increment
    }
  })

  // 或者 - 注意： => 后面需要带有小括号，因为返回的是一个对象
  this.setState((prevState, props) => ({
    counter: prevState.counter + props.increment
  }))
}
```

## 组件绑定事件

* 通过React事件机制 `onClick` 绑定
* JS原生方式绑定（通过 `ref` 获取元素）
* 注意：`ref` 是React提供的一个特殊属性
* ref的使用说明：`react ref`

### React中的事件机制 - 推荐

* 注意：事件名称采用驼峰命名法
* 例如：`onClick` 用来绑定单击事件

```js
<input type="button" value="触发单击事件"
  onClick={this.handleCountAdd}
  onMouseEnter={this.handleMouseEnter}
/>
```

### JS原生方式 - 知道即可

* 说明：给元素添加 `ref` 属性，然后，获取元素绑定事件

```js
// JSX
// 将当前DOM的引用赋值给 this.txtInput 属性
<input ref={ input => this.txtInput = input } type="button" value="我是豆豆" />

componentDidMount() {
  // 通过 this.txtInput 属性获取元素绑定事件
  this.txtInput.addEventListener(() => {
    this.setState({
      count:this.state.count + 1
    })
  })
}
```

### 事件绑定中的this

* 通过 `bind` 绑定
* 通过 箭头函数 绑定

### 通过bind绑定

* 原理：`bind`能够调用函数，改变函数内部`this`的指向，并返回一个新函数
* 说明：`bind`第一个参数为返回函数中`this`的指向，后面的参数为传给返回函数的参数

```js
// 自定义方法：
handleBtnClick(arg1, arg2) {
  this.setState({
    msg: '点击事件修改state的值' + arg1 + arg2
  })
}

render() {
  return (
    <div>
      <button onClick={
        // 无参数
        // this.handleBtnClick.bind(this)

        // 有参数
        this.handleBtnClick.bind(this, 'abc', [1, 2])
      }>事件中this的处理</button>
      <h1>{this.state.msg}</h1>
    </div>
  )
}
```

* 在构造函数中使用`bind`

```js
constructor() {
  super()

  this.handleBtnClick = this.handleBtnClick.bind(this)
}

// render() 方法中：
<button onClick={ this.handleBtnClick }>事件中this的处理</button>
```

### 通过箭头函数绑定

* 原理：`箭头函数`中的this由所处的环境决定，自身不绑定this

```js
<input type="button" value="在构造函数中绑定this并传参" onClick={
  () => { this.handleBtnClick('参数1', '参数2') }
} />

handleBtnClick(arg1, arg2) {
  this.setState({
    msg: '在构造函数中绑定this并传参' + arg1 + arg2
  });
}
```

</details>

