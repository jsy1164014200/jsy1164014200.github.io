---
layout: single
title:  "IP (2nd) Chapter 7笔记"
date:   2024-03-18 14:20:36 +0800
categories: Integer-Programming
---
这一篇是Integer Programming, 2nd Edition (Laurence A. Wolsey) 第七章Branch and Bound的笔记

考虑的主要问题是
$Z = \max\{ \mathbf{c}^{\top} \mathbf{x} : \mathbf{x} \in S \}$. 

## 7.1 Divide and Conquer
B&B的核心思想是分而治之。我们通常使用枚举树来表示B&B。如果$S = S_1 \cup ... \cup S_K.$，那么$Z=\max_k Z^k$. 举了两个例子

- Binary enumeration tree.
- TSP enumeration tree.

## 7.2 Implicit Enumeration

考虑一个小问题$Z^k = \max\{ \mathbf{c}^{\top} \mathbf{x} : \mathbf{x} \in S^k \}$. $\overline{Z}^k$ and $\underline{Z}^k$ 分别是$Z^k$的upperbound和lowerbound。那么，$\underline{Z} = \max_k \underline{Z}^k$, $\overline{Z} = \max_k \overline{Z}^k$。 

这样我们可以想到三种prune策略

- Pruning by optimality: $Z^k$ 被解到最优了
- Pruning by bound：$\overline{Z}^k \leq \underline{Z}$ 
- Pruning by infeasiblity: $S_k = \empty$ 

## 7.3 Branch and Bound: an Example

首先选择一个node，解它的relaxation problem。
然后根据这些信息bounding一下。如果bounding不了就进行branching。 

这其中有很多细节，其中比较常见是父节点的单纯行法得到的basic可以直接给子问题的对偶单纯行法使用。 （复习一下单纯行法，对偶单纯行法，内点法

## 7.4 LP-Based Branch and Bound

![x](../assets/images/LPbasedB&B.jpg "y")

这个算法有很多细节点在商业求解器中得到了优化

- Storing the tree 
- Simplex Strategies 
- Branching and Node Selection 
- SOS1, SOS2可以使用特殊的branching规则，还有很多其他约束
- Priorities
- Symmetry Breaking / Orbital Branching 
- Preprocessing or Presolve 
- Bound tighting 
- Redundant Constraints 
- ... 


 