---
layout: post
title:  "Sort Algorithms"
date:   2018-3-25 17:18:00
categories: Algorithm
tags: Algorithm
---

* content
{:toc}

## Bubble Sort
Bubble Sort is the simplest sorting algorithm that works by repeatedly swapping the adjacent elements if they are in wrong order.

![Bubble Sort](https://raw.githubusercontent.com/love-douya/love-douya.github.io/master/Bubble%20Sort.gif)

```python
def bubbleSort(arr):
    for i in range(1, len(arr)):
        for j in range(0, len(arr) - i):
            if arr[j] > arr[j + 1]:
                arr[j], arr[j + 1] = arr[j + 1], arr[j]
    return arr

print(bubbleSort([12, 2, 8, 1, 23]))
```