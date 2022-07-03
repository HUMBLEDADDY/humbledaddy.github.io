---
title: 红宝书重读笔记之第三章Part.2
date: 2022-04-28 15:32:15
tags: [JavaScript,前端,红宝书]
categories: [前端,JavaScript]
---
第三章其实还是有很多有意思的东西的，特别是相比于第四版加入了很多ES6特性的东西，开个PART2，happy一下🙋‍♂️

#### Symbol类型
Symbol就是ES6新加的数据类型.有一点很有意思,不知道为什么我总是认为Symbol是对象属性,但是其实Symbol是原始类型.🤷‍♂️  
<!-- more -->
Symbol引用最主要的作用就是保证一个对象属性是唯一标识符,不会有属性冲突的危险.  
听起来其实就是私有属性那股味道,但是其实Symbol就是用来创作唯一记号的.  
```JavaScript
let sym = Symbol();
let sym2 = Symbol();

let sym3 = Symbol('czx');
let sym4 = Symbol('czx');

console.log(sym == sym2);//false
console.log(sym3 == sym4);//false
```
##### Symbol没有包装对象
虽然Symbol是原始值,但是Symbol并不似其他的原始值一样,具有包装对象
> 包装对象就是用Boolean或者String之类的,函数本身就是一个构造函数,可以使用new关键字一起使用创建一个具有初始值的对象.
> ```JavaScript
> let myBoolean = new Boolean();
> console.log(typeof myBoolean);//"object"
>
> let mySymbol = new Symbol();// TypeError: Symbol is not a constructor
>```
>如果你要完成一些很稀奇古怪的需求,确实也可以解决,用一个Object去包装就好了.

##### 全局符号注册表
Symbol.for(key)方法,觉得这个方法还是很精彩的.  
第一次使用key,直接返回一个新的符号,并且添加到注册表里面.  
但是如果是发现注册表里面已经存在这个key,就直接返回key本身.但是需要注意的是Symbol和Symbol.for()就算key相同,创建出来的Symbol也不相同.  
Symbol.for(key)的key只支持字符串.传给key的任何值都会被转化为字符串.  
Symbol还有一个keyFor()方法来检验Symbol对象的key
```JavaScript
const mySymbol = Symbol.key('mobius');
console.log(Symbol.keyFor(mySymbol));//mobius
//这个方法对Symbol('mobius')这样的普通符号是无效的.
```

##### Symbol作为对象的属性值使用
```JavaScript
  const s1 = Symbol('m1'),
      s2 = Symbol('m2'),
      s3 = Symbol('m3');
  let o1 = {
      's1': 'string s1 val',
      [s1]: 'm1 val'
  };
  console.log(Object.getOwnPropertyNames(o1));
  //['s1']
  console.log(Object.getOwnPropertySymbols(o1));
  //[Symbol(m1)]
  console.log(Object.getOwnPropertyDescriptors(o1));
  //{s1: {…}, Symbol(m1): {…}}
  console.log(Reflect.ownKeys(o1));
  //['s1', Symbol(m1)]
```

#### Symbol常用内置符号(待完成)
其实这个只是Symbol里面的一个内容,ES6引入了一批常用内置符号,用于暴露语言内部行为.  
我一直觉得这块不太好理解,把这部分重要度提上去.  
首先所有的内置符号属性都是不可写,不可枚举,不可配置的.   

---
### Object类型
老生常谈,对象就是一些功能和数据的集合.  
单纯的Object其实也没有什么有意思的点,结合后面的原型链才有意思.  

### 操作符
很简单,很基础,简单记录一下
一元操作符
```JavaScript
++a, a++//先自加在运算,先运算再自加
```
可以用‘=’‘-’来做快速的类型转换.  
```JavaScript
num>>1//有符号右移
num<<<1//无符号左移
```
```JavaScript
!//逻辑非
&&//逻辑与
||//逻辑或
```
ES7加入了一个指数操作符,以前都是用Math.pow()
```JavaScript
let a = 2;
a = a ** 2;
```
比较操作符  
有一点其实会很有意思就是,再上一个part说过,对于数字来说,0和NaN会转化为false,所以
```JavaScript
if(2){
  console.log('true')
}//是判定为真的.
```
但是在相等操作符和不相等操作转化中,总是把true和false转化为对应的1和0,所以:
```JavaScript
2 == true//fasle
```
很奇葩,也很恶心人.  
相等/不相等运算符转化有五条规则:
* true/false->1/0
* string == number,会把string->number
* object == anything,object->object.valueOf()
* ```null == undefined```
* null,undefined是不能转化为其他的类型的  

然后就是全等和不全等,就是单纯的不转化,要求类型也相同.  

---

### 语句
#### if语句
<p style="  color: white;
            background-color: #c3272b;
            width: fit-content;
            padding: 5px;
            font-size: 1rem;
            font-weight: bolder;
            text-transform: uppercase;
            display: inline-block;">pass</p>🙋‍♂️
#### do-while语句
<p style="  color: white;
            background-color: #c3272b;
            width: fit-content;
            padding: 5px;
            font-size: 1rem;
            font-weight: bolder;
            text-transform: uppercase;
            display: inline-block;">pass</p>🙋‍♂️
#### while语句
<p style="  color: white;
            background-color: #c3272b;
            width: fit-content;
            padding: 5px;
            font-size: 1rem;
            font-weight: bolder;
            text-transform: uppercase;
            display: inline-block;">pass</p>🙋‍♂️
#### for语句
<p style="  color: white;
            background-color: #c3272b;
            width: fit-content;
            padding: 5px;
            font-size: 1rem;
            font-weight: bolder;
            text-transform: uppercase;
            display: inline-block;">pass</p>🙋‍♂️
#### for-in语句

