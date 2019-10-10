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

## 分组
```
import re
m = re.search('\w+@(\w+\.)*(\w+)*\.com','aaa@aa.a.com')
if m is not None:
    print(m.group())
else:
    print("none found")
```

## sub() & subn()
```
#使用函数作为参数
def repl_t(txt):
    if txt.group(0) == '-':
        return 'x'
    elif txt.group(0) == '--':
        return '-'
    elif txt.group(0) == '-1':
        return '\"good\"'
m = re.subn('(-{1,2})\d?',repl_t,"d----asf-s-a-123")
print(m)
```

### Regular Expression -> Split()
```
data = (
 'Mountain View, CA 94040',
 'Sunnyvale, CA',
 'Los Altos, 94023',
 'Cupertino 95014',
 'Palo Alto CA',
 )

for d in data:
     v = re.split(r", |(?= (?:\d{5}|[A-Z]{2})) ",d)
     print(v)
```

### 扩展表达式
// 前瞻：
exp1(?=exp2) 查找exp2前面的exp1
// 后顾：
(?<=exp2)exp1 查找exp2后面的exp1
// 负前瞻：
exp1(?!exp2) 查找后面不是exp2的exp1
// 负后顾：
(?<!exp2)exp1 查找前面不是exp2的exp1

