# Redux学习

React使用的状态管理容器，对标Vuex2

## Action

action其实就是一个简单的JavaScript对象，只是描述应用程序中发生了什么样的事件。

一个type描述action要干啥，一般协作“域/事件名称”。而像是其他的附加信息就放在payload里面

```js
const addTodoAction = {
  type: 'todos/todoAdded',
  payload: 'Buy milk'
}
```

## Action Creator

action creator其实就是一个返回action对象的一个函数，一个个自己手撕太不雅观，写个函数，动态给payload赋值：

```js
const addTodo = text => {
  return {
    type: 'todos/todoAdded',
    payload: text
  }
}
```

## Reducer

一个函数，接受state和action，然后生成新的state,(state,action) => newState

* reducer只能使用state和action来计算新的状态值
* 禁止直接修改state，只能对复制的值来进行不可变更新
* 禁止使用异步，或者随机值，或者其他“副作用”的代码 

## Store

当前 Redux 应用的 state 存在于一个名为 **store** 的对象中。

store 是通过传入一个 reducer 来创建的，并且有一个名为 `getState` 的方法，它返回当前状态值：

```js
import { configureStore } from '@reduxjs/toolkit'

const store = configureStore({ reducer: counterReducer })

console.log(store.getState())
// {value: 0}
```

## Dispatch

更新store的唯一办法，调用store.dispatch()传入一个action对象，store 将执行所有 reducer 函数并计算出更新后的 state，调用 `getState()` 可以获取新 state。而store.dispatch()是view层面发出Action的唯一办法。

```js
store.dispatch({ type: 'counter/increment' })

console.log(store.getState())
// {value: 1}
```

配合上Action Creator，写出的代码很舒服：

```js
store.dispatch(addTodo('Learn Redux'));
```

## Subscribe

监听State的变化，一旦State发生改变就自动执行这个函数

```js
import { createStore } from 'redux';
const store = createStore(reducer);

store.subscribe(listener);
```

对应的,如果在listener的位置放上React组件的render函数或者setState方法,就能实现视图层的自动渲染.

既然监听就会有解除监听(不然就有内存溢出的风险),Subsribe的处理方法和Hook中的useEffect有异曲同工之妙，都是返回一个函数，调用这个函数就可以接触监听。

## Reducer的拆分

目前的理解跟Vuex分module的思路差不多，整个应用的state靠一个reducer维护显然是不太现实的，所以就涉及拆分，拆分成不同的函数，不同的函数处理不同属性，最后合并成一个大的Reducer就行了

```js
const chatReducer = (state = defaultState, action = {}) => {
  return {
    chatLog: chatLog(state.chatLog, action),
    statusMessage: statusMessage(state.statusMessage, action),
    userName: userName(state.userName, action)
  }
};
```

Redux提供一个combineReducers，用于组合拆分出来的Reducer，只要定义各个子函数，然后使用这个方法，将它们合成一个大的Reducer。

```js
import { combineReducers } from 'redux';

const chatReducer = combineReducers({
  chatLog,
  statusMessage,
  userName
})

export default todoApp;
```

## 中间件

有时候我们的Reducer操作会涉及异步操作，所以我们就需要一个新的工具那就是中间件

#### 中间件的概念

如果要在Redux里面添加中间件，Rudcer不行，View不行，Action也不行，所以只剩下dispatch是可行的

``` jsx
let next = store.dispatch;
store.dispatch = function dispatchAndLog(action) {
  console.log('dispatching', action);
  next(action);
  console.log('next state', store.getState());
}
```

