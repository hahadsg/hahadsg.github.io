# argparse

```python
import parser

parser = argparse.ArgumentParser
parser.add_argument('-p', '--path', type=str, default='./test/3.png', help="ocr image path")
args = parser.parse_args()
```

https://www.jianshu.com/p/fef2d215b91d

# getopt

* 例1)

```
>>> import getopt

>>> args = '-a -b -cfoo -d bar a1 a2'.split()  
>>> args  
['-a', '-b', '-cfoo', '-d', 'bar', 'a1', 'a2']  
>>> optlist, args = getopt.getopt(args, 'abc:d:')  
>>> optlist  
[('-a', ''), ('-b', ''), ('-c', 'foo'), ('-d', 'bar')]  
>>> args
['a1', 'a2']
```

* 例2) long option

```
>>> s = '--condition=foo --testing --output-file abc.def -x a1 a2'  
>>> args = s.split()  
>>> args  
['--condition=foo', '--testing', '--output-file', 'abc.def', '-x', 'a1', 'a2']  
>>> optlist, args = getopt.getopt(args, 'x', [  
... 'condition=', 'output-file=', 'testing'])  
>>> optlist  
[('--condition', 'foo'), ('--testing', ''), ('--output-file', 'abc.def'), ('-x', '')]  
>>> args  
['a1', 'a2'] 
```