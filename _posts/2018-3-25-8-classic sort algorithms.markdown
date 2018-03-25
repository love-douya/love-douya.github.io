---
layout: post
title:  "8 classic sort algorithms"
date:   2018-3-25 17:18:00
categories: Algorithm
tags: Algorithm Sort
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

## Selection Sort
selection sort is a sorting algorithm, specifically an in-place comparison sort. It has O(n2) time complexity, making it inefficient on large lists, and generally performs worse than the similar insertion sort. Selection sort is noted for its simplicity, and it has performance advantages over more complicated algorithms in certain situations, particularly where auxiliary memory is limited.

![Selection Sort](https://raw.githubusercontent.com/love-douya/love-douya.github.io/master/Bubble%20Sort.gif)

```python
def selectionSort(arr):
    for i in range(len(arr) - 1):
        minIndex = i
        for j in range(i + 1, len(arr)):
            if arr[j] < arr[minIndex]:
                minIndex = j
        if i != minIndex:
            arr[i], arr[minIndex] = arr[minIndex], arr[i]
    return arr

arr = [12,3,4,6,1]
print(selectionSort(arr))
```

## Insertion Sort
Insertion sort iterates, consuming one input element each repetition, and growing a sorted output list. At each iteration, insertion sort removes one element from the input data, finds the location it belongs within the sorted list, and inserts it there. It repeats until no input elements remain.

![Insertion Sort](https://raw.githubusercontent.com/love-douya/love-douya.github.io/master/Bubble%20Sort.gif)

```python
def insert_sort(lists):
    #insert sort
    count = len(lists)
    for i in range(1, count):
        key = lists[i]
        j = i - 1
        while j >= 0:
            if lists[j] > key:
                lists[j + 1] = lists[j]
                lists[j] = key
            j -= 1
    return lists

list_test = [3,8,1,2,10,12]
result = insert_sort(list_test)
print(result)
```