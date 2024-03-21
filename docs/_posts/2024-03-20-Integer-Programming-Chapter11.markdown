---
layout: single
title:  "IP (2nd) Chapter 11笔记"
date:   2024-03-20 14:50:36 +0800
categories: Integer-Programming
---
这一篇是Integer Programming, 2nd Edition (Laurence A. Wolsey) 第11章Column (and Row) Generation Algorithms的笔记



## 11.1 Introducetion 

把一个IP问题$\max\{ cx : x\in X \}$的feasible region进行分解$X = \cap_{k=0}^K X^k$，是非常常见的思路（分解之后有利于产生cut，做lagrangian relaxation）。具体来说，feasible region会有下面的结构：
$$
A^1 x^1 + ... + A^Kx^K \leq b: X^0 \\ 
D^1 x^1 \leq d_1, x_1 \text{ nonnegative integer }: X^1 \\ 
... \\
D^K x^K \leq d_K, x_K \text{ nonnegative integer }: X^K 
$$
这种结构是非常有利于用一些特殊方法的。

我们假设$X^k$是有界的，这里我们为$conv(X^k)$的每一个extreme point都引入一个变量，或者为每一个feasible points都引入一个变量。这样一个IP问题总可以变成如下形式：
$$
\max \sum_k \gamma^k \lambda^k \\
\text{s.t.} \sum_k B^k \lambda^k = \beta, \\
 \lambda^k \geq 0 \text{ integer }.
$$
其他很多问题都可以reformulate成这个形式，比如TSP，VRP，都会引入特别多的变量。

我们把这个问题叫做Master Problem, 接下来要解MP的LP relaxation，通过Column Generation Subproblems。最后我们会求到这个问题的最优解。这一套方法叫做 IP Column Generation or Branch-and-Price. 如果加入cut，就变成了brach-cut-and-price. 


## 11.2 The Dantzig–Wolfe Reformulation of an IP

为了简化，我们先考虑$K=1$的情况，
$$
\begin{align}
Z_{IP} = \max\{cx: Ax \leq b, x \in X \}, \ X = \{ x \in \mathbb{Z}^n_+ : Dx \leq d \}
\end{align}
$$ 
类似于我们在lagragin relaxation那一章做的，假设其中$Ax\leq b$ 是复杂约束，不好处理，但是X集合是简单的，很好求解。定义S为整个feasible region。

很显然，(1)是等价于下面这个问题的
$$
\begin{align}
Z_{IP} = \max\{cx: Ax \leq b, x \in \mathbb{Z}^n_+, x \in conx(X) \}. 
\end{align}
$$

假设X是有界的，那么$conx(X) = \{ x\in \mathbb{R}^n : x = \sum_{t=1}^T z^t \lambda_t, \sum_{t=1}^T \lambda_t = 1, \lambda \in \mathbb{R}^T_+ \}$. 把x替换成extrem points的组合（convexification），(2)变成了下面这个问题（Master Problem）
$$
\begin{align}
Z_M = & \max \sum_{t=1}^T (cz^t) \lambda_t, \\ 
\text{s.t.}  & \sum_{t=1}^T (Az^t) \lambda_t \leq b, \\ 
& \sum_{t=1}^T \lambda_t = 1, \\ 
& \lambda \in \mathbb{R}^T_+, \\
& x = \sum_{t=1}^T z^t \lambda_t \in \mathbb{Z}^n. 
\end{align}
$$
当然也可以把x替换成X中的所有points（discretization），这样做的话，$\lambda_t$ 就变成binary variable了。

## 11.3 Solving the LP Master Problem: Column Generation

Linear Master Problem
$$
\begin{align}
Z_{LM} = & \max \sum_{t=1}^T (cz^t) \lambda_t, : \pi_i \\ 
\text{s.t.}  & \sum_{t=1}^T (Az^t) \lambda_t \leq b, : \pi_0 \\ 
& \sum_{t=1}^T \lambda_t = 1, \\ 
& \lambda \in \mathbb{R}^T_+, \\
& x = \sum_{t=1}^T z^t \lambda_t
\end{align}
$$
下面先通过column generation algorithm来解LMP.

1. Initialization: 使用已知的p个点，解一个restricted LMP，得到最优解$\lambda^*$ 和 prices $\pi^*, \pi^*_0$。 

2. Primary Feasibility: $Z_{RLM} = \sum_{t=1}^p (cz^t) \lambda_t^* = \pi^* b + \pi^*_0 \leq Z_{LM}$

3. Optimality Check for LM: 解定价子问题，
$$
\begin{align}
(SP) \zeta^p = \max\{ (c-\pi^*A)x-\pi^*_0 : x\in X \text{ or } conx(X) \}
\end{align}
$$
得到最优解$x^*$. 

4. Stopping Criterion. 如果$\zeta^p = 0$，那么RLM得到的prices $\pi^*, \pi^*_0$ 对LM来说是对偶可行的，$Z_{LM} \leq \sum_{i=1}^m \pi^*_i b_i + \pi^*_0$. 结合Primary Feasibility的结论，我们得知$\lambda^*$是最优的。

5. Generating a New Column. 如果$\zeta^p > 0$，那么可以 设置$z^{p+1} = x^*$，然后加一列$(c^{\top} z^{p+1}, Az^{p+1}, 1)^{\top}$到RLM中去。 

6. A Dual (upper) Bound. 根据定价子问题(SP)，我们有$\zeta^p \geq (c-\pi^*A)x-\pi^*_0, \ \forall x \in X \text{ or } conx(X)$。很显然$(\pi^*, \pi^*_0+\zeta^p)$ 是对偶可行的，$Z_{LM} \leq \sum_{i=1}^m \pi^*_i b_i + \pi^*_0 + \zeta^p$. 

7. An Alternative Stopping Criterion: 如果$\zeta^p > 0$，但是SP问题的最优解$x^*$满足$Ax^* \leq b$ 同时 $\pi^*(Ax^* - b) = 0$, 那么这个$x^*$就是LM的最优解。By $\zeta^p = (c-\pi^*A)x^*-\pi^*_0$, 可以得到$cx^* = \pi^*Ax^*+\pi^*_0+\zeta^p = \pi^*b+\pi^*_0+\zeta^p$. 这个可行解achieve了upperbound，所以是LM的最优解。

怎么样找一个RLM的初始可行解呢，加入m个人工变量或者产生m个extreme points，然后加一个人变量，以及column $(b,1)^{\top}$ 对应一个cost M。

同时结合在Lagrangian relaxation中的结论，LM给的解和他一样。

example 11.1 (page 218)，使用列生成求解一个IP的LMP。

## 11.4 Solving the Master Problem: Branch-and-Price

