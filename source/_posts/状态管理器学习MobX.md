---
title: 状态管理器学习MobX
date: 2020-03-18 13:30:10
tags: 
- React
---
### Mobx的概念
Mobx的核心原理是通过`action`触发`state`的变化，进而触发state的衍生对象（`computed value` & `Reactions`）。
#### State
1. 定义：在Mobx中，`State`就对应业务的初始状态，通过`observable`方法，可以使这些状态变得可观察。
2. 定义状态并使其可观察的方式：
    - `observable(data)`，支持的data类型有`Object`, `Array`,` Map`；
    - `Obserable.box(value,options?)`对js基本类型进行包装
    - `@observable classProperty = value`给`类属性`添加注解
    - 其他`Obserable.object(value,options?)`、`Obserable.array(value,options?)`、`Obserable.map(value,options?)`
3. 返回类型：当某一数据被`observable`包装后，他返回的其实是被observable包装后的类型(`ObservableArray {...}`、`ObservableMap {...}`、`ObservableObject {...}`)；基本数据返回`ObservaleValue{...}`。
4. 代码：
``` ts
import {observable} from 'mobx';
// 观察数据
var appState = observable({
    timer: 0
});// ObservableObject {...}
const arr= observable(['a','b','c']);// ObservableArray {...}
var num = observable.box(20);
//使用get 方法可以得到原来的值，使用set设置值
num.get();//20
num.set(111);

// 观察类属性
class Todo {
    id = Math.random();
    @observable title = "";
    @observable finished = false;
}
```
#### action
1. 定义：通过`action`改变`state`。使用MobX你可以在代码中显式地标记出动作所在的位置，action函数是对传入的function进行一次包装，使得function中的observable对象的变化能够被观察到，从而触发相应的衍生。
2. 创建方式：
    - `action(fn)`
    - `action(name,fn)`：对fn函数进行包装/装饰，name将被用作调试名。
    - `@action classMethod` 类函数包装
    - `@action(name) classMethod`
    - `@action boundclassMethod = (args) => {body}`
    - `@action.bound boundclassMethod(args){body}` 创建有范围的动作

#### computed
1. 定义：对于依赖`state`的数据而衍生出的数据，可以使用`computed`。你有一个值，该值的结果依赖于`state`，并且该值也需要被`observable`，那么就使用`computed`。计算值自动响应状态变化的值
2. 创建方式：
    - `computed(fn)`
    - `@computed classMethod` 类函数包装
3. 性能优化（与autorun的不同）：如果计算属性依赖的state没改变，或者该计算值没有被其他计算值或响应（reaction）使用，computed便不会运行。在这种情况下，computed处于暂停状态，此时若该计算属性不再被observable。那么其便会被Mobx垃圾回收。

#### autorun
1. 定义：`autorun`也是响应`state`的api。和`computed`类似，只要依赖的值改变时，其都会改变。不同的是，`autorun`没有了`computed`的优化（当然，依赖值未改变的情况下也不会重新运行，但不会被自动回收）。`autorun`通常用来执行一些有副作用的。例如打印日志，更新UI等等。
2. 创建方式：
    - `autorun(fn)`

#### observer
在和Mobx数据有关联的时候，需要给你的React组件加上`@observer`，创建视图，当observable的相关数据发生改变时，视图会自动更新。MobX 会以一种最小限度的方式来更新视图。 
``` ts
import {observer} from 'mobx-react';
// 父子组件传值
class MyState {
  @observable num1 = 0;
  @observable num2 = 100;

  @action addNum1 = () => {
    this.num1 ++;
  };
  @action addNum2 = () => {
    this.num2 ++;
  };
  @computed get total() {
    return this.num1 + this.num2;
  }
}

const newState = new MyState();
// 子组件AllNum
const AllNum = observer((props) => <div>num1 + num2 = {props.store.total}</div>);
// 子组件Main
const Main = observer((props) => (
  <div>
    <p>num1 = {props.store.num1}</p>
    <p>num2 = {props.store.num2}</p>
    <div>
      <button onClick={props.store.addNum1}>num1 + 1</button>
      <button onClick={props.store.addNum2}>num2 + 1</button>
    </div>
  </div>
));

@observer
export default class App extends React.Component {

  render() {
    return (
      <div>
        <Main store={newState} />
        <AllNum store={newState} />
      </div>
    );
  }
}
```

### MobX的要点
1. 定义状态并使其可观察 observable 
2. 创建视图以响应状态的变化 observer
3. 更改状态 action