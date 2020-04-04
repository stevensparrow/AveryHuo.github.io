---
title: Python Note 1
categories:
- Python
tags: 
- Python
- Note
---
# Python Note 1

+ 逻辑运算符的使用：
+ and or not 会将几个值作为False ：0 None "" []

+ 多变量赋值
```python
minValue, maxValue = 10 , 20
```

+ ### while结构
 注： """  多行string
 
```python
n = 0
while n < 5:
	print("""
This is test!
This is test2!
This is test3!
	""")
	n = n + 1
```

+ ### For结构
 * 普通使用
 
 ```python
 for i in range(5):
 	print()
 ```
 * Use curly braces, 显示变量

```python
 for i in range(5):
 	print(f"i:{i}")
 ```
 * 使用重复*个数输出字符

```python
 for i in range(5):
 	print(f"i:{i}"*4)
 ```

+ ### List
* 普遍用法

```python
names = ['John', 'Bob', 'Mosh', 'Sarah', 'Mary']
print(names[2:])  #Print will start from 'Mosh'''
print(names[:])  #Print all'
names[0] = 'Joh' #Change item
print(names)  #output
# 2d list
matrix = [
   [1, 2, 3],
    [4, 5, 6],
    [7, 8, 9]
]
matrix[0][-3] = 20
print(matrix)
```

* 编辑类

```python
numbers = [5,2,1,7]
numbers.insert(-2,20)
numbers.remove(2)
numbers.append(45)
numbers.pop() #remove the last and return it
print(numbers.index(5))
numbers.sort()
numbers.reverse() #get deasc order
if 5 in numbers:
    print(numbers.index(5))
numbers2 = numbers.copy()
numbers.append(45)
print(numbers)
print(numbers2)

#去重复
numbers = [5,20,1,5,7,5,6,4,5]
uniques = []
for i in numbers:
    if i not in uniques:
        uniques.append(i)
print(uniques)
```

+ ### Tuple
+ 类似于List，但不可修改

```python
numbers = (5,20,1,5,7,5,6,4,5)
numbers[0] = 1 #TypeError: 'tuple' object does not support item assignment
```

+ ### Unpacking
+ 映射数组成员

```python
coordinates = (1,2,3)
a = coordinates[0]
b = coordinates[1]
c = coordinates[2]

# use Unpacking feature, unpacking the tuple/list to three variable
x, y, z = coordinates
print(f"{a},{b},{c} <=> {x}, {y}, {z}")
```

+ ### Dictionary

```python
customer = {
    "name": "John",
    "age": 30,
    "is_verified": True
}
print(customer["name"])
# print(customer["Name"]) #KeyError,don't contain
# print(customer["birthdate"])#KeyError,don't contain
print(customer.get("name"))
print(customer.get("Name","Hey")) #Print,with default value:'Hey'
customer["name"] = "AA"
print(customer.get("name"))

#Exercise
input_str = str(input("Phone:"))
digits_map = {
    "1":"One",
    "2":"Two",
    "3":"Three",
    "4":"Four",
}
output = ''
for s in input_str:
    output += digits_map.get(s,"") + " "

print(output)
```
+ [mac]ctrl+cmd+space>> to show emojis