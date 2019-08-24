## 问题

* 中文画图时乱码

```py
# 解决matplotlib乱码问题
import matplotlib.pyplot as plt
plt.rcParams['font.family'] = 'sans-serif'
plt.rcParams['font.sans-serif']= ['SimHei'] #用来正常显示中文标签
plt.rcParams['axes.unicode_minus'] = False #用来正常显示负号

# 直接修改配置文件
import matplotlib
matplotlib.matplotlib_fname() #将会获得matplotlib包所在文件夹 去该文件修改上述参数

# 解决seaborn乱码问题（matplotlib不会出现乱码，引入seaborn又出现乱码）
import seaborn as sns
sns.set_style({'font.sans-serif':['simhei','Arial']})
```



