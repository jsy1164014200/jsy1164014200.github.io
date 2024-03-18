---
layout: single
title:  "2024/03/17 每周总结"
date:   2024-03-17 07:30:36 +0800
categories: Integer Programming
---
最近在看Integer Programming, 2nd Edition (Laurence A. Wolsey)，打算写一些总结类的博客。这一篇是关于第一到五章的。

近些年IP最大的改变是branch-and-cut基本已经替代了branch-and-bound，除此之外还有column generation(branch-cut-andprice)和Benders' decomposition的大量使用。 

考虑的主要问题
$\max\{ \mathbf{c}^{\top} \mathbf{x} : Ax \leq b,  \text{ partial x are integers} \}$. The feasible region is defined as $X$. 

# Chapter one
这一章为Formulations，主要介绍了什么事LP，IP，MIP，BIP(binary)，COP(combinationary)。同时介绍了一些常见的问题：
1. IP and BIPs 
    - The Assignment Problem
    - The 0-1 Knapsack Problem
    - The Set Covering Problem 
    - The Traveling Saleman Problem
2. MIP 
    - Uncapacitated Facility Location (UFL)
    - Uncapacitated Log-Sizing (ULS)


一个整数规划问题常常有多个formulations

引入了一些基本定义和proposition:
- P = $\{x \in \mathbb{R}^n : Ax \leq b$ is a polyhedron. 
- $P \subseteq \mathbb{R}^{n+p} $ is a formulation for a set $X \subseteq \mathbb{Z}^n \times \mathbb{R}^p $ iff $X = P \cap (\mathbb{Z}^n \times \mathbb{R}^p)$. 这个定义是说LP是一个MIP的formulation，如果它只放松了整数点同时没有包含过多的整数点。
- The convec hull of $X$是说 如果X包含两点，那么它一定包含这两点连线上的所有点。Proposition: Conv(X) is a polyhedron. 
- extreme point of P 是 几何上的vertices. Proposition：如果一个LP存在最优解，那么一定存在一个extrme point是最优解
- $P_1 \subseteq P_2$, $P_1$是better formluation
- 什么是Alnative Formulation: 相同的变量
- 什么是Extend Formulation：变量不同 比较proj
- $proj_x Q = \{ x\in \mathbb{R}^n : (x,w)\in Q \text{  for some  } w \}$



# Chapter two
第二章主要是关于optimality, relaxation, and bounds. 

主要概念：
- primary bound
- dual bound
- relaxation: $\max \{ f(x): x\in T \}$ is a relaxation problem if $X\subseteq T$ and $f(x) \geq c(x),\ \forall x \in X$. 
- LP relaxation: $\max \{ c^{\top} x: x\in P \}$，P is a formulation. Proposition: if a relaxation is infeasible, the original problem is infeasible. 
- Combinatorial Relaxation
- Lagrangian Relaxation: $\max \{ c^{\top} x + u^{\top}(b-Ax): x\in X \}$. 
- weak-dual pair. finding a maximum cardinality matching 于 finding a minimum cardinality covering by nodes 是weak-dual pair. 
- Proposition: $\min\{ u^{\top} b : uA \geq c, u\in \mathbb{R}^m_+ \}$ 于原问题是weak-dual pair. （这是dual bound的来历？
- Supperadditive dual. 



# Chapter three

# Chapter four

# Chapter five




[zhishi-1]: https://www.runoob.com/w3cnote/cpp-header.html 
[lp-dual]: https://en.wikipedia.org/wiki/Dual_linear_program
[cs]: https://www.matem.unam.mx/~omar/math340/comp-slack.html
[enum-class]: https://learn.microsoft.com/zh-cn/cpp/cpp/enumerations-cpp?view=msvc-170
[o-blog]: https://jiangshibiao.github.io/Vehicle-Routing-Problem/