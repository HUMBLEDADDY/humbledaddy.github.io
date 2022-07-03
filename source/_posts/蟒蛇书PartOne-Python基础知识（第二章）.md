---
title: 蟒蛇书PartOne--Python基础知识（第二章）
date: 2022-01-10 14:20:49
tags: [Python,蟒蛇书]
categories: [Python]
---



以前偶尔会写一点Python，现在系统的整理一下啊Python的语言特性。

第一章安装环境，没什么好记录的，便从第二章《变量和简单数据类型》开始。
<!-- more -->
变量名，Python比JavaScript少了“$”，其他的没有什么差别。

> 淦，这蟒蛇书读着读着就觉得过于脑瘫

Python和我熟悉的JavaScript有很多共同之处，都是解释性语言。都是静态类型语言，既在声明变量之时，不明确表示变量的类型，具体的数据类型在赋值和调用时在确定。

> 感觉现在大家对动态静态类型和强弱类型之间的区分不是很明确。



### 字符串

我自认为Python的优秀之处就在于提供了很多实用的小方法。

在字符串这一Part，Python提供了很多现成的小函数：

```python
string.title() #首字母大写
string.upper() #全部大写
string.lower() #全部小写
```

对字符串的拼接也如JavaScript一样方便

```python
first_name = 'ada'
last_name = 'lovelace'
full_name = f"{first_name} {last_name}" #f是farmat的意思
print(f"Hello,{full_name.title()}!") #进一步格式化
```

> f字符串是Python3.6之后才引入的。
>
> 如果是3.5及其之前的版本，写法为
>
> ```python
> full_name = "{} {}".format(first_name, last_name)
> ```

##### 删除空白

对于删除字符串末尾的空白，Python提供了rstrip方法，字符串调用这一方法，可以获得去掉末尾空格的字符串，但是并不会对原本字符串进行更改，需要把得到的字符串重新赋值给原字符串。

```python
favorite_language = 'python '
favorite_language = favorite_language.rstrip()
```

对于开头的空白就用lstrip方法，一样的不赘述。

### 数

Python有一个很舒服的地方，对于乘方操作，可以直接使用两个‘*’号来表示，比什么的sqrt之流要舒服很多。

Python在处理整数和浮点数时并不会很麻烦，Python对浮点数的偏爱毫不掩饰，两个整数相除，哪怕能整除，得到的依然书浮点数。整数和浮点数运算得到的一定是浮点数。

Python数据处理另外一个很舒服的地方就是，可以在数据之间加入 '_'  用于使数据清晰易读。

```python
universe_age = 14_000_000_000
print(universe_age)
```

打印时并不会把下划线打印出来。

##### 常量

Python定义常量和他声明变量的方式一样独特。Python一般情况下，全大写的变量视为常量。