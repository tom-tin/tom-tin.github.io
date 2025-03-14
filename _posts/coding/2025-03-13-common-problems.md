---
layout: post
title:  "Common Coding Question Patterns"
date:   2025-03-13 11:00:00 +0700
categories: [coding, problems, interview]
---

## Pattern 1: Prefix Sum
* [YouTube source](https://www.youtube.com/watch?v=DjYZk8nrXVY&list=WL&index=1).
* [Colab notebook](https://colab.research.google.com/drive/1tFBTNkswFBVgUDWNZLzWdSmQjbQsHhYH#scrollTo=AUo2NXgBxdsr).
* Basic problem: find sum of elements in a sub-array.
  * Say you need to find sum of a[i] to a[j]. Then only need to loop through and add up. Hence only O(n).
* But if you have m queries (i.e. need to perform m different sums). Then if we simply repeat the above, we need O(mn). How to do it more efficiently?
* Example of single query:
~~~python
# single query
def find_subarray_sum(array, i, j):
    subarray_sum = 0
    for k in range(i, j+1):
        subarray_sum += array[k]
    return subarray_sum
~~~
* Idea: create a **prefix summary**, where value at index i is the sum of all elements from start up to index i.
  * p[i] = a[0] + a[1] + ... + a[i]
  * Now, you can do one query in just O(1):
  * sum[i,j] = p[j] - p[i-1]
  * If there is also a space constraint (you are not allow to create a new array to store p, then you can modify the input array itself), e.g:
~~~python
def create_prefix_sum(array):
    for i in range(1, len(array)):
        array[i] = array[i-1] + array[i]
    return array
~~~

* Related Leetcode problems:
  * 303. Range Sum Query - Immutable.
  * 525. Contiguous array
  * 560. Subarray sum equals K.
   
* **303. Range Sum Query - Immutable**.
 * Given an integer array nums, and multiple queries, each query is a pair of indices [i,j], return corresponding sums of these queries. Each sum is the sum of elements between the indices i, and j, inclusively
~~~python
   '''
["NumArray", "sumRange", "sumRange", "sumRange"]
[[-2, 0, 3, -5, 2, -1], [0, 2], [2, 5], [0, 5]]
Output
[null, 1, -1, -3]
'''
~~~

* **525. Contiguous array**.

* **560. Subarray sum equals K.**.

