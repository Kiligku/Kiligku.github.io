---
title: python装饰器
date: 2022-06-24 11:09:14
categoris:
- python
tags:
- python
---

# python装饰器是啥？有什么作用？
<!--more-->

[参考文章-知乎](https://zhuanlan.zhihu.com/p/435467555)
[参考文章-菜鸟](https://www.runoob.com/w3cnote/python-func-decorators.html)


python装饰器可以分为**装饰器本体**和装饰器内部的**处理函数**（通常规定名字为wrapper）。调用的函数本身作为参数传入装饰器，装饰器再调用内部的wrapper函数，对函数的进行规定的处理，最后装饰器返回wrapper函数本身。

在经过装饰器的处理后，调用函数其实就是在调用wrapper，只是调用时的名称仍是原来的函数，所以看起来原函数是被“**装饰**”了。

## 调用的方法
在函数前一行加上
@装饰器名字

## 1. 基本的装饰器应用
### 典型应用1
用户登陆系统，验证输入的账号密码是否正确，只有二者都正确时才提示登陆成功。

```python
def checkInfo(func):  # 装饰器
    def wrapper(*args, **kwargs):  # 处理函数
        print('args:{}'.format(args))
        if args[0] == 'xuanyuan' and args[1] == '12345':
            return func(*args, **kwargs)
        else:
            print('username or password is incorrect!')
            return None
    return wrapper  # 将wrapper自身返回，作为一个新的函数供调用


@checkInfo
def user_login(username, password):
    print('login success!')

>>> user_login('xuanyuan', '12345')
>>> login success!

>>> user_login('111', '222')
>>> username or password incorrect!
```

@checkInfo相当于把下面定义的函数传入了装饰器。装饰器函数本身返回内部的wrapper函数。在执行user_login函数时，先执行了wrapper中自定义的内容，即“装饰”的部分，再返回被装饰的函数本身，原函数被返回时即被执行，并且可以用变量接收返回值。

### 应用2
计算函数的执行时间
```python

import time
  
def timeis(func):
    '''Decorator that reports the execution time.'''
  
    def wrap(*args, **kwargs):
        start = time.time()
        result = func(*args, **kwargs)
        end = time.time()
          
        print(func.__name__, end-start)
        return result
    return wrap
  
@timeis
def countdown(n):
    '''Counts down'''
    while n > 0:
        n -= 1
  
countdown(5)
countdown(1000)
```
## 2. 带参数的装饰器
**需求**：需要在被装饰函数执行时在终端输出日志信息，并将信息写到指定的文件中。
可以把日志文件的路径作为参数，实现带参数的装饰器

用函数形式实现的装饰器需要注意每层函数的返回值。logit()函数返回内部的func_decorator，下半部分的函数相当于语句logit()(words)，内部的func_decorator和无参装饰器一样返回wrapper，再由wrapper返回被装饰函数的返回值。

之前定义无参装饰器的方法还存在一个问题：装饰器返回的是内部的wrapper函数，调用原函数相当于调用wrapper函数，但此时原函数的函数名(func.\_\_name\_\_)和函数文档(func.\_\_doc\_\_)都被wrapper函数覆盖掉了，这时候需要用到python的functool库，在装饰器的定义下添加@wraps(被装饰函数名)解决这个问题。

**完整代码**
```python
from functool import wraps
def logit(PATH='log.txt'):
    def func_decorator(func):
        @wraps(func)
        def wrapper(*args, **kwargs):
            log_info = func.__name__ + ' being executed'
            print(log_info)
            print('params: {}'.format(args))
            with open(PATH, 'a') as f:
                f.write(log_info)
            return func(*args, **kwargs)
        return wrapper
    return func_decorator


@logit()
def say(words):
    print(words)

if __name__ == '__main__':
    say('hello')

>>> say being executed
>>> params: ('hello',)
>>> hello
```

## 3. 装饰器类
当装饰器需要实现更加复杂的功能时，用函数定义装饰器会显得繁琐。这时候可以利用类的__call__方法来实现装饰器。用类定义的装饰器支持继承等操作，更易于拓展。

### 调用方法
和函数定义的装饰器相同

### 代码实例
```python
class Loggit:
    def __init__(self, path='log_class.txt'):
        self.log_path = path

    def __call__(self, func):
        @wraps(func)
        def wrapper(*args, **kwargs):
            log_info = func.__name__ + ' being executed'
            print(log_info)
            print('params: {}'.format(args))
            with open(self.log_path, 'a') as f:
                f.write(log_info)
            self.notify()
            return func(*args, **kwargs)
        return wrapper

    def notify(self):
        # 由子类重写该方法
        pass


class EmailLogger(Loggit):
    def __init__(self, address):
        super().__init__()
        self.address = address

    def notify(self):
        print('An email has been sent')

if __name__ == '__main__':
    say('hello')

>>> say being executed
>>> params: ('hello',)
>>> An email has been sent
>>> hello
```

