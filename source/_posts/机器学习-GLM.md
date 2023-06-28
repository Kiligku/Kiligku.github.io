---
title: 机器学习-GLM
date: 2022-08-29 22:06:06
categories:
- 机器学习
tags:
- 机器学习
---

# Generalized Linear Model

## 1.The exponential family
指数家族的分布函数都可以被写成以下形式：
$$
p(y;\eta) = b(y) exp(\eta^TT(y) - a(\eta))
$$
- $\eta$: natural parameter / canonical parameter（正规参数）
- $T(y)$: sufficient statistic(充分统计量)
- $a(\eta)$: log partition function. $e^{-a(\eta)}$在式子中充当归一项，让概率分布函数的积分为1

## 2.Constructing GLMs
令$y,x$为符合指数家族分布函数分布的随机变量，我们做出如下假设。通过这几条假设能推导出GLM的学习法则。
1. 给定$x$, 我们的目标



