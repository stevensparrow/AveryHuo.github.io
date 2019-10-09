---
title: Python Note 3
tags: Python, Note
---
# Python Note 3

+ ### Classes
+ Use Pacal naming convertion,not like variables/function use lower cases and underscore connection.
+ Basic usage:
```
class Point:
	def draw(self):
		print("draw")

	def print(self):
		print("this is point")


point1 = Point()
point1.x = 5
point1.draw()
print(point1.x)
```

+ ### Constructor
```
class Point:
	def __init__(self, x, y):
		self.x = x
		self.y = y

	def draw(self):
		print("draw")

	def print(self):
		print("this is point")


point1 = Point(10, 5)
point1.draw()
print(point1.x)
```

