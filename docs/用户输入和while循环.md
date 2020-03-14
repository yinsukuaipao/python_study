# 用户输入和while循环

## 用户输入input()

```python
name = input("Please enter you name:")
print("Hello, " + name + "!")
```

## Python2.7中获取输入

应使用raw_input()，Python2.7的input()会把用户输入解读为代码，并尝试运行

## while循环

### 语法

```python
num = 1
while num <= 5:
    print(num)
    num += 1

# 1
# 2
# 3
# 4
# 5
```

```python
num = [1,2,2,3]
while 2 in num:
    num.remove(2)

print(num) # [1, 3]
```

### break

退出循环

```python
num = 0
while True:
    num += 1
    if num == 2:
        break

print(num) # 2
```

### continue

结束本次循环

```python
num = 0
while num < 10:
    num += 1
    if num > 2:
        continue
    print(num)

# 1
# 2
```

## for循环

```python
str = ['a','b','c']
for v in str:
    print(v)

#a
#b
#c
```