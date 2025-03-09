---
layout: post
title:  "Python - Useful code snippets"
date:   2025-03-09 09:34:10 +0700
categories: [python, example]
---
## Ref
- [10 Python One-Liners That Will Boost Your Data Preparation Workflow](https://machinelearningmastery.com/10-python-one-liners-that-will-boost-your-data-preparation-workflow/).


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

pivot_df = df.pivot_table(index='category', columns='sub_category', values='value',
                            aggfunc={'value': [np.mean, np.sum]})
~~~

- Time Series Resampling with Multiple Aggregation
    - Time series data resampling is a method of data summarization in a time-frequent manner we want, such as daily, weekly, monthly, etc. 

~~~python
df_resampled = df.set_index('timestamp').resample('D').agg({'value': ['mean', 'max'], 'count': 'sum'}).reset_index()
~~~

- Conditional Selection For Assigning Values

~~~python
import pandas as pd
import numpy as np

data = {
    'employee_id': [1, 2, 3, 4, 5],
    'name': ['Alice', 'Bob', 'Charlie', 'David', 'Eve'],
    'salary': [3500, 5000, 2500, 8000, 1000]
}
df = pd.DataFrame(data)

df['salary_level'] = np.select(
    [df['salary'] = 3000) & (df['salary']  6000],
    ['Low', 'Medium', 'High']
~~~

- Conditional Replacement For Several Columns

~~~python
df = df.pipe(lambda d: d.rename(columns={'old_name': 'new_name'})).pipe(lambda d: d.query('new_name > 10'))
~~~

- Multiple Columns Combination
    - Not necessarily work for numerical data, more for text data. 

~~~python
df['combined'] = df[['col1', 'col2', 'col3']].astype(str).agg('_'.join, axis=1)
~~~

- Column Splitting

~~~python
df[['first', 'last']] = df['full_name'].str.split(' ', n=1, expand=True)
~~~

- Outlier Identification and Removal

~~~python
df['capped'] = df['value'].clip(lower=df['value'].quantile(0.05), upper=df['value'].quantile(0.95))
~~~

- Merge Multiple DataFrame with Reduce
    - Without having to manually merge with intermediate dataframes. Not sure about speed improvement. 

~~~python
import pandas as pd
from functools import reduce

df1 = pd.DataFrame({'key': [1, 2, 3], 'A': ['a1', 'a2', 'a3']})
df2 = pd.DataFrame({'key': [2, 3, 4], 'B': ['b2', 'b3', 'b4']})
df3 = pd.DataFrame({'key': [3, 4, 5], 'C': ['c3', 'c4', 'c5']})

list_of_dfs = [df1, df2, df3]

df_merged = reduce(lambda left, right: pd.merge(left, right, on='key', how='outer'), list_of_dfs)
~~~

-  DataFrame Query Optimization with Eval
    - Creating a new column based on a DataFrame calculation might take some time, especially if the data are large.
    - To optimize this process, we can use the Pandas eval() function. By using a procedure similar to the query() function, eval() can improve the execution time while reducing the need for an intermediate object.  

~~~python
df = df.eval("col3 = (col1 * 0.8 + col2 * 0.2) / col4", inplace=False)
~~~
