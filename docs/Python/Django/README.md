<div style="position: fixed; bottom: 20px; right: 39px; border-radius: 5px; background-color: #797979; z-index: 100;">
    <a href="#目录" style="color: white; border-right: 1px solid white; text-decoration: none; font-size: 14px; font-weight: bold; display: inline-block; padding: 5px 8px; line-height: 20px;">back to top ▲</a>
    <a href="javascript:void(0)" style="color: white; border-right: 1px solid white; text-decoration: none; font-weight: bold; display: inline-block; padding: 5px 8px; line-height: 20px;" onclick="(function(){document.querySelector('.btn.pull-left.js-toolbar-action').click()})()"><i class="fa fa-align-justify"></i></a>
</div>

# Django



Django是用Python写的一个Web框架包。

## Django特点
* #### 强大的数据库功能
    拥有强大的数据库操作接口（QuerySet API），如需要也能执行原生SQL；
* #### 自带强大后台
    几行简单的代码就让你的网站拥有一个强大的后台，轻松管理内容；
* #### 优雅的网址
    用正则匹配网址，传递到对应函数，随意定义；
* #### 模板系统
    强大，易扩展的模板系统，设计简易，代码，样式分开设计，更容易管理；

    注：前后端分离时，也可以用Django开发API，完全不用模板系统
* #### 缓存系统
    与Memcached，Redis等缓存系统联用，更出色的表现，更快的加载速度；
* #### 国际化
    完全支持多语言应用，允许定义翻译的字符，轻松翻译成不同国家的语言。



## Django项目结构

* #### urls.py
    网址入口，关联到对应的views.py中的一个函数（或者generic类），访问网址就对应一个函数；
* #### views.py
    处理用户发出的请求，从urls.py中对应过来, 通过渲染templates中的网页可以将显示内容，比如登陆后的用户名，用户请求的数据，输出到网页；
* #### models.py
    与数据库操作相关，存入或读取数据时用到这个，当然用不到数据库的时候 你可以不使用；
* #### forms.py
    表单，用户在浏览器上输入数据提交，对数据的验证工作以及输入框的生成等工作，当然你也可以不使用；
* #### templates文件夹
    views.py中的函数渲染templates中的Html模板，得到动态内容的网页，当然可以用缓存来提高速度；
* #### admin.py
    后台，可以用很少量的代码就拥有一个强大的后台；
* #### settings.py
    Django的配置文件，配置DEBUG的开关，静态文件的位置等。


## Django基本命令

* #### 新建一个Django project
    ```python
    django-admin.py startproject project_name
    # 如果报错，尝试用django-admin代替django-admin.py
    ```
* #### 新建app
    ```python
    # 先进入项目目录
    python manage.py startapp app_name
    # django-admin.py startapp app_name
    ```
* #### 创建数据库表/更改数据库表或字段
    ```python
    # 1. 创建更改的文件
    python manage.py makemigrations
    # 2. 将生成的py文件应用到数据库
    python manage.py migrate
    ```
    这种方法可以在数据库中创建与models.py代码对应的表，不需要自己手动执行SQL。
* #### 使用开发服务器
    开发时使用，由于性能问题，建议只用来测试，不要用在生产环境。一般修改代码后会自动重启，方便调试和开发。
    ```python
    python manage.py runserver
    # 提示端口被占用时可以用其它端口
    python manage.py runserver 8001
    python manage.py runserver 9999
    
    # 监听机器所有可用IP（电脑可能有多个内网IP或多个外网IP）
    python manage.py runserver 0.0.0.0:8000
    # 如果是外网或者局域网上其他电脑查看开发服务器
    # 可以访问对应的IP加端口，比如http://172.16.20.2:8000
    ```
* #### 清空数据库
    ```python
    python manage.py flush
    ```
    此命令会询问是yes还是no, 选择yes会把数据全部清空掉，只留下空表。
* #### 创建超级管理员
    ```python
    python manage.py createsuperuser
    # 按照提示输入用户名和对应的密码，邮箱可以留空
    # 修改用户密码可以用：
    python manage.py changepassword username
    ```
* #### 导出/导入数据
    ```python
    # 导出
    python manage.py dumpdata appname > appname.json
    # 导入
    python manage.py loaddata appname.json
    ```
* #### Django项目环境终端
    ```python
    python manage.py shell
    ```
    可以在这个shell里面调用当前项目的models.py中的API，对于操作数据，还有一些小测试非常方便。
* #### 数据库命令行
    ```python
    python manage.py dbshell
    ```
    Django会自动进入在settings.py中设置的数据库，如果是MySQL或postgreSQL，会要求输入数据库用户密码。
* #### 更多命令
    输入python manage.py可以看到详细的列表。