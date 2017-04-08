---
layout: post
title:  "Python - How to zip and upzip"
date:   2017-04-07 18:34:10 +0700
categories: [python, example]
---

~~~python
salaries_and_tenures = [(83000, 8.7), (88000, 8.1),
(48000, 0.7), (76000, 6),
(69000, 6.5), (76000, 7.5),
(60000, 2.5), (83000, 10),
(48000, 1.9), (63000, 4.2)]
x, y =zip(*salaries_and_tenures)#zip with * means un-zip

import matplotlib.pyplot as plt
%matplotlib inline
plt.scatter(x, y)
plt.show()

#try to zip the two list again
zipped = zip(y, x)
print(list(zipped))

#another way:
for salary, tenure in salaries_and_tenures:
    print(salary, tenure)
~~~

----------------
_Original source:_ [Grus-Data Science from scratch.](https://github.com/joelgrus/data-science-from-scratch/)
