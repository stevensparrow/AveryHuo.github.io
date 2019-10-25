---
title: Django  初始测试
categories:
- Python Web
tags: 
- Python
- Note
- Django
---

### 使用models.py 创建数据库

> 注意事项：
>1、makemigrations 和 migrate 工作原理分别是什么：
makemigrations：根据检测到的模型创建新的迁移。迁移的作用，更多的是将数据库的操作，以文件的形式记录下来，方便以后检查、调用、重做等等。
migrate：使数据库状态与当前模型集和迁移集同步。说白了，就是将对数据库的更改，主要是数据表设计的更改，在数据库中真实执行。例如，新建、修改、删除数据表，新增、修改、删除某数据表内的字段等等。
2、如果不想使用 Django 的 makemigrations 和 migrate 功能，但是不小心执行了这两个命令会发生什么，
首先在该app下建立 migrations目录，并记录下你所有的关于modes.py的改动，比如0001_initial.py，
接着执行migrate的话，这时候会作用到数据库文件，产生对应的表


> 1. 先执行一下迁移
>

> 1. 编辑app里的models.py
如：

```
from django.db import models


class Question(models.Model):
    question_text = models.CharField(max_length=200)
    pub_date = models.DateTimeField('date published')


class Choice(models.Model):
    question = models.ForeignKey(Question, on_delete=models.CASCADE)
    choice_text = models.CharField(max_length=200)
    votes = models.IntegerField(default=0)
```

> 2. 执行生成数据库


```
python manage.py migrate
```







