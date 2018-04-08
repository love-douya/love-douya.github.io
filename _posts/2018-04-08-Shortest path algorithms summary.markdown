---
layout: post
title:  "最短路径算法归纳"
date:   2018-04-08 14:20:00
categories: Algorithm 
tags: Algorithm Graph Dijkstra Bellman-ford SPFA Topological Sort
mathjax: true
---

* content
{:toc}

所有节点对的最短路径计算可以使用Floyd-Warshall算法，该算法为暴力算法，时间复杂度为 $O(V^3)$ ，下面主要讨论单源最短路径算法。
单源最短路径算法有
1.	朴素Dijkstra算法，时间复杂度 $O(V^2)$ ，无法判断是否存在负环。
2.	Bellman-Ford算法，时间复杂度 $O(VE)$ ，可以判断是否存在负环，并且可以找到负环。
3.	SPFA(Bellman-Ford的队列实现)，时间复杂度不稳定(有两个改良时间复杂度的优化策略SLF(Small Label First)和LLL(Large Label Last)，这里不做详细讨论)，可以判断是否存在负环，但是无法找到负环。
4.	Dijkstra算法(二叉堆优化)，时间复杂度 $O(VlogV+ElogV)$ ，BFS时间复杂度 $O(V+E)$ ，二叉堆时间复杂度 $O(logV)$ ，同样无法判断是否存在负环。
5.	Dijjkstra算法(斐波那契堆优化)，时间复杂度 $O(E+VlogV)$ ，无法判断是否存在负环。
6.	在DAG中，可以使用Topological Sort来计算最短路径，时间复杂度 $O(V+E)$ ，由于没有环，所以不存在负环。
