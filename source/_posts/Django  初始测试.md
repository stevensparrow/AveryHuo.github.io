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






