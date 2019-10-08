---
title: Python Note 1
tags: Python,Note
---
# Python杂项

+ ### while结构
 注： """  多行string
![enter description here](/images/1570501535887.png)

+ ### For结构
 * 普通使用
 ![enter description here](./images/1570516202093.png)
 * Use curly braces, 显示变量
![enter description here](./images/1570516527166.png)
 * 使用重复*个数输出字符
 ![enter description here](./images/1570517022147.png)

+ ### List
* 普遍用法
```
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

```
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
> 类似于List，但不可修改
> 
