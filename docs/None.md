# None

None表示空值，它是一个特殊 Python 对象, None的类型是NoneType

```python
>>> type(None)
<class 'NoneType'>
```

None在 Python 解释器启动时自动创建, 解释器退出时销毁。

在一个解释器进程中只有一个 None 存在, 因为不可能有其他对象会使用 None 已占用的内存(它就是占了个坑)
所以只有: None is None and None == None

* None不支持任何运算也没有任何内建方法
* None和任何其他的数据类型比较永远返回False
* None有自己的数据类型NoneType，不能创建其他 NoneType对象（它只有一个值None）
* None与0、空列表、空字符串不一样
  
```python
>>> None == 0
False
>>> None == ''
False
>>> None == None
True
>>> None == False
False
```

* 可以将None赋值给任何变量，也可以给None值变量赋值
* None是没有像len,size等属性的，要判断一个变量是否为None，直接使用

```python
if a is None:
    pass
```

None可以认为是内存中的唯一一个地址，is的判断的就是地址是否相等，虽然一般情况下==也是可以的，但是==其实是调用的内部函数__eq__，如果__eq__被重载，那就有可能达不到预期。

```python
>>> class test():
...     def __eq__(self,other):
...         return True
... 
>>> t=test()
>>> t is None
False
>>> t == None
True
```
