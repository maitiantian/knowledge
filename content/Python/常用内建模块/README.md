# 目录
* [sys](#sys)



# <p align="center">sys</p>

###### [<p align="right">back to top ▲</p>](#目录)

sys模块提供了一系列有关Python运行环境的变量和函数。

* ### sys.argv

用于获取当前正在执行的命令行命令的参数列表(list)。

|变量|解释|
|:---|:---|
|sys.argv[0]|当前程序名|
|sys.argv[1]|第一个参数|
|sys.argv[0]|第二个参数|

参考代码：

```python
# encoding: utf-8
# filename: argv_test.py
import sys
# 获取脚本名字
print 'The name of this program is: %s' %(sys.argv[0])
# 获取参数列表
print 'The command line arguments are:'
for i in sys.argv:
    print i
# 统计参数个数
print 'There are %s arguments.'%(len(sys.argv)-1)
```

运行结果：

```
E:\p>python argv_test.py arg1 arg2 arg3
The name of this program is: argv_test.py
The command line arguments are:
argv_test.py
arg1
arg2
arg3
There are 3 arguments.
```

* ### sys.platform

获取当前执行环境的平台，win32表示Windows 32bit操作系统，linux2表示是linux平台。

```python
# linux 
>>> import sys
>>> sys.platform
'linux2'

# windows
>>> import sys
>>> sys.platform
'win32'
```

* ### sys.path

目录列表，模块搜索路径。
```python
>>>import sys
>>>sys.path
# 交互环境下sys.path第一个路径是一个空项，对应当前目录。
['', 
'C:\\Python\\Python36\\python36.zip', 
'C:\\Python\\Python36\\DLLs', 
'C:\\Python\\Python36\\lib', 
'C:\\Python\\Python36', 
'C:\\Python\\Python36\\lib\\site-packages', 
'C:\\Python\\Python36\\lib\\site-packages\\win32', 
'C:\\Python\\Python36\\lib\\site-packages\\win32\\lib', 
'C:\\Python\\Python36\\lib\\site-packages\\Pythonwin']

# foo.py
import sys
print(sys.path)

# 运行
E:\MyProjects\PycharmProjects\bao>python foo.py
['E:\\MyProjects\\PycharmProjects\\bao', 
'C:\\Python\\Python36\\python36.zip', 
'C:\\Python\\Python36\\DLLs', 
'C:\\Python\\Python36\\lib', 
'C:\\Python\\Python36', 
'C:\\Python\\Python36\\lib\\site-packages', 
'C:\\Python\\Python36\\lib\\site-packages\\win32', 
'C:\\Python\\Python36\\lib\\site-packages\\win32\\lib', 
'C:\\Python\\Python36\\lib\\site-packages\\Pythonwin']
```

* ### sys.builtin_module_names

返回一个tuple，包含内建模块的名字。

```python
>>>import sys
>>>sys.builtin_module_names
('_ast', '_bisect', '_blake2', '_codecs', '_codecs_cn', '_codecs_hk', 
'_codecs_iso2022', '_codecs_jp', '_codecs_kr', '_codecs_tw', '_collections', 
'_csv', '_datetime', '_functools', '_heapq', '_imp', '_io', '_json', '_locale', 
'_lsprof', '_md5', '_multibytecodec', '_opcode', '_operator', '_pickle', 
'_random', '_sha1', '_sha256', '_sha3', '_sha512', '_signal', '_sre', '_stat', 
'_string', '_struct', '_symtable', '_thread', '_tracemalloc', '_warnings', 
'_weakref', '_winapi', 'array', 'atexit', 'audioop', 'binascii', 'builtins', 
'cmath', 'errno', 'faulthandler', 'gc', 'itertools', 'marshal', 'math', 'mmap', 
'msvcrt', 'nt', 'parser', 'sys', 'time', 'winreg', 'xxsubtype', 'zipimport', 'zlib')
```

代码示例：

```python
# find_module.py
# encoding: utf-8

import sys
# print sys.builtin_module_names
def find_module(module):
    if module in sys.builtin_module_names:
        print module," => ","__builtin__"
    else:
        print module,"=> ",__import__(module).__file__

find_module('os')
find_module('sys')
find_module('strop')
find_module('zlib')
find_module('string')

# 运行结果：
os =>  E:\Python27\lib\os.pyc
sys  =>  __builtin__
strop  =>  __builtin__
zlib  =>  __builtin__
string =>  E:\Python27\lib\string.pyc
```

* ### sys.exit(n)

调用sys.exit(n)可以中途退出程序，当参数非0时，会引发一个SystemExit异常，从而可以在主程序中捕获该异常。

```python
# encoding: utf-8
import sys
print 'running...'
try:
    sys.exit(1)
except SystemExit:
    print 'SystemExit exit 1'

print 'exited'

# 运行结果：
running...
SystemExit exit 1
exited
```
