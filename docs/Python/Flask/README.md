<div style="position: fixed; bottom: 20px; right: 39px; border-radius: 5px; background-color: #797979; z-index: 100;">
    <a href="#flask" style="color: white; border-right: 1px solid white; text-decoration: none; font-size: 14px; font-weight: bold; display: inline-block; padding: 5px 8px; line-height: 20px;">back to top ▲</a>
    <a style="cursor: pointer; color: white; border-right: 1px solid white; text-decoration: none; font-weight: bold; display: inline-block; padding: 5px 8px; line-height: 20px;" onclick="(function(){document.querySelector('.btn.pull-left.js-toolbar-action').click()})()"><i class="fa fa-align-justify"></i></a>
</div>

# Flask

#### Flask程序基本结构
```python
|-flasky
    |-app/ # flask程序一般保存在名为app的包中
        |-templates/
        |-static/
        |-main/
            |-__init__.py
            |-errors.py
            |-forms.py
            |-views.py
        |-__init__.py
        |-email.py
        |-models.py
    |-migrations/ # migrations文件夹包含数据库迁移脚本
    |-tests/ # 单元测试写在tests包中
        |-__init__.py
        |-test*.py
    |-venv/ # venv文件夹包含Python虚拟环境
    |-requirements.txt # 列出所有依赖包，便于在其它电脑中重新生成相同的虚拟环境
    |-config.py # 存储配置
    |-manage.py # 用于启动程序以及其它的程序任务
```

```python
import os

basedir = os.path.abspath(os.path.dirname(__file__))

# Config基类中包含通用配置，子类分别定义专用配置
class Config:
    SECRET_KEY = os.environ.get('SECRET_KEY') or 'hard to guess string'
    # 为了更加灵活安全，某些配置可以从环境变量中导入，
    # 如SECRET_KEY，可在环境中设定，但也要提供一个默认值防止环境中没有定义

    SQLALCHEMY_COMMIT_ON_TEARDOWN = True
    FLASKY_MAIL_SUBJECT_PREFIX = '[Flasky]'
    FLASKY_MAIL_SENDER = 'Flasky Admin <flasky@example.com>'
    FLASKY_ADMIN = os.environ.get('FLASKY_ADMIN')

    @staticmethod
    def init_app(app):
        pass

class DevelopmentConfig(Config):
    DEBUG = True
    MAIL_SERVER = 'smtp.googlemail.com'
    MAIL_POST = 587
    MAIL_USE_TLS = True
    MAIL_USERNAME = os.environ.get('MAIL_USERNAME')
    MAIL_PASSWORD = os.environ.get('MAIL_PASSWORD')
    SQLALCHEMY_DATABASE_URI = os.environ.get('DEV_DATABASE_URL') or 'sqlite:///' + os.path.join(basedir, 'data-dev.sqlite')

class TestingConfig(Config):
    TESTING = True
    SQLALCHEMY_DATABASE_URI = os.environ.get('TEST_DATABASE_URL') or 'sqlite:///' + os.path.join(basedir, 'data-test.sqlite')

class ProductionConfig(Config):
    SQLALCHEMY_DATABASE_URI = os.environ.get('DATABASE_URL') or 'sqlite:///' + os.path.join(basedir, 'data.sqlite')

# 3个子类中，SQLALCHEMY_DATABASE_URI被指定了不同的值，
# 这样程序就可以在不同的配置环境中运行了，每个环境使用不同的数据库

config = {
    'development': DevelopmentConfig,
    'testing': TestingConfig,
    'production': ProductionConfig,

    'default': DevelopmentConfig
}
```

