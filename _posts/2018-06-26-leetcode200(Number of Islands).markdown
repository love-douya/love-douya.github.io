---
layout: post
title:  "Number of Islands(Leetcode200)"
date:   2018-06-26 21:21:00
categories: Algorithm Leetcode
tags: Algorithm Leetcode
---

* content
{:toc}

## Problem

Write a function to find the longest common prefix string amongst an array of strings.

If there is no common prefix, return an empty string "".

### Example 1

>* Input: ["flower","flow","flight"]
>* Output: "fl"

### Example 2

>* Input: ["dog","racecar","car"]
>* Output: ""
>* Explanation: There is no common prefix among the input strings.





### Python solution

```python

import sys

class Solution:
    def __init__(self, Graph):
        self.Graph = Graph

    def numIslands(self):
        """
        :type grid: List[List[str]]
        :rtype: int
        """
        flag = 2
        for i in range(len(self.Graph)):
            for j in range(len(self.Graph[0])):
                if self.Graph[i][j] == 0:
                    continue
                else:
                    if self.Graph[i][j] < flag and self.Graph[i][j] != 1:
                        continue
                    else:
                        self.Graph = self.DFS(self.Graph, i, j, flag)
                        flag += 1
        return flag - 2

    def DFS(self, Graph, i, j, flag):
        Graph[i][j] = flag
        if (i != 0) and Graph[i - 1][j] == 1:
            Graph[i - 1][j] = flag
            self.DFS(Graph, i - 1, j, flag)
        if (j != 0) and Graph[i][j - 1] == 1:
            Graph[i][j - 1] = flag
            self.DFS(Graph, i, j - 1, flag)
        if (i != len(Graph) - 1) and Graph[i + 1][j] == 1:
            Graph[i + 1][j] = flag
            self.DFS(Graph, i + 1, j, flag)
        if (j != len(Graph[0]) - 1) and Graph[i][j + 1] == 1:
            Graph[i][j + 1] = flag
            self.DFS(Graph, i, j + 1, flag)
        return Graph

if __name__ == "__main__":
    #Row Number
    sys.stdout.write("Input Row Number: \n")
    Row_Number = int(sys.stdin.readline())
    #Column Number
    sys.stdout.write("Input Column Number: \n")
    Column_Number = int(sys.stdin.readline())
    Graph = [[0 for j in range(Column_Number)] for i in range(Row_Number)]
    #Initialize Land And Sea
    sys.stdout.write("Input Value: \n")
    for i in range(0, Row_Number):
        for j in range(0, Column_Number):
            Graph[i][j] = int(sys.stdin.readline())
    sys.stdout.write("Result is: \n" + str(Solution(Graph).numIslands()))

```