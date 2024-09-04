---
layout: post
title:  "Pyspark - A few useful code snippets"
date:   2024-09-04 18:34:10 +0700
categories: [python, example]
---

~~~python
# ----------------------------------------
# --- find number of nulls for all cols
# ----------------------------------------
from pyspark.sql.functions import *
col_null_cnt_df =  df.select([count(when(col(c).isNull(),c)).alias(c) for c in df.columns])
display(col_null_cnt_df)
~~~