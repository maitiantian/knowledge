# 目录
* [sys](#sys)
* [os](#os)



# <p align="center">sys</p>

###### [<p align="right">back to top ▲</p>](#目录)

> This module provides access to some variables used or maintained by the interpreter and to functions that interact strongly with the interpreter.

sys模块用来访问由解释器使用或维护的变量和与解释器进行交互的函数。

## sys常用属性/方法

|属性/方法|用途|
|:---|:---|
|sys.argv|命令行参数List，第一个元素是程序本身路径|
|sys.modules|返回系统导入的模块字段，key是模块名，value是模块|
|sys.modules.keys()|返回所有已经导入的模块列表|
|sys.exc_info()|获取当前正在处理的异常类,exc_type、exc_value、exc_traceback当前处理的异常详细信息|
|sys.exit(n)|退出程序，正常退出时exit(0)|
|sys.hexversion|获取Python解释程序的版本值，16进制格式如：0x020403F0|
|sys.version|获取Python解释程序的版本信息|
|sys.maxint|最大的Int值（python3.0中，sys.maxint不存在了，因为int的大小不再受到限制）|
|sys.maxsize|The largest supported length of containers. sys.maxsize can be used as an integer larger than any practical list or string index.|
|sys.maxunicode|最大的Unicode值|
|sys.path|返回模块的搜索路径，初始化时使用PYTHONPATH环境变量的值|
|sys.platform|返回操作系统平台名称|
|sys.stdout|标准输出。sys.stdout.write('hello' + '\n') 等于 print('hello')|
|sys.stdin|标准输入。sys.stdin.readline()会将标准输入全部获取，包括末尾的'\n'，因此用len计算长度时是把换行符'\n'算进去了的；sys.stdin.input()获取输入时返回的结果是不包含末尾的换行符'\n'的。|
|sys.stderr|错误输出|
|sys.exec_prefix|返回平台独立的python文件安装的位置|
|sys.byteorder|本地字节规则的指示器，big-endian平台的值是'big',little-endian平台的值是'little'|
|sys.copyright|记录python版权相关的东西|
|sys.api_version|解释器的C的API版本|

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


# <p align="center">os</p>

###### [<p align="right">back to top ▲</p>](#目录)

> This module provides a portable way of using operating system dependent functionality.

os模块提供了一种方便的使用操作系统函数的方法。

## os常用属性/方法

|属性/方法|用途|
|:---|:---|
|os.name|windows是nt，linux是posix|
|os.remove()|删除文件|
|os.rename()|重命名文件|
|os.walk()|生成目录树下的所有文件名|
|os.chdir()|改变目录|
|os.mkdir()/makedirs()|创建目录/多层目录|
|os.rmdir()/removedirs()|删除目录/多层目录|
|os.listdir()|列出指定目录的文件，不给参数默认输出当前路径下所有文件|
|os.getcwd()|取得当前工作目录|
|os.stat()|查看文件/目录状态信息|
|os.chmod()|改变目录权限|
|os.chown()|改变文件的属主、属组，但需要有足够的权限|
|os.path.basename()|去掉目录路径，返回文件名|
|os.path.dirname()|去掉文件名，返回目录路径|
|os.path.join()|将分离的各部分组合成一个路径名|
|os.path.split()|返回 (dirname(), basename()) 元组|
|os.path.splitext()|返回 (filename, extension) 元组|
|os.path.getatime()\getctime()\getmtime()|分别返回最近访问、创建、修改时间|
|os.path.getsize()|返回文件大小|
|os.path.exists()|是否存在|
|os.path.isabs()|是否为绝对路径|
|os.path.isdir()|是否为目录|
|os.path.isfile()|是否为文件|

