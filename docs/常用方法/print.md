# print

## 格式化输出

```python
>>> str = "the length of (%s) is %d" %('abc',len('abc'))
>>> print(str)
the length of (abc) is 3
```

python字符串格式化符号:

|符号|描述|
|--|--|
|%c	|格式化字符及其ASCII码|
|%s	|格式化字符串|
|%d	|格式化整数|
|%u	|格式化无符号整型|
|%o	|格式化无符号八进制数|
|%x	|格式化无符号十六进制数|
|%X	|格式化无符号十六进制数（大写）|
|%f	|格式化浮点数字，可指定小数点后的精度|
|%e	|用科学计数法格式化浮点数|
|%E	|作用同%e，用科学计数法格式化浮点数|
|%g	|%f和%e的简写|
|%G	|%f 和 %E 的简写|
|%p |用十六进制数格式化变量的地址|

## str.format()

```python
>>>"{} {}".format("hello", "world")    # 不设置指定位置，按默认顺序
'hello world'
 
>>> "{0} {1}".format("hello", "world")  # 设置指定位置
'hello world'
 
>>> "{1} {0} {1}".format("hello", "world")  # 设置指定位置
'world hello world'
```

可以设置参数：

```python
print("网站名：{name}, 地址 {url}".format(name="菜鸟教程", url="www.runoob.com"))
 
# 通过字典设置参数
site = {"name": "菜鸟教程", "url": "www.runoob.com"}
print("网站名：{name}, 地址 {url}".format(**site))
 
# 通过列表索引设置参数
my_list = ['菜鸟教程', 'www.runoob.com']
print("网站名：{0[0]}, 地址 {0[1]}".format(my_list))  # "0" 是必须的
```

也可以向 str.format() 传入对象：

```python
#!/usr/bin/python
# -*- coding: UTF-8 -*-
 
class AssignValue(object):
    def __init__(self, value):
        self.value = value
my_value = AssignValue(6)
print('value 为: {0.value}'.format(my_value))  # "0" 是可选的
```