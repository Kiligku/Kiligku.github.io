---
title: Markdown 基本语法
date: 2022-04-04 11:27:19
tags:
- markdown
---


## 这是一级标题
<!--more-->

这是一级标题的正文。
新起一行？

新起一段！
加星号加粗！**加粗了**  *斜体了*
1. 一
   1. 二级列表1
   2. 二级列表2
2. 二
3. 三

中间插入文字重新从一开始编号
1. 一一
2. 二二
3. 三三


### 1. 插入图片
粘贴的快捷键为**ctrl+alt+v**
换行加星号给图片添加标题，圆括号内添加标题只能在鼠标悬停于图片上时显示
<img src="https://raw.githubusercontent.com/Kiligku/images/master/%E6%9D%B1%E6%96%B9%E9%92%A2%E7%90%B4%E7%A5%AD%EF%BC%9A%E5%B9%BB%E6%A2%A6%E7%BB%88%E9%86%92%20%E6%9C%AC%E6%97%A0%E4%B8%8D%E6%95%A3%E4%B9%8B%E5%AE%B4_109951163071966688.jpg" style="zoom:50%;" />

*辉夜姬*

<img src="https://raw.githubusercontent.com/Kiligku/images/master/2022-04-04-21-40-49.png" width=50% style="zoom:50%;" />

*harutya*

```markdown
markdown语法
![](https://raw.githubusercontent.com/Kiligku/images/master/%E6%9D%B1%E6%96%B9%E9%92%A2%E7%90%B4%E7%A5%AD%EF%BC%9A%E5%B9%BB%E6%A2%A6%E7%BB%88%E9%86%92%20%E6%9C%AC%E6%97%A0%E4%B8%8D%E6%95%A3%E4%B9%8B%E5%AE%B4_109951163071966688.jpg)

*辉夜姬*

HTML语法
<img src="https://raw.githubusercontent.com/Kiligku/images/master/2022-04-04-21-40-49.png" width=50%/>

*harutya*
```


### 2. 实现图片并排
#### markdown语法
![](https://raw.githubusercontent.com/Kiligku/images/master/2022-04-04-21-43-11.png)![](https://raw.githubusercontent.com/Kiligku/images/master/2022-04-04-21-43-11.png)
两短代码中间不能有空格  
如果图片过大则无法实现并排

#### HTML语法
<center class="half">
<img src="https://img-blog.csdnimg.cn/2019012511060017.png" width=200>
<img src="https://img-blog.csdnimg.cn/2019012511060017.png" width=200>
</center>

```markdown
#### markdown语法
![](https://raw.githubusercontent.com/Kiligku/images/master/2022-04-04-21-43-11.png)![](https://raw.githubusercontent.com/Kiligku/images/master/2022-04-04-21-43-11.png)
两短代码中间不能有空格  
如果图片过大则无法实现并排

#### HTML语法
<center class="half">
<img src="https://img-blog.csdnimg.cn/2019012511060017.png" width=200>
<img src="https://img-blog.csdnimg.cn/2019012511060017.png" width=200>
</center>
```
### 3. 插入公式
#### 单独成行的公式(前后加两个美元符号)
$$
\lim_{x \to 0}\frac{sin(x)}{x}=1
$$
```markdown
$$
\lim_{x \to 0}\frac{sin(x)}{x}=1
$$
```
#### 行内公式 
等价无穷小$\lim_{x \to 0}\frac{sin(x)}{x}=1$

``` markdown
等价无穷小$\lim_{x \to 0}\frac{sin(x)}{x}=1$
```
### 4. 插入表格
表格内的文字默认为左对齐，在右侧打一个冒号改为右对齐，两侧都打冒号改为中对齐

| aa  |  bb   |   cc |
| --- | :---: | ---: |
| 1.1 |  4.5  |  1.4 |
| 1.9 |  1.9  |  8.1 |

一键格式化表格输入内容 **shift+alt+f**
``` markdown
| aa  |  bb   |   cc |
| --- | :---: | ---: |
| 1.1 |  4.5  |  1.4 |
| 1.9 |  1.9  |  8.1 |
```

### 5. 插入超链接
选中文字，然后ctrl+v粘贴
这是一个[链接](https://www.bilibili.com/video/BV1si4y1472o?spm_id_from=333.337.search-card.all.click)

```markdown
这是一个[链接](https://www.bilibili.com/video/BV1si4y1472o?spm_id_from=333.337.search-card.all.click)
```
### 6. 插入代码块

输入``` *代码内容* + 语言名称
```python
def model_forward(x_train, para):  # forward propagation on the entire model
    caches = {'A0': x_train}  # insert x_train as A0
    # caches: store intermediate variable A, in order to calculate backward propagation
    L = int(len(para) / 2)
    for l in range(L - 1):
        W = para['W' + str(l + 1)]
        b = para['b' + str(l + 1)]
        A_prev = caches['A' + str(l)]
        caches['A' + str(l + 1)], caches['Z' + str(l + 1)
                                         ] = forwardProp(W, b, A_prev, activation='relu')
    # process the last layer alone
    W = para['W' + str(L)]
    b = para['b' + str(L)]
    A_prev = caches['A' + str(L - 1)]
    caches['A' + str(L)], caches['Z' + str(L)] = forwardProp(W,
                                                             b, A_prev, activation='sigmoid')
    return caches
```

用这个方法还可以生成行内代码块```print("hello world")```

### 7. 禅模式
快捷键ctrl+k松开后再按z

### 8. 数学公式编号
$$x = y+1 \tag{1.1}$$
$$x^2 + y^2 = 1 \tag{1.2}$$

```markdown
$$x = y+1 \tag{1.1}$$
$$x^2 + y^2 = 1 \tag{1.2}$$
```
