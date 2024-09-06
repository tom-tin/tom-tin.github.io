---
layout: post
title:  "Pyspark - A few useful code snippets"
date:   2024-09-04 18:34:10 +0700
categories: [python, example]
---
<span style="color:blue">I will keep adding more tips as I found them useful.</span>

### Exploring data
* Find the number of nulls for all cols
~~~python
col_null_cnt_df =  df.select([count(when(col(c).isNull(),c)).alias(c) for c in df.columns])
~~~

### Interoperability with Python
* **Functions**: In pyspark.sql.functions apply to only to dataframe columns (instead of to python variables). Hence, if you do:
~~~python
from pyspark.sql.functions import sqrt
~~~
then you would need to explicitly use np.sqrt() on a python variable.

* **Data types**: If you use np.sqrt() on a variable, the returned value is of type np.float64, which is not accepted by a df in  pyspark. A solution is to use np.sqrt().item() which returns type float and this is accepted by pyspark.

### A few useful functions
