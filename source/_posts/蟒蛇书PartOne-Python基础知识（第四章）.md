---
title: 蟒蛇书PartOne--Python基础知识（第四章）
date: 2022-01-10 16:10:09
tags: [Python,蟒蛇书]
categories: [Python]
---

# Python--基础知识（第四章-操作列表）

```python
magicians = ['alice','david','carolina']
for magician in magicians:
    print(magician)
```

简简单单的一个for循环

> 蟒蛇书这一Part能讲两页纸我也是服了

### 缩进

到了Python比较奇特的一个点——缩进

Python没有使用大部分语言所习惯的大括号来标记代码块，而是使用了缩进来表示代码块。

> 我一直觉得这是一种聪明的做法，不仅是开发者不用去纠结括号的对应，还能使得代码的可读性更高。

另外，Python对于不必要的缩进会报错。应当只缩进应当缩进的代码。

### 创建数值列表

##### range()

range()用来生成一系列的数据，

> 冷知识，range(1,5)，不会包含5

##### list()

可以用list()来把range()生成的一系列数据转化为列表

```python
numbers = list(range(0,5))
```

range()还可以加入第三个参数用来表示步长

```python
even_nums = list(range(2,11,2)) #2,4,6,8,10
```

range()可以有很多特别好用的技巧，比如获得1-10的平方列表

```python
squares = []
for value in range(1,11):
	square = value ** 2
	squares.append(square) #可以简写为squares.append(value ** 2)
print(square)
```

##### 统计学层面

Python对列表提供很方便的方法

min(list),max(list),sum(list)

> 看名字就应该知道啥意思                                                                                                                                                                                                                                                                                                                                                                                                                             

##### 列表解析

其实就是把for循环和创建新元素的代码合并在一起。比如说上面的求平方的算法，也可以简写成一行：

```python
squares = [value ** 2 for value in range(1,11)]
print(squares)
```

> 我个人还是很欣赏这种写法的，倒不是简短，简短肯定不是评价代码好坏的标准，真正的标准应该是一目了然

### 使用列表的一部分

Python在对列表(数组)的处理上和JS类似，都提供了很多现成的好用的方法

##### 切片

Python可以对于列表提供直接以下标来划分局部的方法：

```python
players = ['charles','martina','michael','florence','eli']
print(players[0:3])
```

这样就能直接划分出前三个元素（注意不是四个，差一行为），头尾下标缺省就是列表头和列表尾。

##### 遍历切片

上述的切片也可以应用于循环之中

```python
for player in players[:3]:
	print(player.title()) #会输出前三位
```

##### 复制列表

用一个缺省起始索引和终止索引的的切片直接完成列表的复制

```python
my_foods = ['pizza','falafel','carrot cake']
friend_foods = my_foods[:] #这样的写法真的很有意思
```

而且这样的复制是深度复制，浅复制直接复制就行，不需要使用切片

```python
friend_foods = my_foods
```

### 元组

不可变的列表就是元组：

元组使用括号来标识，定义一个元组之后，就像列表一样用下标去访问。

```python
dimensions = (200,50)
print(dimensions[0])
print(dimensions[1])
```

Python不支持对元组元素的修改，否则会报错。

> 有一说一，元组其实并不是用圆括号标识，而是用逗号标识，如果元组只有一个元素，则要写成这种形式：
>
> ```python
> my_t = (3,)
> ```
>
> 不过只有一个元素的元组其实没有什么意义。

##### 元组的遍历

可以像遍历列表一样的对元组的进行遍历，没啥特殊的点，不赘述。

##### 修改元组变量

虽然修改元组的元素是违法的，但是可以重新定义整个元组来达到修改元组变量的目的

```python
dimensions = (200,50)
dimensions = (400,100)
```

