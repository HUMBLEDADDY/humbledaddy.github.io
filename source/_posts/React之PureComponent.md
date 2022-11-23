# React之PureComponent和memo

其实主要的点是在memo,memo是React16.6.0推出的(另外一个主要的功能就是React.lazy())

memo其实就是PureComponent的Functional component版本

PureComponent的逻辑其实就是把props和state进行了一层浅比较,如果改变了,那么就调用render().如果没有或者只是包含的某个属性发生了改变,就不重新渲染,最后的目的其实就是实现性能的优化.

所以只推荐在拥有简单的props和state的时候,才推荐去使用PureComponent,一旦涉及复杂的数据结构,就有可能出现model层已经更新了,但是view层经过浅对比,觉得不用更新

所以就有forceUpdate( )这个函数来强制更新

``` jsx
import React ,{Component,PureComponent} from 'react'
 
class Son extends PureComponent {
    constructor(props){
        super(props)
        this.state = {
           style:{ width:'100px',
            height:'100px',
            background: this.props.color  // props改变 state不会更新
        }}
    }
    render(){
        return(
            <div style = {this.state.style}>
            {console.log('Son render()')}
            </div>
        )
    }
    componentWillReceiveProps(props,state){
        this.forceUpdate()    // 每次传递属性时 都会强制渲染 并忽略shouldComponentUpdate
        if ( props.color === this.props.color ) return false;
        this.setState((pre)=>{
            let newStyle = {...pre.style}
            newStyle.background = props.color
            console.log(props.color)
            return {style:newStyle}
        })
    }
}
 
class Father extends Component {
    constructor(){
        super()
        this.state = {
            color :'pink' 
        }
    }
    changeColor = (color)=>{
        this.setState({
            color:color
        })
    }
    render(){
        return(
            <>
                {console.log('Father render')}
                <button onClick = {this.changeColor.bind(null,'black')}>blcak</button>
                <button onClick = {this.changeColor.bind(null,'pink')}>pink</button>
                <button onClick = {this.changeColor.bind(null,'yellow')}>yellow</button>
                <Son color = {this.state.color}></Son>
            </> 
        )
        
    }
 
}
 
export default Father
```

### Memo其实大差不差

``` jsx

import React from "react";

function Child({seconds}){
    console.log('I am rendering');
    return (
        <div>I am update every {seconds} seconds</div>
    )
};

function areEqual(prevProps, nextProps) {
    if(prevProps.seconds===nextProps.seconds){
        return true
    }else {
        return false
    }

}
export default React.memo(Child,areEqual)
```

### useMemo

有一个问题就是，有时候父组件的某个state更新，导致整个父组件重新render，然后传给子组件的参数由于父组件的重新render导致地址发生了改变

``` jsx
const Child = memo(({data}) =>{
    console.log('child render...', data.name)
    return (
        <div>
            <div>child</div>
            <div>{data.name}</div>
        </div>
    );
})

const Hook =()=>{
    console.log('Hook render...')
    const [count, setCount] = useState(0)
    const [name, setName] = useState('rose')

    const data = {
        name
    }

    return(
        <div>
            <div>
                {count}
            </div>
            <button onClick={()=>setCount(count+1)}>update count </button>
            <Child data={data}/>
        </div>
    )
}
```

例如data重新被定义，所以data的内存地址发生了改变，导致Child组件重新render，但是data本身的值是没有发生改变的，很浪费

React提供了useMemo的方法，render的时候都会把值和上一次的值进行一个比对，如果值发生了变化在触发Child的render函数

``` jsx
const Child = memo(({data}) =>{
    console.log('child render...', data.name)
    return (
        <div>
            <div>child</div>
            <div>{data.name}</div>
        </div>
    );
})

const Hook =()=>{
    console.log('Hook render...')
    const [count, setCount] = useState(0)
    const [name, setName] = useState('rose')

   const data = useMemo(()=>{
        return {
            name
        }
    },[name])
    
    return(
        <div>
            <div>
                {count}
            </div>
            <button onClick={()=>setCount(count+1)}>update count </button>
            <Child data={data}/>
        </div>
    )
}

```

**useCallback的用法（useMemo的语法糖）**

useCallback（x=>console.log(x)，[m]）

等价于

useMemo（()=>(x)=>console.log(x)，[m]）