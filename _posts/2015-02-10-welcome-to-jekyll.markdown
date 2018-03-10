---
layout: post
title:  "BFS"
date:   2018-3-10 12:44:00
categories: Algorithm
tags: Algorithm
excerpt: BFS in Python
mathjax: true
---
Use a queue to implement this algorithm. If weight of each edge is same, we can use only BFS to traverse the graph to achieve shortest path. In dijkstra with adjacency list, BFS is used when we traverse the graph.


*** The loop version of BFS
```python
graph = {'A': set(['B', 'C']),
         'B': set(['A', 'D', 'E']),
         'C': set(['A', 'F']),
         'D': set(['B']),
         'E': set(['B', 'F']),
         'F': set(['C', 'E'])}

def bfs(graph, start):
    visited, queue = set(), [start]
    while queue:
        vertex = queue.pop(0)
        if vertex not in visited:
            visited.add(vertex)
            queue.extend(graph[vertex] - visited)
    return visited

print(bfs(graph, 'A'))# {'B', 'C', 'A', 'F', 'D', 'E'}
```

Block Mathjax 

$$
f(x) = ax + b
$$

Inline Mathjax $a \neq b$

