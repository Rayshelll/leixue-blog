---
title: react相关
date: 2019-08-16 13:18:12
tags: 
- React
categories: 前端学习
---
#### react框架
1. 创建容器，用于接受渲染虚拟DOM元素
``` html
<div id="app"></div>
```
2. 创建虚拟DOM元素
``` jsx
//参数一：创建的标签名；标签二：节点属性；参数三：子节点
const myh1 = React.createElement('h1',{title:'my is a div', id:'myh1'}, 'this h1 content')
//or
const myh1 = <h1 id="myh1" title="my is a div">this h1 content</h1>
```

3. 渲染虚拟DOM元素
``` jsx
React.render(myh1, document.getElementById('app'))
```

<!-- more -->

#### react生命周期
- 组件创建阶段：一辈子只执行一次
    - `componentWillMount()`
    - `render()`
    - `componentDidMount()`
- 组件运行阶段：按需执行，根据props和state的状态改变，有选择性的执行0-n次
    - `componentWillReceiveProps()`
    - `shouldComponentUpdate()`
    - `componentWillUpdate()`
    - `render()`
    - `componentDidUpdate()`
- 组件销毁阶段：一辈子只执行一次
    - `componentWillUnmount()`

#### setState
``` jsx
this.setState({comment: 'Hello'});
```
状态更新可能是异步的：状态中使用了props传过来的值increment，让`setState()`来接受一个函数而不是一个对象。 该函数将接收先前的状态作为第一个参数counter，将此次更新被应用时的`props`做为第二个参数：

``` jsx
//正确的做法
this.setState((prevState, props) => ({
  counter: prevState.counter + props.increment
}));
```
#### 组件
##### 无状态组件
``` jsx 
function Header(props){
           
}
```
使用情况：纯粹的渲染 html 内容，不需要对数据进行判断和处理；要么这个组件所需要的数据，都是来自于上层结构（父组件传递下来的数据，或者 `Redux` 的 `store` 中的数据。
引用props：`props.xx`

##### 有状态组件
``` jsx
class Header extends React.Component(){

}
```
or
``` jsx
class Header extends React.PureComponent(){

}
```
使用情况：要处理组件里的数据
引用props：`this.props.xx`

React中的就提供了一个`PureComponent`的类，当我们的组件继承于它时，组件更新时就会默认先比较新旧属性和状态，从而决定组件是否更新。值得注意的是，PureComponent进行的是浅比较，所以组件状态或属性改变时，都需要返回一个新的对象或数组

#### 受控组件和非受控组件
##### 受控组件
`input`的`value`值必须是我们设置在`constructor`构造函数的state中的值，然后，通过`onChange`触发事件来改变`state`中保存的`value`值，这样形成一个循环的回路影响。`input`中的`value`值通过`state`值获取，`onChange`事件改变state中的`value`值，`input`中的`value`值又从`state`中获取，也可以说是`React`负责渲染表单的组件仍然控制用户后续输入时所发生的变化。

``` jsx
handleChange(e){
    this.setState({
        value: e.target.value
        });
}
<input type="text" value={this.state.value} onChange={this.handleChange} />
```

##### 非受控组件
不需要设置它的`state`属性，而通过`ref`来操作真实的`DOM`。
``` jsx
<input type="text" ref={input => this.textInput = input} />
```
#### 重构：显示和状态分离
用`stateless组件`来负责显示，`class组件`来负责状态和逻辑

#### React 中 keys 的作用是什么？
`Keys` 是 React 用于追踪哪些列表中元素被修改、被添加或者被移除的辅助标识。在 `React Diff` 算法中 React 会借助元素的 Key 值来判断该元素是新近创建的还是被移动而来的元素，从而减少不必要的元素重渲染。此外，React 还需要借助 Key 值来判断元素与本地状态的关联关系，因此我们绝不可忽视转换函数中 Key 的重要性。

### react常见面试题
#### 调用 setState 之后发生了什么？
在代码中调用 setState 函数之后，React 会将**传入的参数对象与组件当前的状态合并**，然后React 会以相对高效的方式根据新的状态构建 React 元素树并且着手重新渲染整个 UI 界面。在 React 得到元素树之后，React 会自动计算出新的树与老树的节点差异，然后根据差异对界面进行最小化重渲染。在差异计算算法中，React 能够相对精确地知道哪些位置发生了改变以及应该如何改变，这就保证了按需更新，而不是全部重新渲染。

#### react 生命周期函数
1. 初始化阶段：
    - getDefaultProps:获取实例的默认属性
    - getInitialState:获取每个实例的初始化状态
    - componentWillMount：组件即将被装载、渲染到页面上
    - render:组件在这里生成虚拟的 DOM 节点
    - componentDidMount:组件真正在被装载之后
2. 运行中状态：
    - componentWillReceiveProps:组件将要接收到属性的时候调用
    - shouldComponentUpdate:组件接受到新属性或者新状态的时候（可以返回 false，接收数据后不更新，阻止 render 调用，后面的函数不会被继续执行了）
    - componentWillUpdate:组件即将更新不能修改属性和状态
    - render:组件重新描绘
    - componentDidUpdate:组件已经更新
3. 销毁阶段：
    - componentWillUnmount:组件即将销毁
    - shouldComponentUpdate 是做什么的，（react 性能优化是哪个周期函数？）
    - shouldComponentUpdate 这个方法用来判断是否需要调用 render 方法重新描绘 dom。因为 dom 的描绘非常消耗性能，如果我们能在shouldComponentUpdate 方法中能够写出更优化的 dom diff 算法，可以极大的提高性能。

#### 为什么虚拟 dom 会提高性能?(必考)
`虚拟 dom `相当于在 js 和真实 dom 中间加了一个缓存，利用 dom diff 算法避免了没有必要的 dom 操作，从而提高性能。
用 JavaScript 对象结构表示 DOM 树的结构；然后用这个树构建一个真正的 DOM 树，插到文档当中当状态变更的时候，重新构造一棵新的对象树。然后用新的树和旧的树进行比较，记录两棵树差异把 2 所记录的差异应用到步骤 1 所构建的真正的 DOM 树上，视图就更新了。

#### react diff 原理（常考，大厂必考）
- 把树形结构按照层级分解，只比较同级元素。
- 给列表结构的每个单元添加唯一的 key 属性，方便比较。
- React 只会匹配相同 class 的 component（这里面的 class 指的是组件的名字）
- 合并操作，调用 component 的 setState 方法的时候, React标记有差异的节点，到每一个事件循环结束, 检查所有标记的节点 component 重新绘制.
- 选择性子树渲染。开发人员可以重写 shouldComponentUpdate 提高 diff 的性能。

#### React 中 refs 的作用是什么？
Refs 是 React 提供给我们的安全访问 `DOM 元素`或者某个组件实例的句柄。

#### 为什么建议传递给 setState 的参数是一个 callback 而不是一个对象
因为 this.props 和 this.state 的更新可能是`异步`的，不能依赖它们的值去计算下一个 state。

#### 应该在 React 组件的何处发起 Ajax 请求
在 React 组件中，应该在 `componentDidMount` 中发起网络请求

#### React 项目用过什么脚手架（本题是开放性题目）
`creat-react-app`

#### 简述 flux 思想
- Flux 的最大特点，就是数据的"单向流动"。
- 用户访问 View
- View 发出用户的 Action
- Dispatcher 收到 Action，要求 Store 进行相应的更新
- Store 更新后，发出一个"change"事件
- View 收到"change"事件后，更新页面

#### 了解 redux 么，说一下 redux 吧
`redux` 是一个应用数据流框架，主要是解决了组件间状态共享的问题，原理是集中式管理，主要有三个核心方法，`action`，`store`，`reducer`工作流程是：
1. view 调用 store 的 dispatch 接收 action 传入 store，reducer 进行 state 操作，view 通过 store 提供的 getState 获取最新的数据；
2. 新增 state,对状态的管理更加明确，通过 redux，流程更加规范了，减少手动编码量，提高了编码效率，同时缺点时当数据更新时有时候组件不需要，但是也要重新绘制，有些影响效率。一般情况下，我们在构建多交互，多数据流的复杂项目应用时才会使用它们

#### redux 有什么缺点
一个组件所需要的数据，必须由父组件传过来，而不能像 flux 中直接从 store 取。
当一个组件相关数据更新时，即使父组件不需要用到这个组件，父组件还是会重新 render，可能会有效率影响，或者需要写复杂的 shouldComponentUpdate 进行判断。

#### flux与redux的不同
Redux 和 Flux 很像。主要区别在于 Flux 有多个可以改变应用状态的 store，在 Flux 中 dispatcher 被用来传递数据到注册的回调事件，但是在 redux 中只能定义一个可更新状态的 store，redux 把 store 和 Dispatcher 合并,结构更加简单清晰

#### react边界错误
React 16 引入了一个新的概念 —— 错误边界
错误边界是一种 React 组件，这种组件可以捕获并打印发生在其子组件树任何位置的 JavaScript 错误，并且，它会渲染出备用 UI，而不是渲染那些崩溃了的子组件树。错误边界在渲染期间、生命周期方法和整个组件树的构造函数中捕获错误。
如果一个 `class` 组件中定义了 `static getDerivedStateFromError() `或 `componentDidCatch()` 这两个生命周期方法中的任意一个（或两个）时，那么它就变成一个错误边界。当抛出错误后，请使用 `static getDerivedStateFromError()` 渲染备用 UI ，使用 `componentDidCatch() `打印错误信息。
