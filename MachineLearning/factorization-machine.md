## FM(Factorization Machine)

FM是为了解决稀疏数据下的特征组合问题

假设一个分类问题（预测搜索广告场景下用户是否点击广告）

Country|Ad_type|Ad_location|is_clicked
---|---|---|---
USA|Link|North|1
China|Picture|East|1
China|Link|East|0

其中，Country、Ad_type、Ad_location是特征，is_clicked
是label。这三个特征都是categoricall类型的，所以需要进行one-hot encoding，得到

Country=USA|Country=China|Ad_type=Link|Ad_type=Picture|Ad_location=North|Ad_location=East|label
---|---|---|---|---|---|---|
1|0|1|0|1|0|1
0|1|0|1|0|1|1
0|1|1|0|0|1|0

可以看到，现在数据变得非常稀疏，另外，经过one-hot encoding后，特征空间也会变得非常大。

在实际业务中，两个特征组合可能是很有意义的。比如图片广告放在北区用户不太会点（并不一定真实 我的猜想，有种很明显广告的即视感，用户就直接翻下去）

根据上述思路，建立模型：

$$y(x) = w_0 + \sum\limits^n_{i=1}w_ix_i + \sum\limits^n_{i=1}\sum\limits^n_{j=i+1}w_{ij}x_ix_j$$

这里暂时只有特征两两间的关系，两个以上特征组合暂时不讨论，这里的x是已经one-hot后的特征

我们假设特征组合的参数$$w_{ij}$$组成的矩阵为$$W$$，那么它的大小就是$$n\times n$$，这将会非常大

所以FM做的就是将$$W$$进行分解，$$W=VV^T$$，$$V$$可以理解为是特征的隐变量（很像Embedding），$$V$$的大小是$$n\times k$$，$$V$$的第$$j$$行便是第$$j$$维特征的隐变量，所以$$w_{ij} = \left< v_i, v_j \right>$$

而$$k \ll n$$，那么参数的数量就大幅度变少了

那FM的模型为：

$$y(x) = w_0 + \sum\limits^n_{i=1}w_ix_i + \sum\limits^n_{i=1}\sum\limits^n_{j=i+1}\left< v_i, v_j \right>x_ix_j$$

另外，参数因子化使得$$w_{hi}$$和$$w_{ij}$$不再独立，（$$w_{hi} = \left< v_h, v_i \right>$$，$$w_{ij} = \left< v_i, v_j \right>$$

），而在线性模型中它们是独立的

上式的复杂度是$$O(kn^2)$$。但是，上式可以化简为：

$$\sum\limits^n_{i=1}\sum\limits^n_{j=i+1}\left< v_i, v_j \right>x_ix_j = \frac{1}{2}\sum\limits^k_{f=1}\left(\left( \sum\limits^n_{i=1}v_{i,f}x_i \right)^2 - \sum\limits^n_{i=1}v_{i,f}^2x_i^2 \right)$$

这里下标$$f$$代表$$v_i$$的第$$f$$个值，化简后复杂度为$$O(kn)$$，所以FM是种很高效的模型

**个人感想**：模型的式子中$$x_ix_j$$其实有很多都是0，实际实现不一定要完全根据式子来，可以用像Embedding那样，直接索引获取隐变量，也就是不将原特征进行one-hot encoding，这样可以省很多时间。

## FFM(Field Factorization Machine)

FFM引入了field概念，将同一个原特征的特征归为同一个field，如：将Country_USA、Country_China归为同一个field。如果有$$f$$个原变量，那么就有$$f$$个field

而$$x_i$$对应的隐变量，从FM的唯一的$$v_i$$，变成FFM的$$v_{i,f_j}$$，$$j$$是跟$$x_i$$组合的另外一个特征，也就是隐变量的数量是之前的$$f$$倍

模型变成：

$$y(x) = w_0 + \sum\limits^n_{i=1}w_ix_i + \sum\limits^n_{i=1}\sum\limits^n_{j=i+1}\left< v_{i,f_j}, v_{j,f_i} \right>x_ix_j$$

不过，FFM的模型没法化简，也就是预测的复杂度为$$O(kn^2)$$


## 参考

https://tech.meituan.com/deep-understanding-of-ffm-principles-and-practices.html
