# Trick
-----

## to clipboard

```py
from pandas.io import clipboard
clipboard.clipboard_set(text)
```

## flatten multiIndex

```py
['_'.join(col) for col in pkg_pivot.columns.values]
```

## .ix deprecated

```python
df.iloc[:, [df.columns.get_loc('target')]]
```

## explode list

```python
df[target_column].apply(lambda x: x.split('，')) \
    .apply(pd.Series) \
    .stack() \
    .reset_index(level=1, drop=True) \
    .to_frame(new_name) \
    .join(df)
```

## read/write

### write to excel multi-sheet

```python
df1 = pd.DataFrame({'Data': [11, 12, 13, 14]})
df2 = pd.DataFrame({'Data': [21, 22, 23, 24]})
df3 = pd.DataFrame({'Data': [31, 32, 33, 34]})

writer = pd.ExcelWriter('./test.xlsx', engine='xlsxwriter')

df1.to_excel(writer, sheet_name='Sheet1')
df2.to_excel(writer, sheet_name='Sheet2')
df3.to_excel(writer, sheet_name='Sheet3')

writer.save()
```

# Problem
-----

## 关于copy

* copy\(\) 只会拷贝index和data，如果data是object不会进行深度拷贝

```py
In [1]: import pandas as pd

In [2]: class test(object):
   ...:     def __init__(self, x):
   ...:         self.x = x
   ...: 

In [3]: df = pd.DataFrame({'A': [test(1), test(3)]})

In [4]: df
Out[4]: 
                                       A
0  <__main__.test object at 0x105aec908>
1  <__main__.test object at 0x105aec940>
```

copy\(\)只会对index和data进行拷贝，如果data是object不会进行深度拷贝

```py
In [5]: df2 = df.copy() 

In [6]: df2
Out[6]: 
                                       A
0  <__main__.test object at 0x105aec908>
1  <__main__.test object at 0x105aec940>
```

用python自带的包进行deepcopy

```py
In [7]: import copy

In [8]: df3 = copy.deepcopy(df)

In [9]: df3
Out[9]:
A
0 <__main__.test object at 0x105b0e1d0>
1 <__main__.test object at 0x105b0e080>
```

## 关于Warning: A value is trying to be set on a copy of a slice from a DataFrame.

* 这个问题很奇怪，如果df2是df的拷贝，那就不应该报警告；而df2是df的引用，那df2修改时df没有修改···

```py
In [18]: df = pd.DataFrame({
   ....:         'A': np.random.randn(5), 
   ....:         'B': np.random.randn(5), 
   ....:         'C': np.random.randn(5), 
   ....:     })

In [19]: df
Out[19]: 
          A         B         C
0  0.778093  0.534797 -0.271507
1  1.536066  0.078380  0.028316
2 -0.429115 -2.397360 -0.766024
3 -0.154933 -0.045179  0.350458
4 -0.520098  1.142862  0.461002

In [20]: df2 = df.loc[df['A'] < 0.1, :]

In [21]: df2
Out[21]: 
          A         B         C
2 -0.429115 -2.397360 -0.766024
3 -0.154933 -0.045179  0.350458
4 -0.520098  1.142862  0.461002

In [22]: df2['B'] = 1
/Library/Frameworks/Python.framework/Versions/3.5/bin/ipython:1: SettingWithCopyWarning: 
A value is trying to be set on a copy of a slice from a DataFrame.
Try using .loc[row_indexer,col_indexer] = value instead

See the caveats in the documentation: http://pandas.pydata.org/pandas-docs/stable/indexing.html#indexing-view-versus-copy
  #!/Library/Frameworks/Python.framework/Versions/3.5/bin/python3.5

In [23]: df2
Out[23]: 
          A  B         C
2 -0.429115  1 -0.766024
3 -0.154933  1  0.350458
4 -0.520098  1  0.461002

In [24]: df
Out[24]: 
          A         B         C
0  0.778093  0.534797 -0.271507
1  1.536066  0.078380  0.028316
2 -0.429115 -2.397360 -0.766024
3 -0.154933 -0.045179  0.350458
4 -0.520098  1.142862  0.461002
```

## 关于groupby.apply

* 很奇怪 groupby后apply会对每一行都进行计算

```py
In [4]: df = pd.DataFrame({'a':[1,1,3], 'b':[2,3,4]})

In [5]: def test(x):
   ...:     print(x)
   ...:     return x.sum()
   ...: 

In [6]: df.groupby('a').apply(test)
   a  b
0  1  2
1  1  3
   a  b
0  1  2
1  1  3
   a  b
2  3  4
Out[6]: 
   a  b
a      
1  2  5
3  3  4
```

## 关于pivot\_table

* 如果value中又空值，而aggfunc又不能处理空值，则会出错

```py
In [9]: a = pd.DataFrame({
   ...:     'a': [1, 2, 1, 2, 2],
   ...:     'b': [1, 1, 2, 2, 2],
   ...:     'c': ['1', '1', '1', '1', None],
   ...: })
   ...: 
In [12]: a.pivot_table('c', 'a', 'b', aggfunc=lambda s: '+'.join(s)) # 出错了
Out[12]: 
b      1      2
a              
1  a+b+c  a+b+c
2  a+b+c  a+b+c

In [13]: a.pivot_table('c', 'a', 'b', aggfunc=lambda s: '+'.join(s.fillna(''))) # 没问题
Out[13]: 
b  1   2
a       
1  1   1
2  1  1+
```




