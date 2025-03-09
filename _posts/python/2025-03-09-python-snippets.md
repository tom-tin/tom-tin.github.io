---
layout: post
title:  "Python - Useful code snippets"
date:   2025-03-09 09:34:10 +0700
categories: [python, example]
---

## General
### Chain Transformation with Pipe
~~~python
df = df.pipe(lambda d: d.rename(columns={'old_name': 'new_name'})).pipe(lambda d: d.query('new_name > 10'))
~~~

## Ref
- [10 Python One-Liners That Will Boost Your Data Preparation Workflow](https://machinelearningmastery.com/10-python-one-liners-that-will-boost-your-data-preparation-workflow/).

