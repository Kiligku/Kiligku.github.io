---
title: 类与对象_BIF
date: 2022-05-02 09:53:36
categories:
- python
tags: 
- 面向对象编程
---
# python类与对象的BIF(Built In Function)
---
<!--more-->
## 1. issubclass(class, classinfo)
检查class是否为classinfo的子类，classinfo可以为一个类或者一个元组（包含多个类）。该函数为**非严格检查**，即自己是自己的子类

```python
class A:
    pass
class B(A):
    pass

>>> issubclass(B, A)
True
>>> issubclass(B, B)
True
```
## 2. isinstance(object, classinfo)
检测实例是否属于指定的类

## 3. hasattr(object, name)
检测对象是否拥有指定属性
```python
class C:
    def __init__(self, x=0):
        self.x = x
c1 = C()

>>> hasattr(c1, 'x') # 引号不可缺失
True

```
## 4. getattr(object, name[, default])
返回实例中名字为name的成员的值，如果第三个参数为空，则当名字为name的成员不存在时报错，否则显示相应的信息。
函数中的参数name一定要加单引号

## 5. setattr(object, name, value)
设置指定实例中成员的值，如果指定名字的成员不存在，则创建一个该名字的成员

## 6.property(fget=None, fset=None, fdel=None, doc=None)
传入获取、设置、删除属性值的函数，返回一个新式的类属性

```python
class C(object):
    def __init__(self):
        self._x = None
 
    def getx(self):
        return self._x
 
    def setx(self, value):
        self._x = value
 
    def delx(self):
        del self._x

    x = property(getx, setx, delx, "I'm the 'x' property.")

>>> c.x
触发getter
>>> c.x = value
触发setter
>>> del c.x
触发deleter
```
利用property可以增加代码的可拓展性，只需要修改三个函数而无需修改调用的语句