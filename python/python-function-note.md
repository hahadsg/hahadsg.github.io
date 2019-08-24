### zip

* zip and unzip

```py
In [18]: a = [[1,2,3], [4,5,6]]

In [22]: list(zip(*a))
Out[22]: [(1, 4), (2, 5), (3, 6)]

In [23]: z = list(zip(*a))

In [24]: list(zip(*z))
Out[24]: [(1, 2, 3), (4, 5, 6)]
```