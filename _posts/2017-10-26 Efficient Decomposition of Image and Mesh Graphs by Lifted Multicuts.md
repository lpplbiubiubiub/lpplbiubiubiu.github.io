---
title: Kernighan-Lin 算法描述
description: 对该算法简单描述
categories:
comments: true
 - 日记 图论
tags: algorithm cv
---
## 摘要：
作者提出了MP(multicut problem)问题的泛化形式LMP(multicut problem with long term), 这里的long term应该理解为在原图中连接非相邻点之间的假想的边。
作者针对本问题提出了两种针对该问题的解，相关代码作者已经公布，连接
[github](https://github.com/bjoern-andres/graph)

## contrubution
作者提出了Mimnimum cost lift multicut problem(LMP)问题， 一种mp问题的泛化形式， 并对此提出了两种针对的算法来解决本问题。

## problem formulation
LMP问题的最优解是将对图的一对一分解， 其中图的边权值可以自定义，用来表示图中不同集合之间节点之间的cost。

该问题的定义可以如下
1. 简单的无向图G = (V, E)
2. 额外边F 属于G中结点集的任何不相邻的两点，实际上距离d范围为 1< d < d*， d*是固定的，也就是说不会真的是全连接图。
3. 对于图中任何的边e属于E或者F，都会存在一个权值c。
