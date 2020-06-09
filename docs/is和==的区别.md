# is和==的区别

Python中对象包含的三个基本要素，分别是：id(身份标识)、type(数据类型)和value(值)。
is和==都是对对象进行比较判断作用的，但对对象比较判断的内容并不相同。下面来看看具体区别在哪。
==比较操作符和is同一性运算符区别

==是python标准操作符中的比较操作符，用来比较判断两个对象的value(值)是否相等，例如下面两个字符串间的比较：

例1.

```python
>>> a = 'cheesezh'
>>> b = 'cheesezh'
>>> a == b
True
```

is也被叫做同一性运算符，这个运算符比较判断的是对象间的唯一身份标识，也就是id是否相同。通过对下面几个list间的比较，你就会明白is同一性运算符的工作原理：

例2.

```python
>>> x = y = [4,5,6]
>>> z = [4,5,6]
>>> x == y
True
>>> x == z
True
>>> x is y
True
>>> x is z
False
>>>
>>> print id(x)
3075326572
>>> print id(y)
3075326572
>>> print id(z)
3075328140
```

前三个例子都是True，这什么最后一个是False呢？x、y和z的值是相同的，所以前两个是True没有问题。至于最后一个为什么是False，看看三个对象的id分别是什么就会明白了。

下面再来看一个例子，例3中同一类型下的a和b的（a==b）都是为True，而（a is b）则不然。

例3.

```python
>>> a = 1 #a和b为数值类型
>>> b = 1
>>> a is b
True
>>> id(a)
14318944
>>> id(b)
14318944
>>> a = 'cheesezh' #a和b为字符串类型
>>> b = 'cheesezh'
>>> a is b
True
>>> id(a)
42111872
>>> id(b)
42111872
>>> a = (1,2,3) #a和b为元组类型
>>> b = (1,2,3)
>>> a is b
False
>>> id(a)
15001280
>>> id(b)
14790408
>>> a = [1,2,3] #a和b为list类型
>>> b = [1,2,3]
>>> a is b
False
>>> id(a)
42091624
>>> id(b)
42082016
>>> a = {'cheese':1,'zh':2} #a和b为dict类型
>>> b = {'cheese':1,'zh':2}
>>> a is b
False
>>> id(a)
42101616
>>> id(b)
42098736
>>> a = set([1,2,3])#a和b为set类型
>>> b = set([1,2,3])
>>> a is b
False
>>> id(a)
14819976
>>> id(b)
14822256
```

通过例3可看出，只有数值型和字符串型的情况下，a is b才为True，当a和b是tuple，list，dict或set型时，a is b为False。

intern机制就是不管你创建了多少个相同的字符串，在python中都是会指向同一个对象的。这是为了防止你不小心创建了多个相同对象而浪费大量内存甚至会发生挤爆内存的后果。有了这个理解，我们再看看下面例子就容易得出答案了。

例4.

```python
class Person():
    pass
p = Person()
print(type(p) is Person)  # 结果 True
```

为什么上面结果是True呢？这是因为我们之前说过类本身也是个对象，用type()方法会指向该对象，又因为这个类，也就是对象是唯一的，所以结果就是True。