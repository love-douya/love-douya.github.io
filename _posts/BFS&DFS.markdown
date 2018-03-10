---
layout: post
title:  "BFS"
date:   2018-3-10 12:44:00
categories: Algorithm
tags: Algorithm
excerpt: BFS&DFS in Python
mathjax: true
---

* content
{:toc}

Use a queue to implement this algorithm. If weight of each edge is same, we can use only BFS to traverse the graph to achieve shortest path. In dijkstra with adjacency list, BFS is used when we traverse the graph.


* The loop version of BFS
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

* Use generator to return all of the paths when implementing BFS
```Python
graph = {'A': set(['B', 'C']),
         'B': set(['A', 'D', 'E']),
         'C': set(['A', 'F']),
         'D': set(['B']),
         'E': set(['B', 'F']),
         'F': set(['C', 'E'])}

def bfs_paths(graph, start, goal):
    queue = [(start, [start])]
    while queue:
        (vertex, path) = queue.pop(0)#here deque with leftpop() O(1) is better than queue pop(0) O(n)
        for next in graph[vertex] - set(path):
            if next == goal:
                yield path + [next]
            else:
                queue.append((next, path + [next]))

print(list(bfs_paths(graph, 'A', 'F')))# [['A', 'C', 'F'], ['A', 'B', 'E', 'F']]
```
* Recursion version of BFS
```Python
#first result is the shortest path
def shortest_path(graph, start, goal):
    try:
        return next(bfs_paths(graph, start, goal))
    except StopIteration:
        return None

print("Shortest path is: ", shortest_path(graph, 'A', 'F'))# ['A', 'C', 'F']
```

Block Mathjax 

$$
f(x) = ax + b
$$

Inline Mathjax $a \neq b$

