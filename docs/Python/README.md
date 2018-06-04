# 目录
* [IDLE](#IDLE)
* [运行Python](#运行Python)
* [Python标准文档模板](#Python标准文档模板)
* [可变、不可变数据类型](#可变、不可变数据类型)
* [变量、函数命名](#变量、函数命名)
* [模块](#模块)
* [函数参数](#函数参数)
* [装饰器（Decorator）](#装饰器（Decorator）)

# IDLE
IDLE是Python自带的简单的**集成开发环境**（**IDE**, Integrated Development Environment），是一个可以用来编辑、运行、浏览和调试Python程序的GUI。

> IDLE是IDE的一个官方变形，是为了纪念Monty Python成员Eirc Idle而命名的。

# 运行Python
## 命令行模式
python *.py
## Python交互模式
在系统提示环境（命令行、Win+R）下输入“python”即可开启一个交互的Python会话

**输入一行，执行一行**

* 优点：适合实验语法和测试已写入文件的代码
* 缺点：输入的代码不会保存，要重新执行必须重新输入

退出交互模式：exit()



# Python标准文档模板
```python
#!/usr/bin/env python
# -*- coding: utf-8 -*-

' a test module '

__author__ = 'Michael Liao'
```
第1行和第2行是标准注释，

第1行注释可以让这个.py文件直接在Unix/Linux/Mac上运行，

第2行注释表示.py文件本身使用标准UTF-8编码；

第4行是一个字符串，表示模块的文档注释，任何模块代码的第一个字符串都被视为模块的文档注释；

第6行使用__author__变量把作者写进去。



# 可变、不可变数据类型
***Python，一切皆为对象，一切皆为对象的引用***
* ***可变数据类型：*** list、dict、set
* ***不可变数据类型：*** int、float、string、tuple


* 变量是一个系统表的元素，拥有指向对象的连接的空间
    * 变量名没有类型，类型属于对象
* 对象是分配的一块内存，有足够的空间去表示他们所代表的值
    * 每个对象都有两个标准的头部信息：一个类型标志符去标识这个对象的类型，一个引用的计数器，用来决定是不是可以回收这个对象
* 引用是自动形成的从变量到对象的指针

**id()方法：**
> Return the “identity” of an object. This is an integer (or long integer) which is guaranteed to be unique and constant for this object during its lifetime. Two objects with non-overlapping lifetimes may have the same id()value.

**Python对每个一个对象都提供一个唯一的id值**

* 交互模式下：
    - Python**在一个语句中**对值相同的不可变对象（tuple除外）都解释为了同一个对象
    ```python
    >>> id(1) == id(1)
    True
    >>> id(1000) == id(1000)
    True
    >>> id(10000) == id(10000)
    True
    ```
    - Python对**整型-5~256**都提前构造好了对象，后续所有值在这个范围内的整型都是指向唯一的对象。目的是为了防止经常使用的数字不断的被创建和销毁
    ```python
    >>> a = 1
    >>> b = 1
    >>> id(a) == id(b)
    True
    >>> a = 257
    >>> b = 257
    >>> id(a) == id(b)
    False
    >>> a = -5
    >>> b = -5
    >>> id(a) == id(b)
    True
    >>> a = -6
    >>> b = -6
    >>> id(a) == id(b)
    False
    ```
* 命令行模式下：
    - Python**在一个文件中**对值相同的不可变对象（tuple除外）都解释为同一个对象
    ```python
    a = 257
    b = 257
    print(id(a), id(b), id(257))
    # 199678070416 199678070416 199678070416
    print(a is b, a is 257)
    # True True
    ```
    
```python
>>> x = 257
>>> id(x)
15475528976
>>> x = 258
>>> id(x)
15475529008
>>> if True:
        a = 257
        b = 257
        c = 257
>>> print(id(a), id(b), id(c))
15475529840 15475529840 15475529840
```
***不可变对象，对象的值是不能被改变的：*** id为15475528976的对象的值在没被垃圾回收之前一直都是257，不能改变，如果要把变量x赋值为258，只能将变量x引用的对象从15475528976变为15475529008。

***不可变对象的优点：*** 不管有多少个引用，相同值的对象只占用一块内存（++tuple例外++）。 

***不可变对象的缺点：*** 当需要对变量进行运算从而改变变量的值时，由于是不可变对象的值不能被改变，所以必须创建新的对象，这样就会使得一次次的运算创建了一个个新的对象，不过不再被任何变量引用的对象会被垃圾回收器回收。

```python
>>> if True:
        a = [1, 2, 3]
        b = [1, 2, 3]
        c = [1, 2, 3]
    
>>> print(id(a), id(b), id(c))
15480645448 15480645128 15480645000

# 变量a、b、c引用的对象的id是不同的,其实是创建了三个不同的对象
# 对于可变数据类型的对象来说，值相同的对象也是不同的对象
# 在内存中可能存在多个值相同的对象，它们的id不同
>>> a.append(4)
>>> id(a)
15480645448
>>> a += [2]
>>> id(a)
15480645448
# 对变量a进行操作相当于直接改变了变量a所引用的对象的值
# 对象本身还是那个对象，对象的id不变
>>> a
[1, 2, 3, 4, 2]
```

***可变对象的意思就是说对象的值是可变的，操作变量不会引起新建对象，只是改变了变量所引用的对象的值。***

# 变量、函数命名
## 公开的（public）：
abc、x123、PI

可以被直接引用
## 特殊变量：
\_\_author\_\_ , \_\_name\_\_ , \_\_doc\_\_
可以被直接引用，有特殊用途
## 非公开的（private）：
\_xxx , \_\_xxx
不应该被直接引用(“不应该”但不是“不能”)

# 模块
## 模块导入
```python
try:
    import cStringIO as StringIO
except ImportError:
    import StringIO
```


# 函数参数
## 位置参数（必选参数）
***调用函数时，按照位置顺序传递参数。***
## 默认参数
```python
def enroll(name, gender, age=6, city='Beijing'):
    print('name:', name)
    print('gender:', gender)
    print('age:', age)
    print('city:', city)

# 调用有多个默认参数的函数
# 按顺序提供默认参数
enroll('Bob', 'M', 7)
# 不按顺序提供默认参数时，需要写上参数的名字
enroll('Adam', 'M', city='Tianjin')
```

***默认参数必须指向不变对象:***
```python
def add_end(L=[]):
    L.append('END')
    return L    # L是一个变量，它指向对象[]
>>> add_end()
['END']
>>> add_end()
['END', 'END']
>>> add_end()
['END', 'END', 'END']
```
## 可变参数
```python
def calc(*numbers):
    sum = 0
    for n in numbers:
        sum = sum + n * n
    return sum
```
***可变参数允许你传入0个或任意个参数，这些可变参数在函数调用时自动组装为一个tuple。***
## 关键字参数
```python
def person(name, age, **kw):
    print('name:', name, 'age:', age, 'other:', kw)
```
***关键字参数允许你传入0个或任意个含参数名的参数，这些关键字参数在函数内部自动组装为一个dict。***
## 命名关键字参数
```python
# *, 后面的参数被视为命名关键字参数
def person(name, age, *, city, job):
    print(name, age, city, job)
# 命名关键字参数必须传入参数名，否则将报错
>>> person('Jack', 24, 'Beijing', 'Engineer')
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
TypeError: person() takes 2 positional arguments but 4 were given
# 由于调用时缺少参数名city和job
# Python解释器把这4个参数均视为位置参数
# 但person()函数仅接受2个位置参数

# 如果函数定义中已经有了一个可变参数，后面的命名关键字参数就不需要特殊分隔符 *,
def person(name, age, *args, city, job):
    print(name, age, args, city, job)
    
# 命名关键字参数可以有缺省值，从而简化调用
def person(name, age, *, city='Beijing', job):
    print(name, age, city, job)
```

***参数定义的顺序必须是：位置参数（必选参数）、默认参数、可变参数和关键字参数。***
```python
def func(a, b, c=0, *args, **kw):
    print('a =', a, 'b =', b, 'c =', c, 'args =', args, 'kw =', kw)
```

# 装饰器（Decorator）
* 实质：是一个返回函数的高阶函数
* 参数：要装饰的函数名（并非函数调用）
* 返回：是装饰完的函数名（也非函数调用）
* 作用：为已经存在的对象添加额外的功能
* 特点：不需要对对象做任何的代码上的变动

```python
def decorator(func):
    def wrapper(*args, **kw):
        # do something here
        return func(*args, **kw)    # 执行func，并返回func的返回结果
    return wrapper

# 带参数的decorator
def decoratorWithArg(arg):
    def decorator(func):
        def wrapper(*args, **kw):
            # do something with arg here
            return func(*args, **kw)
        return wrapper
    return decorator
```
***@语法糖***
```python
@decorator
def func():
    pass
# 相当于func = decorator(func)
```