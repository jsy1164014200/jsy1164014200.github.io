---
layout: single
title:  "IP (2nd) Chapter 12笔记"
date:   2024-03-21 14:50:36 +0800
categories: Integer-Programming
---
这一篇是Integer Programming, 2nd Edition (Laurence A. Wolsey) 第12章Benders' Algorithms的笔记



## 12.1 Introducetion 

考虑如下问题：
$$
\begin{align}
Z = \max \{ \mathbf{c}^{\top} \mathbf{x} + \mathbf{h}^{\top} \mathbf{y} : \mathbf{F} \mathbf{x} + \mathbf{G} \mathbf{y} \leq \mathbf{d},\ \mathbf{x} \in \mathbf{X} \subseteq \mathbb{Z}^n_+,\ \mathbf{y} \in \mathbb{R}^p_+ \}
\end{align}
$$
其中p很大，n很小。Benders 算法的核心思想是分解问题，在x-space中解问题。

## 12.2 Benders' Reformulation 

(1) 可以写成：
$$
\begin{align}
Z = \max \{ \mathbf{c}^{\top} \mathbf{x} + \phi(\mathbf{x}) :  \mathbf{x} \in \mathbf{X}   \}
\end{align}
$$
其中$\phi(\mathbf{x}) = \max\{ \mathbf{h}^{\top} \mathbf{y}:  \mathbf{G} \mathbf{y} \leq \mathbf{d}-\mathbf{F} \mathbf{x},\  \mathbf{y} \in \mathbb{R}^p_+ \}$。

我们先定义下 $\phi(\mathbf{x})$的对偶问题
$$
(DSP) \ \min \{ \mathbf{u}^{\top} (\mathbf{d} - \mathbf{F}\mathbf{x}) : \mathbf{u}^{\top} \mathbf{G} \geq \mathbf{h}^{\top}, \mathbf{u} \in \mathbb{R}^m_+ \}.
$$

Assumption：为了简化，我们假设$U = \{ \mathbf{u} \in \mathbb{R}^m_+ : \mathbf{u}^{\top} \mathbf{G} \geq \mathbf{h}^{\top} \}$ 不为空集，因为如果U是空的，那么$\phi(x) = \infty \ \forall x \in X$. （根据对偶，很好证明）

根据Farkas' Lemma，$\phi(\mathbf{x}) $ is feasible （或者说对偶问题最优解不为负无穷）iff 
$$
\mathbf{v}^{t \top} (\mathbf{d}-\mathbf{F} \mathbf{x}) \geq 0, \ t = 1, ..., T
$$
其中$\mathbf{v}^t$是 extreme rays of U. 
很显然，如果$\phi(x)$是可行的，那么他可以写成$\phi(x) = \min_{s=1,...,S} \mathbf{u}^{s \top} (\mathbf{d}-\mathbf{F} \mathbf{x})$，其中$u^s$ 是U的extreme points. 

通过这种方式，（2）又能写成下面这种形式
$$
\begin{align}
Z = \max \ &\mathbf{c}^{\top} \mathbf{x} + \eta \\ 
\text{s.t.} \ & \mathbf{v}^{t\top} (\mathbf{d} - \mathbf{F}\mathbf{x}) \geq 0, \ \forall t = 1,..., T \\ 
& \mathbf{u}^{s\top} (\mathbf{d} - \mathbf{F}\mathbf{x}) \geq \eta, \ \forall s = 1,..., S \\
& \mathbf{x} \in \mathbf{X}, \eta \in \mathbb{R}. 
\end{align}
$$
在最开始大假设下，（4）保证我们只考虑可行的x。（5）保证了$\eta=\phi(x)$。这个问题一般有exponential number的约束，所以一般会采用branch and cut来求解。 

 

下面介绍Branch-and-cut algorithm for Benders' 

在枚举树的每一个node，我们都要解一个LP relaxation问题：
$$
\begin{align}
(BR) \ Z^* = \max \ & \mathbf{c}\mathbf{x} + \eta \\
\text{s.t.} \ & \mathbf{v}^{t\top} (\mathbf{d} - \mathbf{F}\mathbf{x}) \geq 0, \ \forall t \in T^{\prime} \\ 
& \mathbf{u}^{s\top} (\mathbf{d} - \mathbf{F}\mathbf{x}) \geq \eta, \ \forall s \in S^{\prime} \\
& l \leq x \leq k, \\ 
& \mathbf{x} \in P_{X}, \eta \in \mathbb{R}. 
\end{align}
$$
其中$P_X$ 是X的一个formulation，i.e.，$X=P_X \cap \mathbb{Z}^n$. 同时，在这个node上，也会尽量找一个incumbent，提供一个$\underline{Z}$.  

Initialization。把原问题放到list里面去。

1. select一个node。移除出list
2. 解BR。
3. 如果BR不可行，那么这个node就可以pruned掉。
4. BR可行，对应最优解$(\mathbf{x}^*, \eta^*)$。
    - 如果$\mathbf{c}^{\top} \mathbf{x}^* + \eta^* \leq \underline{Z}$, pruned掉。
    - 想办法给原问题加cut，加cut就需要解一个separation problem，这个问题就是DSP。 
        - 如果DSP is unbounded，它会给出一个extreme ray $\mathbf{v}^t$ 同时 $\mathbf{v}^{t\top} (\mathbf{d} - \mathbf{F}\mathbf{x}^*) < 0$。因为DSP的可行集是不变的，那么这个extreme ray不受$x$ 影响，但是如果$\mathbf{v}^{t\top} (\mathbf{d} - \mathbf{F}\mathbf{x}) < 0$，那很显然这个$x$对应的$\phi(x)$不可行。所以我们就可以加一条 feasibility cut: $\mathbf{v}^{t\top} (\mathbf{d} - \mathbf{F}\mathbf{x}) \geq 0$。 
        - 如果DSP is feasible同时 $\phi(x^*) = \mathbf{u}^{s\top}(\mathbf{d} - \mathbf{F}\mathbf{x}^*)  < \eta^*$。其中$u^s$是U的extreme point。那么我们可以加optimality cut: $\mathbf{u}^{s\top} (\mathbf{d} - \mathbf{F}\mathbf{x}) \geq \eta$。 
        - DSP is feasible同时 $\phi(x^*)   = \eta^*$。所有约束都是满足的，BR解到最优了
            - 如果x是整数，那么可行更新 incumbent 和 $\underline{Z}$. 同时pruned掉这个node
            - 如果x不是整数，那么就要branching了


## 12.3 Benders’ with Multiple Subproblems

K个子问题的Bender，跟前面的非常类似，就不啰嗦了。 

两个经典的例子：
- The Uncapacitated Facility Location Problem
- Two-stage Stochastic Programming with Recourse

## 12.4 Solving the Linear Programming Subproblems

这一部份我没太理解，为什么不够strong cuts。

Unfortunately the solution of the dual of the linear programming separation problem
does not always provide strong cuts. Thus, when the optimum is unbounded
(i.e. the primal is infeasible), the extreme ray that is found is somewhat arbitrary.
Therefore, as for the lift-and-project algorithm in Section 8.9, it is usual to add
a normalization constraint so that the LP has a bounded optimal value.


## 12.5 Integer Subproblems: Basic Algorithms

首先要明确一个观点：
> Benders’ algorithm is just a way to solve linear programs by iterating between LPs in the (x, 𝜂)-space and LPs in the y-space.