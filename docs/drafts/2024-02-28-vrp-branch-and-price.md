---
layout: single
title:  "VRP问题：使用branch and price求解"
date:   2024-02-28 17:35:36 +0800
categories: VRP
---
## review 
1. review文章
    - Fifty Years of Vehicle Routing. Transportation Science.
2. 当前最先进的精确解VRP的文章
    - Improved branch-cut-and-price for capacitated vehicle routing. Math. Prog. Comp.
    - New Enhancements for the Exact Solution of the Vehicle Routing Problem with Time Windows. INFORMS Journal on Computing.
3. 当前最先进的启发解VRP的文章
    - 还在研究中...

## branch and bound 
分支定界算法（B&B）是精确算法中的核心算法。它的基本思想来自于“分而治之”。
B&B一般用来求解整数规划问题，当然它也可以被用来求解非线性优化问题（NLP）。因此，熟练掌握B&B算法能为后续学习其他精确算法打下良好的基础。


branch and bound

cutting plane

branch and cut

column generation (不保证得到最优解，需要结合其他技巧获得最优解)

branch and price (保证获得全局最优解)

Lagrangian relaxation (不保证得到最优解，需要结合其他技巧获得最优解)

Dantzig-Wolfe decomposition

Benders decomposition










## mac使用gurobi碰到的问题
1. 使用 官方提供的cmake文件 FindGUROBI.cmake & CMakeLists.txt
2. set(GUROBI_DIR /Library/gurobi1100/macos_universal2) in FindGUROBI.cmake
3. link错误: https://support.gurobi.com/hc/en-us/articles/360039093112-How-do-I-resolve-undefined-reference-errors-while-linking-Gurobi-in-C

> 还是有问题gcc的问题？