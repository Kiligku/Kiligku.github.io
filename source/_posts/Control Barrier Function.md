---
title: Control Barrier Function
date: 2023-06-28 21:36:55
categories:
- 控制理论
- 强化学习
---
# Control Barrier Function
## 1. Lyapunov Function（LF）
<!--more-->
目的：构造一个能量函数$V(x)$，对于稳定点为$x_e$的系统，分析其是否渐近稳定(asymptotically stable)。

对于一般线性\非线性系统动态：
$$\dot{x} = f(x) + g(x)u$$

如果构造$V(x)$
$$
\begin{aligned}
    s.t. \quad  &V(x_e) = 0, V(x) > 0 \quad for \; x \neq x_e \\
    & \dot{V}(x) = \frac{\partial V}{\partial x}f(x) < 0  \quad for \; x \neq x_e
\end{aligned}
$$
则可以证明系统渐进稳定

Lyapunov Function的性质：对于所有$c>0$的sublevel set:
$$\Omega_c = \{x | V(x)\leq c\}$$
$\Omega_c$都是invariant set

构造Lyapunov函数分析系统稳定性的一个好处是不用求解原系统的微分方程。
## 2. Control Lyapunov Function(CLF)
对于自身无法稳定的系统，我们希望构造一个反馈控制器$u=k(x)$来镇定系统。
$$stability \rarr stablizibility \\
forward\;invariance \rarr control\; invariance$$

由于加入了控制的作用，$V$现在同时是$x$和$u$的函数，CLF需要满足的条件如下：
$$
\begin{aligned}
&1. \quad \Omega_C :=\{x\in\mathbb{R}:V(x) \leq c\}\; is\; bounded \\
&2. \quad V(x) > 0, \quad \forall s \in \mathbb{R}^n \setminus \{x_e\}, V(x_e)=0 \\
&3. \quad \underset{u \in U}{min}\dot{V}(x, u) < 0, \quad \forall x \in \Omega_c \setminus \{x_e\}
\end{aligned}
$$
$\Omega_c$被称为region of attraction(ROA),这个集合内出发的所有状态都会渐近稳定至$x_e$

### Exponentially Stablizing CLF
为了保证系统趋近稳定的速率，CLF的条件3可以修改为
$$
\underset{u \in U}{min}\dot{V}(x, u) + \lambda V(x) < 0, \quad \forall x \in \Omega_c \setminus \{x_e\}
$$
## 3. Nagumo's Invariance Principle
若不要求系统渐近稳定，而对系统的安全提出要求。即要求系统在安全集内forward invariant，我们可以借助Nagumo's invariance principle构造函数$h(x)$：

若存在一个连续可微函数$h(x)$, 对于它的superlevel set：$\mathcal{C}=\{x|h(x) \geq 0\}$，满足
$$\dot{h}(x) > 0 \quad \forall x\in \partial\mathcal{C}$$
其中$\partial \mathcal{C}$表示集合的边界

则$\mathcal{C}$具有forward invariant性质

相比LF拥有多个forward invariant的sublevel set，$h(x)$只有对应0的superlevel set拥有此性质。并且对$h(x)$本身只有边界导数值的要求，这使得$h(x)$更加易于构造。
## 4. Control Barrier Function
对于