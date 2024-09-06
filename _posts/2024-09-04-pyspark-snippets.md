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
* Get a list of distinct values on a column.
~~~python
user_list = [row.user_pin[0] for row in df.select('user_pin').distinct().collect()]
~~~
A less-efficient way, but worth noting:
~~~python
user_list = list(df.toPandas()['user_pin'].value_counts().keys())
~~~
* Sorting
~~~python
df.sort(desc('col1'), asc('col2')).show()
# col2 is considered ascending only if there is a tie in col1
~~~

### Interoperability with Python
Sometimes, you have to switch back and forth between python and pyspark (due to scalability vs flexibility). The following tips can help.
* **Functions**: In pyspark.sql.functions apply to only to dataframe columns (instead of to python variables). Hence, if you do:
~~~python
from pyspark.sql.functions import sqrt
~~~
then you would need to explicitly use np.sqrt() on a python variable. Hence, it's a good practice to import only the functions you need to improve speed and avoid overwriting other functions in python.

* **Data types**: If you use np.sqrt() on a variable, the returned value is of type np.float64, which is not accepted by a df in  pyspark. A solution is to use np.sqrt().item() which returns type float and this is accepted by pyspark.

### Interoperability with SQL
* Either way works:
~~~python
df.filter(col("act_date").between("2016-10-01", "2017-04-01"))
df.filter("act_date BETWEEN '2016-10-01' AND '2017-04-01'")
~~~
* Be careful with some differences between the two. For example, you need to extract a sub-string from a string. These usually rely on the starting and ending index/character that you want to extract. While python's indexing starts from 0, SQL's indexing starts from 1.


### A few useful functions
I will find a way to add these later. It takes a lot of space.


### Miscellaneous tips
* Don't create variables with names reserved for functions (e.g., `col`). 
