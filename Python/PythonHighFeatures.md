# 切片 Slice 

根据索引取元素（list，tuple，string）

格式：`L[startIndex : endIndex]` 

从索引startIndex开始取，直到索引endIndex截止，不包括索引endIndex

L[:3] ；如果第一个索引是0，还可以省略

支持倒数切片

###### 复制功能 [:]

复制list或者tuple

# 迭代 Iteration 

如果给定一个list或tuple，我们可以通过`for`循环来遍历这个list或tuple，这种遍历我们称为迭代（Iteration）。

在Python中，迭代是通过`for ... in`来完成的

因为dict的存储不是按照list的方式顺序排列，所以，迭代出的结果顺序很可能不一样。

默认情况下，dict迭代的是key。如果要迭代value，可以用`for value in d.values()`，如果要同时迭代key和value，可以用`for k, v in d.items()`。

如何判断一个对象是可迭代对象呢？方法是通过collections模块的Iterable类型判断： ` isinstance(123, Iterable) # 整数是否可迭代`

Python内置的`enumerate`函数可以把一个list变成索引-元素对，这样就可以在`for`循环中同时迭代索引和元素本身： 

```python
for i, value in enumerate(['A', 'B', 'C']):
     print(i, value)
```



# 列表生成式 List Comprehensions 

`[ 表达式（item的规则） for循环 <for循环> <if条件判断>]`



` [x * x for x in range(1, 11)]` ==>>  [1, 4, 9, 16, 25, 36, 49, 64, 81, 100]

`[x * x for x in range(1, 11) if x % 2 == 0]` ==>>  [4, 16, 36, 64, 100]

`[m + n for m in 'ABC' for n in 'XYZ']`  ==>>  ['AX', 'AY', 'AZ', 'BX', 'BY', 'BZ', 'CX', 'CY', 'CZ']



`for`循环其实可以同时使用两个甚至多个变量，比如`dict`的`items()`可以同时迭代key和value： ` [k + '=' + v for k, v in d.items()]`  ==>>   ['y=B', 'x=A', 'z=C']



# 生成器 generator 

要创建一个generator，有很多种方法。第一种方法很简单，只要把一个列表生成式的`[]`改成`()`，就创建了一个generator： 

`( 表达式（item的规则） for循环 <for循环> <if条件判断>)`

打印generator的元素

1.通过`next()`函数获得generator的下一个返回值   next(g)

2.for循环 for n in g:



第二种方法：

比如，著名的斐波拉契数列（Fibonacci），除第一个和第二个数外，任意一个数都可由前两个数相加得到：

1, 1, 2, 3, 5, 8, 13, 21, 34, ...

斐波拉契数列用列表生成式写不出来，但是，用函数把它打印出来却很容易：

```python
def fib(max):
    n, a, b = 0, 0, 1
    while n < max:
        print(b)
        a, b = b, a + b
        n = n + 1
    return 'done'
```

上面的函数和generator仅一步之遥。要把`fib`函数变成generator，只需要把`print(b)`改为`yield b`就可以了：

```
def fib(max):
    n, a, b = 0, 0, 1
    while n < max:
        yield b
        a, b = b, a + b
        n = n + 1
    return 'done'
```

这就是定义generator的另一种方法。如果一个函数定义中包含`yield`关键字，那么这个函数就不再是一个普通函数，而是一个generator：



# 迭代器

这些可以直接作用于`for`循环的对象统称为可迭代对象：`Iterable`。

可以使用`isinstance()`判断一个对象是否是`Iterable`对象：



而生成器不但可以作用于`for`循环，还可以被`next()`函数不断调用并返回下一个值，直到最后抛出`StopIteration`错误表示无法继续返回下一个值了。

可以被`next()`函数调用并不断返回下一个值的对象称为迭代器：`Iterator`。

可以使用`isinstance()`判断一个对象是否是`Iterator`对象：



凡是可作用于`for`循环的对象都是`Iterable`类型；

凡是可作用于`next()`函数的对象都是`Iterator`类型，它们表示一个惰性计算的序列；

集合数据类型如`list`、`dict`、`str`等是`Iterable`但不是`Iterator`，不过可以通过`iter()`函数获得一个`Iterator`对象。