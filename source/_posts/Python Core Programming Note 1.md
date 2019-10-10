---
title: Python Core Programming Note 1
tags: Python, Note
---

## Regular Expression
![常用表达式](./images/1570674939333.png)
![续](./images/1570674953248.png)

## match() & search()
```
import re
m = re.match('\d','a541')
if m is not None:
    print(m.group())
else:
    print("none found")
	
## none found

import re
m = re.match('\d','a541')
if m is not None:
    print(m.group())
else:
    print("none found")
	
## 5
```
```
import re
m = re.search('..[\d]{1,3}','\na51')
if m is not None:
    print(m.group())
else:
    print("none found")
# . 匹配除\n外的任意字符，其他如\t,\.都可以
```