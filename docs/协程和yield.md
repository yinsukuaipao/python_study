# 协程和yield

## 协程

函数内，在赋值运算符的右边

```python
def receiver():
    print("Ready to receive")
    while True:
        n = (yield)
        print("Got %s" % n)
```

以这种方式使用yield的函数成为协程，使用时，先用next函数启动协程，程序就会运行到yield这里等待，然后用send函数向协程发送消息，此时yield就会返回，返回值就是send发送的消息，然后程序会运行到下一个yield，继续等待。

```python
>>> def receiver():
...     print("Ready to receive")
...     while True:
...             n = (yield)
...             print("Got %s" % n)
... 
>>> r = receiver()
>>> r
<generator object receiver at 0x106b76bd0>
>>> r.send(1)
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: can't send non-None value to a just-started generator
>>> r.next()
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
AttributeError: 'generator' object has no attribute 'next'
>>> r.__next__() # 或者 next(r)
Ready to receive
>>> r.send(1)
Got 1
>>> r.send(2)
Got 2
>>> r.send("Hello")
Got Hello
```

用**close**关闭协程，会引发协程内部的（yield）GeneratorExit异常，如果此时调用send函数，则会返回StopIteration异常，注意StopIteration异常不是在协程yield处，而是在send调用处

```python
>>> def receiver():
...     print("Ready to receive")
...     try:
...         while True:
...             n = (yield)
...             print("Got %s" % n)
...     except GeneratorExit:
...         print("Receiver done")
... 
>>> r = receiver()
>>> next(r)
Ready to receive
>>> r.close()
Receiver done
>>> r.send(1)
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
StopIteration
```

用throw(exctype [, value [, tb]])方法在协程内部引发异常，在yield语句处。其中exctype为异常类型，value为异常值，tb为跟踪对象

```python
>>> def receiver():
...     print("Ready to receive")
...     try:
...         while True:
...             n = (yield)
...             print("Got %s" % n)
...     except RuntimeError:
...         print("RuntimeError")
... 
>>> r = receiver()
>>> next(r)
Ready to receive
>>> r.send(1)
Got 1
>>> r.throw(RuntimeError, "Throw Error") # 这里不仅协程内部出现error，而且
RuntimeError
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
StopIteration
>>> r.send(2)
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
StopIteration
```