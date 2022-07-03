---
title: 蟒蛇书PartOne--Python基础知识（第三章）
date: 2022-01-10 15:05:05
tags: [Python,蟒蛇书]
categories: [Python]
---



列表应该算是Python的特色了，Python没有提供现成的数组模块（标准库里面提供了array类，可以自己定义），但是提供了更为强大的列表。
<!-- more -->
列表其实和数组很像，定义一系列元素。但是列表还是比数组花里胡哨不少的。

```python
color = ['blue','red','yellow']
print(color) #可以直接对列表元素打印，但是，包括方括号
print(color[-1]) #这样可以直接访问最后一个元素，这种方法其实好用到爆，这样哪怕你不知道列表的长度，依旧可以很快的访问最后一个元素,但是如果列表为空就会报错
```

### 对列表的增删改查

改好说，直接根据下标寻值，重新赋值即可。

尾部增：用append就行

```python
color.append('green')
```

制定位置增：用insert就行

```python
color.insert(0,'teal')
```

不多逼逼，直接删除：用del

```python
del color(0)
```

多逼逼一会儿，带返回值地删除：用pop

```python
popColor = color.pop() #不带参数就是末尾最后一个
popColor = color.pop(0) #制定删除的位置并返回其值
```

上面都是按照址删除值，现在来个按值删除：remove

```python
color.remove('red') #只能删除第一个red
```

### 组织列表

##### 排序算法

Python提供现成的排序算法

```python
color.sort() #按字母顺序排序，排完序之后是无法还原的
color.sort(reverse = true) #来排个反序
```

上面的sort算法会破坏原列表的顺序，为了保护原来的顺序不被破坏，可以使用：sorted

```python
colorSorted = sorted(color) #这样不会破坏color的原来的顺序，排好序的列表放在了colorSorted
```

##### 列表逆置

逆置太简单了：reverse

```python
color.reverse() #简简单单就逆置了，舒舒服服
```

##### 确定列表的长度

```python
length = len(color)
```

