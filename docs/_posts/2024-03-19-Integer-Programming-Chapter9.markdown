---
layout: single
title:  "IP (2nd) Chapter 9笔记"
date:   2024-03-18 14:50:36 +0800
categories: Integer-Programming
---
这一篇是Integer Programming, 2nd Edition (Laurence A. Wolsey) 第九章Strong Valid Inequality的笔记



## 9.1 Introducetion 
切平面算法以及Gomory fractional切平面法在实际上表现并不好，但是cut在实际中特别有用。

## 9.2 Strong Inequalities
Consider $P = \{ x\in \mathbb{R}^n_+ : Ax \leq b \}$. 

Def of Dominance: $\pi x \leq \pi_0$ dominates $\mu x\leq \mu_0$ if there exists $u>0$ such that $\pi \geq u \mu$ and $\pi_0 \leq u \mu_0$, and $(\pi, \pi_0) \neq (u\mu, u\mu_0)$. 

Def of Redundant in the description of P: 一个有效不等式如果被 其他有效不等式的线性组合所占优，那么它就是多余的in the description of P。

这两个定义也可以从集合角度来看待。 

Full-dimensional Polyhedra 是指包含n个线性独立方向的P？dim(P) = n 
如果P是一个full-dimensional polyhedron，它有一个唯一的描述（每一个不等式都是必须的）。

- face：把有效不等式的不等好改成等号，同时face上的点全在P上
- facet：face with dimmension = dim(P)-1

Prop: If P is full-dimensional, a valid inequality $\pi x \leq \pi_0$ is necessary in the description of P iff it defines a facet of P. 

这一小节也给了一些证明$conv(X)$ 的strong valid inequalities的方法。


## 9.6 Branch and cut 
> A Cut-and-Branch Algorithm is a branch-and-bound algorithm in which cuts are generated at the top node of the tree before branch begins. A Branch-and-Cut Algorithm is a branch-and-bound algorithm in which cutting planes are generated
throughout the branch-and-bound tree. 

![x](../assets/images/B&C.jpg)
