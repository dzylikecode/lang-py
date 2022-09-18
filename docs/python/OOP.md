# 面向对象

## 创建类

```py
class Person:
    def __init__(self, name, age):
        self.name = name
        self.age = age

    def say(self):
        print("I'm %s, %d years old" % (self.name, self.age))
Dz = Person("Dz", 18)
```

- `__init__`

  用于初始化

## 封装

| 私有                | 特点                                               |
| ------------------- | -------------------------------------------------- |
| `_` 一个下划线开头  | 弱隐藏 不想让别人用 (别人在必要情况下还是可以用的) |
| `__` 两个下划线开头 | 强隐藏 不让别人用                                  |

## 继承

```py
class Student(Person):
    def __init__(self, name, age, school):
        super().__init__(self, name, age)
        self.school = school

    def say(self):
        super().say()
        print("I am studying in %s" % (self.name, self.age, self.school))
```
