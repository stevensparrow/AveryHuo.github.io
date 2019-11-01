---
title: Django 实例 Web Application
categories:
- Python Web
tags: 
- Python
- Note
- Django
- 实例
---

## Preparing

 > Python
 > Django
 > Html
 > css
 > Javascript
 > Databases
 > HeroKu
 > Materialize  
 > Beautiful suite
 > Web scraping


## Starters!

+ 创建conda环境

```
conda create --name codedaddies python=3
```

+ 安装django

```
pip install django
```

+ 创建工程（指定目录下）

```
django-admin startproject codedaddies_list
```

+ 创建APP

```
python manage.py startapp my_app
```

+ 数据库构建

```
python manage.py makemigrations
python manage.py migrate
```

+ Templates文件夹
> 配置在settings中，加入以下：
TEMPLATE_DIR = os.path.join(BASE_DIR, "templates")
> 底部加入:
STATICFILES_DIR = (os.path.join(BASE_DIR, 'static'),)

注：需要在pycharm中设置templates标志

+ APP中新建urls.py
在文件中配置路径表：

```
from . import views


urlpatterns = [
    path('', views.home, name='home'),
]
```


## First Page






