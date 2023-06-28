# C++链接器是怎么工作的

错误信息：编译阶段发生的错误编号以C开头（例如语法错误），链接阶段发生的错误编号以LNK开头（例如缺少main函数）。

## 程序的入口

程序的入口一般是main函数，但也不必须是main函数，可以在VS的Property界面更改。

<img src="https://raw.githubusercontent.com/Kiligku/images/master/QQ%E6%88%AA%E5%9B%BE20230306000002.png" style="zoom:67%;" />

## 什么情况下会发生链接错误？

在这里只讨论视频中讲到的情形，多与函数定义有关。

### 1. 函数声明找不到对应的实现

在Math.cpp中定义函数：

```C++
#include <iostream>
void Log(const char * message); // 函数的声明

int Multiply(int a, int b)
{
    Log("Multiply");
    return a * b;
}

int main()
{
    std::cout << Multiply(5, 8) << std::endl;
   	return 0;
}
```

可以看出这个函数中，只有Log函数的声明而没有对应的实现。在编译阶段，编译器不关心函数的声明是否有对应的实现，不会报错。而在链接阶段，IDE提示

| 严重性 | 代码    | 说明                            | 项目       | 文件                                                   |
| ------ | ------- | ------------------------------- | ---------- | ------------------------------------------------------ |
| 错误   | LNK1104 | 无法打开文件“x64\Debug\Log.obj” | cherno_cpp | C:\Users\kilig\source\repos\cherno_cpp\cherno_cpp\LINK |

当注释掉Multiply函数的调用之后，即使在整个项目中Multiply函数都没有被调用，在链接阶段同样会报相同的错误。

这是因为C++架设了在Math.cpp的其他文件中（尽管并不存在）Multiply函数也存在被调用的可能。

当我们希望告诉C++：Log函数只在这个文件中被调用时，我们需要使用static关键字：

```C++
static int Multiply(int a, int b)
{
    Log("Multiply");
    return a * b;
}
```

表示Multiply函数只会在当前翻译单元中被调用。此时build项目，不出现错误。

### 2. 函数重定义

当两个函数名字和参数类型均相同时，会出现链接错误。