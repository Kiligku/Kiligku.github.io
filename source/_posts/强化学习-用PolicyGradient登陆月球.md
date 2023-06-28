---
title: 强化学习-用PolicyGradient登陆月球
date: 2022-12-25 20:53:33
categories:
- 强化学习
tags:
- 强化学习
- pytorch
---

# 强化学习-用PolicyGradient登陆月球
---
<!--more-->
## 1. 理论基础
PolicyGradient（以下简称PG)是一种policy-based的强化学习方法，PG不为state设定value值，而是直接参数化policy，输入state，得到action的概率分布，通过对action进行随机采样决定下一步的行动。\
训练Policy时，用Agent和环境进行多次互动得到多个Trajectory。将Trajectory奖励的期望值（估计值）最大作为优化目标，对目标函数运用梯度上升算法。

$\tau$
