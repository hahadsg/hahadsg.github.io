## 遇到的问题

* apply\_along\_axis产生的类型会以第一行为准

```py
# apply_along_axis产生的类型会以第一行为准
In [3]: a
Out[3]: [['a', 'b'], ['cc', 'dd']]

In [7]: np.apply_along_axis(lambda x: '.'.join(x), 1, a)
Out[7]: 
array(['a.b', 'cc.'], 
      dtype='<U3')
```

* np.var和np.cov的方差计算方式不同

```py
In [3]: a = np.array([[1,2,3], [2,3,4]])

# 平方误差和
In [4]: ((a[0] - a[0].mean()) ** 2).sum()
Out[4]: 2.0

# 平方误差和/n
In [5]: np.var(a[0])
Out[5]: 0.66666666666666663

# 平方误差和/(n-1)
In [6]: np.cov(a)
Out[6]: 
array([[ 1.,  1.],
       [ 1.,  1.]])
```

## 技巧

### One-Hot

```py
>>> a = np.array([1, 0, 3])
>>> b = np.zeros((3, 4))
>>> b[np.arange(3), a] = 1
>>> b
array([[ 0.,  1.,  0.,  0.],
       [ 1.,  0.,  0.,  0.],
       [ 0.,  0.,  0.,  1.]])
```



