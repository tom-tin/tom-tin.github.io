---
layout: post
title:  "Common Coding Question Patterns"
date:   2025-03-13 11:00:00 +0700
categories: [coding, problems, interview]
---

## Prefix Sum
* [YouTube source](https://www.youtube.com/watch?v=DjYZk8nrXVY&list=WL&index=1).
* [Colab notebook](https://colab.research.google.com/drive/1tFBTNkswFBVgUDWNZLzWdSmQjbQsHhYH#scrollTo=AUo2NXgBxdsr).
* Basic problem: find sum of elements in a sub-array.
  * Say you need to find sum of a[i] to a[j]. Then only need to loop through and add up. Hence only O(n).
* But if you have m queries (i.e. need to perform m different sums). Then if we simply repeat the above, we need O(mn). How to do it more efficiently?
*  


