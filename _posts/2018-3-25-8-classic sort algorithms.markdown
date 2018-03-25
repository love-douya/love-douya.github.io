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

![Bubble Sort](https://raw.githubusercontent.com/love-douya/love-douya.github.io/master/picture/Bubble%20Sort.gif)

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

![Selection Sort](https://raw.githubusercontent.com/love-douya/love-douya.github.io/master/picture/Selection%20Sort.gif)

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

![Insertion Sort](https://raw.githubusercontent.com/love-douya/love-douya.github.io/master/picture/Insertion%20Sort.gif)

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

## Shell Sort
Shellsort is an in-place comparison sort. It can be seen as either a generalization of sorting by exchange (bubble sort) or sorting by insertion (insertion sort).The method starts by sorting pairs of elements far apart from each other, then progressively reducing the gap between elements to be compared. Starting with far apart elements, it can move some out-of-place elements into position faster than a simple nearest neighbor exchange.

![Shell Sort](https://raw.githubusercontent.com/love-douya/love-douya.github.io/master/picture/Shell%20Sort.gif)

```python
def shellsort(alist):
    sublistcount = len(alist) // 2
    while sublistcount > 0:
        for startposition in range(sublistcount):
            gap_insertion_sort(alist, startposition, sublistcount)
        print("After increments of size", sublistcount, "The list is", alist)
        sublistcount = sublistcount // 2

def gap_insertion_sort(alist, start, gap):
    for i in range(start+gap, len(alist), gap):
        currentvalue = alist[i]
        position = i       
        while position >= gap and alist[position - gap] > currentvalue:
            alist[position] = alist[position - gap]
            position = position - gap
        alist[position] = currentvalue

alist = [54, 26, 93, 17, 77, 31, 44, 55, 20]
shellsort(alist)
print(alist)
```

## Merge Sort
Merge sort works as follows:
1. Divide the unsorted list into n sublists, each containing 2. Element (a list of 1 element is considered sorted).
Repeatedly merge sublists to produce new sorted sublists until there is only 1 sublist remaining. This will be the sorted list.

![Merge Sort](https://raw.githubusercontent.com/love-douya/love-douya.github.io/master/picture/Merge%20Sort.gif)

```python
def mergeSort(arr):
    import math
    if(len(arr) < 2):
        return arr
    middle = math.floor(len(arr) / 2)
    left, right = arr[0:middle], arr[middle:]
    return merge(mergeSort(left), mergeSort(right))

def merge(left, right):
    result = []
    while left and right:
        if left[0] <= right[0]:
            result.append(left.pop(0))
        else:
            result.append(right.pop(0))
    while left:
        result.append(left.pop(0))
    while right:
        result.append(right.pop(0))
    return result

arr = [14,4,5,6,2,9]
arr_after_sort = mergeSort(arr)
print(arr_after_sort)
```
## Heap Sort
Heapsort is a comparison-based sorting algorithm. Heapsort can be thought of as an improved selection sort: like that algorithm, it divides its input into a sorted and an unsorted region, and it iteratively shrinks the unsorted region by extracting the largest element and moving that to the sorted region. The improvement consists of the use of a heap data structure rather than a linear-time search to find the maximum.

![Heap Sort](https://raw.githubusercontent.com/love-douya/love-douya.github.io/master/picture/Heap%20Sort.gif)

```python
def swap(i, j):
    sqc[i], sqc[j] = sqc[j], sqc[i]

def heapify(end, i):
    l = 2 * i + 1
    r = 2 * (i + 1)
    max = i
    if l < end and sqc[i] < sqc[l]:
        max = l
    if r < end and sqc[max] < sqc[r]:
        max = r
    if max != i:
        swap(i, max)
        heapify(end, max)
        
def heap_sort():
    end = len(sqc)
    start = end // 2 - 1 #use // instead of /
    for i in range(start, -1, -1):
        heapify(end, i)
    for i in range(end - 1, 0, -1):
        swap(i, 0)
        heapify(i, 0)

sqc = [0, -5, 1, -9, 11, 3, 10]
heap_sort()
print(sqc)
```

## Quick Sort
Quicksort (sometimes called partition-exchange sort) is an efficient sorting algorithm, serving as a systematic method for placing the elements of an array in order. When implemented well, it can be about two or three times faster than its main competitors, merge sort and heapsort.

![Quick Sort](https://raw.githubusercontent.com/love-douya/love-douya.github.io/master/picture/Quick%20Sort.gif)

```python
def quicksort(alist):
    quick_sort_helper(alist, 0, len(alist) - 1)

def quick_sort_helper(alist, first, last):
    if first < last:
        splitpoint = partition(alist, first, last)

        quick_sort_helper(alist, first, splitpoint - 1)
        quick_sort_helper(alist, splitpoint + 1, last)
        
def partition(alist, first, last):
    pivotvalue = alist[first]

    leftmark = first + 1
    rightmark = last

    done = False
    while not done:
                
        while leftmark <= rightmark and alist[leftmark] <= pivotvalue:
            leftmark = leftmark + 1  

        while rightmark >= leftmark and alist[rightmark] >= pivotvalue:
            rightmark = rightmark - 1          
        
        if rightmark < leftmark:
            done = True
        else:
            temp = alist[leftmark]
            alist[leftmark] = alist[rightmark]
            alist[rightmark] = temp

    temp = alist[first]
    alist[first] = alist[rightmark]
    alist[rightmark] = temp

    return rightmark

alist = [12, 1, 2, 3, 4, 5, 6, 7, 11]
quicksort(alist)
print(alist)
```
## Counting Sort
Counting sort is an algorithm for sorting a collection of objects according to keys that are small integers; that is, it is an integer sorting algorithm. It operates by counting the number of objects that have each distinct key value, and using arithmetic on those counts to determine the positions of each key value in the output sequence. Its running time is linear in the number of items and the difference between the maximum and minimum key values, so it is only suitable for direct use in situations where the variation in keys is not significantly greater than the number of items.

![Counting Sort](https://raw.githubusercontent.com/love-douya/love-douya.github.io/master/picture/Counting%20Sort.gif)

```python
def Counting_Sort(A, B, k):
    C = [None] * k
    for i in range(0, k):
        C[i] = 0
    for j in range(0, len(A)):
        C[A[j]] += 1 # C[i] now contains the number of elements equal to i.
    for i in range(1, k):
        C[i] = C[i] + C[i - 1] # C[i] now contains the number of elements less than or equal to i.
    for j in range(0, len(A)):
        B[C[A[j]] - 1] = A[j]
        C[A[j]] -= 1

A = [2, 5, 3, 0, 2, 3, 0, 3]
B = [None] * len(A)
Counting_Sort(A, B, 6)
print(B)
```