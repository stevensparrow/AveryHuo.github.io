---
title: Python Note 2
tags: Python,Note
---
# Python Note 2

+ ### Function definition
+ As python recommended, left two blank lines after function
```
def greet_user():
    print("GO")
    print("Hi THERE!")


greet_user()
```

+ ### Function parameters
```
def greet_user(name):
    print(f"GO:{name}")
    print("Hi THERE!")


greet_user("John")
greet_user() #Error, no parameter

def greet_user2(first_name,second_name):
    print(f"GO:{first_name} {second_name}")
    print("Hi THERE!")


greet_user2("John","Smith")
greet_user2(second_name="John",first_name="Smith") #使用keyword形式作为参数
```