---
layout: single
title:  "IP (2nd) Chapter 8笔记"
date:   2024-03-18 14:50:36 +0800
categories: Integer-Programming
---
这一篇是Integer Programming, 2nd Edition (Laurence A. Wolsey) 第八章Cutting Plane Algorithms的笔记



## 8.1 Introducetion
考虑的主要问题是
$\max\{ \mathbf{c}^{\top} \mathbf{x} : Ax \leq b,  x \in Z^n_+ \}$. The feasible region is defined as $X$. 

Prop: $conv(X) = \{ x: \tilde{A} x \leq \tilde{b},  x \geq 0 \}$ is a polyhedron. 

Def: $\boldsymbol{\pi}^{\top} \mathbf{x} \leq \pi_0$ is a valid inequality for $X$ if it holds for all $x \in X$. 

## 8.2 some examples 

## 8.3 Valid Inequalities 
LP problem $P = \{ x : Ax \leq b, x\geq 0 \}$ 的有效不等式满足：$\boldsymbol{\pi}^{\top} \mathbf{x} \leq \pi_0$ is valid iff there exist $u \geq 0, v\geq 0$ such that $uA-v=\pi$ and $ub\leq \pi_0$. (证明是根据LP的对偶来的

对于IP problem来说，所有的有效不等式都是通过应用有限次数的CG procedure产生的。 

![x](../assets/images/CGprocedure.jpg "y")

CG procedure非常简单，就是把所有约束的左边和右边乘一个非负系数然后相加。 

## 8.4 A Priori Addition of Constraints

加cut有优点也有缺点，优点在于可以得到跟好的formluation，更快的找到可行解。缺点在于加多了cut会让LP解的很慢。 

寻找有效不等式的常用方法：划分约束 $X = X^1 \cap X^2$，然后分别找$X^1$ and $X^2$的有效不等式。注意这里的 思想不同于B&B，这里用的是 交集，B&B那里是并。

## 8.5 Cutting Plane Algorithms
> 也叫Automatic Reformulation？

切平面法的核心思想不是把所有有效不等式都找到，然后找到conv hull，而是find a good approximation to $conv(X)$ in the neighborhood of an optimal solution.

![x](../assets/images/cuttingplanealgorithm.jpg)



## 8.6 Gomory’s Fractional Cutting Plane Algorithm

对于纯的IP问题：$\max \{ cx : Ax = b, x\geq 0 \text{ and integer } \}$. 

Gomory’s Fractional Cutting Plane Algorithm能保证给一个切掉LP solution的cut 

## 8.7 Mixed Integer Cut
前面说的（除了8.4，8.5）都是说给IP约束加cut，这一小节给了一些给MIP约束加cut的方法。 

- The Basic Mixed Integer Inequality: $(x,y) \in Z^1_+ \times R^1$
- The Mixed Integer Rounding (MIR) Inequality: $(x_1,x_2,y) \in Z^2_+ \times R^1$
- The Gomory Mixed Integer Cut: 扩展了8.6节，针对MIP约束了
- Split Cuts

> In fact, it is not difficult to show
that MIR, split, and Gomory mixed integer cuts are essentially equivalent in the
sense that any inequality that is of one type, can also be obtained as an inequality
of the other two types.

## 8.9 Disjunctive Inequalities and Lift-and-Project