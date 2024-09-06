---
layout: post
title:  "Pyspark - A few useful code snippets"
date:   2024-09-04 18:34:10 +0700
categories: [python, example]
---

### Exploring data
* Find the number of nulls for all cols
~~~python
from pyspark.sql.functions import *
col_null_cnt_df =  df.select([count(when(col(c).isNull(),c)).alias(c) for c in df.columns])
display(col_null_cnt_df)
~~~

### Interoperability with Python
Functions in pyspark.sql.functions apply to only to dataframe columns (instead of to python variables).

### A few useful functions
