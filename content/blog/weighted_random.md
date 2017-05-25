+++
date = "2017-05-25T11:10:23+08:00"
title = "python 加权随机"

+++

经常会遇到一种场景，从一堆数据中随机选择一个，一般用`random`模块就能解决，如果这些数据被选择的概率不同，就需要在`random`的基础上再做些改造。

<script src="https://gist.github.com/c1ay/8a89ebc4b6655f668d2390ef0779ee50.js"></script>



```python
In [6]: WeightedRandomGenerator([1, 3, 4, 2])()
Out[6]: 2

In [7]: WeightedRandomGenerator([1, 3, 4, 2])()
Out[7]: 0

In [8]: WeightedRandomGenerator([1, 3, 4, 2])()
Out[8]: 2

In [9]: WeightedRandomGenerator([1, 3, 4, 2])()
Out[9]: 1
```

返回随机结果的索引值。