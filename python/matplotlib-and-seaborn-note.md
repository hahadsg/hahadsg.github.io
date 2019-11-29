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

## demo

* 将图片集画出nrows * ncols的fig

```
nplt = 21
ncols = 4
nrows = (nplt + ncols - 1) // ncols

fig, ax = plt.subplots(nrows, ncols, figsize=(27, nrows*4), dpi=150)

i = 0
for img_info in img_list:
    img_path = img_info['img_path']
    if not os.path.exists(img_path):
        continue
    img = misc.imread(icon_path)
    if not img.shape:
        continue

    row = i // ncols
    col = i % ncols
    ax[row][col].imshow(img)
    ax[row][col].set_title(img_info['title'], fontsize=15)

    i += 1
    if i >= nplt:
        break
```


