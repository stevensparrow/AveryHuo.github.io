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

#exercise
class Person:
	def __init__(self, name):
		self.name = name

	def talk(self):
		print(f"{self.name} is talking..")


while True:
	person_name = str(input("Please enter person: "))
	if person_name == "Quit":
		break
	elif person_name != "":
		new_person = Person(person_name)
		new_person.talk()
	else:
		print("You enter a empty!")

```

+ ### inheritance
+ use bracket to inherit parent class
```
class Mammal:
	def walk(self):
		print("walk")


class Dog(Mammal):
	def bark(self):
		print("bark")


class Cat(Mammal):
	pass  # tell python to pass this line


dog1 = Dog()
dog1.walk()
dog1.bark()

```

