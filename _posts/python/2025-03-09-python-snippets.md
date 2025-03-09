---
layout: post
title:  "Python - Useful code snippets"
date:   2025-03-09 09:34:10 +0700
categories: [python, example]
---

## General
- Chain Transformation with Pipe
~~~python
df = df.pipe(lambda d: d.rename(columns={'old_name': 'new_name'})).pipe(lambda d: d.query('new_name > 10'))
~~~

- Pivot Data with Multiple Aggregation
~~~python
import pandas as pd
import numpy as np

data = {
    'category': ['A', 'A', 'B', 'B', 'C', 'C'],
    'sub_category': ['X', 'Y', 'X', 'Y', 'X', 'Y'],
    'value': [10, 20, 30, 40, 50, 60]
}
df = pd.DataFrame(data)

pivot_df = df.pivot_table(index='category', columns='sub_category', values='value', aggfunc={'value': [np.mean, np.sum]})
~~~

- 


## Ref
- [10 Python One-Liners That Will Boost Your Data Preparation Workflow](https://machinelearningmastery.com/10-python-one-liners-that-will-boost-your-data-preparation-workflow/).

