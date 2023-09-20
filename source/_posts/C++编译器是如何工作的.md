---
title: C++编译器是如何工作的
date: 2023-09-09 16:50:24
categories:
- C++
tags: 
- 基础知识
---

# C++编译器是如何工作的

<!--more-->
每一个.cpp文件编译后在project_name/x64/Debug/目录下生成一个.obj文件。

## 1. “文件没有意义”

编译器按照默认规则处理文件，例如将.cpp文件当做源文件处理，.h文件当做头文件处理，这种规则可以被修改。

每个文件通过编译器生成一个**翻译单元**(Translation Unit)，每个翻译单元会生成一个obj文件（机器码文件）。如果一个cpp文件包含了多个cpp文件，编译后只会得到一个翻译单元。

## 2. #include是如何工作的？

单纯的复制粘贴！

在编译之前（所有的预处理指令都在这个时候生效），预处理器（preprocessor）读取include的文件，把文件中的内容粘贴进代码中。

定义头文件EndBracet.h（只包含一个反括号）

```c++
}
```

定义源文件Math.cpp

```c++
int Multiply(int a, int b)
{
    return a * b
#include "EndBrace"
```

代码编译成功！

## 3. 另一个预处理指令的例子

### #if   #endif

如果符合#if后面的条件，编译时处理这段代码，否则编译时不处理这段代码。

```C++
#if 0
int Multiply(int a, int b)
{
    return a * b
}
#endif
```

编译后输出的预处理文件（Math.i）如下：

```c++
#line 1 "C:\\Users\\kilig\\source\\repos\\cherno_cpp\\cherno_cpp\\Math.cpp"




#line 8 "C:\\Users\\kilig\\source\\repos\\cherno_cpp\\cherno_cpp\\Math.cpp"
```

可以看到中间的代码已经被全部忽略。











