## 1、特征工程是什么

![](/assets/feature_engineering/feature_engineering_frame.png)

## 2、数据预处理

未经处理的特征，常见的有以下问题：

* 不属于同一量纲：可以利用无量纲化解决这一问题。
* 信息冗余：对于某些定量特性，比如学习成绩，如果只关心“及格”和“不及格”，则可以将定量的分数转化成0和1来表示“不及格”和“及格”。二值化可以解决这一问题。
* 定性特征不能直接使用：通常使用哑编码的方式将定性特征转化为定量特征。
* 存在缺失值：需要补充缺失值。
* 信息利用率低

使用sklearn中的**preprocessing库**来进行数据预处理，可以覆盖以上问题的解决方案。

### 2.1无量纲化

#### 2.1.1标准化

标准化需要计算特征的均值和标准差，公式如下：

$$x' = \frac{x - \bar{X}}{S}$$

```py
from sklearn.preprocessing import StandardScaler, scale
StandardScaler().fit_transform(iris.data)
scale(iris.data)
```

#### 2.1.2区间缩放法

区间缩放法的思路有很多种，常用的一种为利用两个最值进行缩放，公式如下：

$$x' = \frac{x - Min}{Max - Min}$$

```py
from sklearn.preprocessing import MinMaxScaler, minmax_scale
MinMaxScale().fit_transform(iris.data)
minmax_scale(iris.data)
```

#### 2.1.3归一化

标准化是依据特征矩阵的列处理数据，通过求z-score的方法，将样本的特征值转化到同一量纲下。归一化是依照特征矩阵的行处理数据，其目的在于样本向量 在点乘运算或其他核函数计算相似性时，拥有统一的标准，也就是都转化成“单位向量”。规则为l2的归一化公式如下：

$$x' = \frac{x}{\sqrt{\sum^m_jx[j]^2}}$$

```py
from sklearn.preprocessing import Normalizer, normalize
Normalizer().fit_transform(iris.data)
normalize(iris.data)
```

### 2.2对定量特征二值化

定量特征二值化的核心需要定一个阈值，大于阈值的为1，小于等于阈值的为0，公式如下：

$$ f(x)=\left\{
\begin{aligned}
1, x > threshold \\
0, x \leq threshold \\
\end{aligned}
\right.$$

```py
from sklearn.preprocessing import Binarizer, binarize
# 二值化，阈值设置为3
Binarizer(threshold = 3).fit_transform(iris.data)
binarize(iris.data, threshold = 3)
```

### 2.3对定性变量哑编码

```py
from sklearn.preprocessing import OneHotEncoder
OneHotEncoder().fit_transform(iris.target.reshape((-1, 1)))
```

### 2.4缺失值计算

```
from numpy import vstack, array, nan
from sklearn.preprocessing import Imputer
# 参数missing_value为缺失值的表现形式，默认为NaN
# 参数strategy为缺失值填充方式，默认为‘mean’，可选'mean', 'median', 'most_frequent'
Imputer().fit_transform(vstack((array([nan, nan, nan, nan]), iris.data)))
```

### 2.5数据变换

常见的数据变换有基于多项式的、基于指数函数的、基于对数函数的。

* 多项式转化：
  4个特征，度为2的多项式转化公式如下：

$$
(x'_1,x'_2,x'_3,x'_4,x'_5,x'_6,x'_7,x'_8,x'_9,x'_{10},x'_{11},x'_{12},x'_{13},x'_{14},x'_{15}) \\
= (1,x_1,x_2,x_3,x_4,x_1^2,x_1x_2,x_1x_3,x_1x_4,x_2^2,x_2x_3,x_2x_4,x_3^2,x_3x_4,x_4^2)
$$

```py
from sklearn.preprocessing import PolynomialFeatures
# 参数degree为度，默认为2
PolynomialFeatures().fit_transform(iris.data)
```

* 基于单变元函数的数据变换

```py
from numpy import log1p
from sklearn.preprocessing import FunctionTransformer
# 第一个参数func是单变元函数
FunctionTransformer(log1p).fit_transform(iris.data)
```

### 2.6汇总

| 类 | 功能 | 说明 |
| :--- | :--- | :--- |
| StandardScaler | 无量纲化 | 标准化，基于特征矩阵的列，将特征值转换至服从标准正态分布 |
| MinMaxScaler | 无量纲化 | 区间缩放，基于最大最小值，将特征值转换到\[0, 1\]区间上 |
| Normalizer | 归一化 | 基于特征矩阵的行，将样本向量转换为“单位向量” |
| Binarizer | 二值化 | 基于给定阈值，将定量特征按阈值划分 |
| OneHotEncoder | 哑编码 | 将定性数据编码为定量数据 |
| Imputer | 缺失值计算 | 计算缺失值，缺失值可填充为均值等 |
| PolynomialFeatures | 多项式数据转换 | 多项式数据转换 |
| FunctionTransformer | 自定义单元数据转换 | 使用单变元的函数来转换数据 |

## 3、特征选择

数据预处理完以后，需要选择有意义的特征输入机器学习的算法和模型进行训练。通常从两个方面考虑：

* 特征是否发散：若一个特征的方差接近于0，则说明样本在这个特征上基本没有差异，这个特征对于样本的区分没有什么用。
* 特征与目标的相关性：与目标相关性高的特征，应当优先选择。

特征选择的方法分为以下3种：

Filter：过滤法，按照发散性或者相关性对每个特征进行评分，设定阈值或者待选择阈值的个数，选择特征

Wrapper：包装法，根据目标函数，每次选择若干特征，或者排除若干特征

Embedded：嵌入法，先使用某些机器学习算法和模型进行训练，得到各个特征的权值系数，根据系数从大到小选择特征。

使用sklearn中的**feature\_selection库**来进行特征选择。

### 3.1Filter

#### 3.1.1方差选择法

使用方差选择法，先计算每个特征的方差，然后根据阈值，选择大于阈值的特征。

```py
from sklearn.feature_selection import VarianceThreshold
VarianceThreshold(threshold = 3).fit_transform(iris.data) # 参数threshold为阈值
```

#### 3.1.2相关系数法

使用相关系数法，先要计算每个特征对目标值的相关系数以及相关系数的p值。

```
from sklearn.feature_selection import SelectKBest
from scipy.stats import pearsonr
# 选择k个最好的特征，返回选择特征后的数据
```

#### 3.1.3卡方检验

经典的卡方检验是检验定性自变量对定性因变量的相关性。

#### 3.1.4互信息法

经典的互信息法也是评价定性自变量对定性因变量的相关性，互信息法公式如下：

$$ I(X;Y) =
\sum\limits_{x{\in}X} \sum\limits_{y{\in}X}
p(x,y)log\frac{p(x,y)}{p(x)p(y)}$$

### 3.2Wrapper

#### 3.2.1递归特征消除法

这种方法使用一个基模型来进行多轮训练，每轮训练后，消除若干权值系数的特征，再基于新的特征集进行下一轮训练。

```
from sklearn.feature_selection import RFE
from sklearn.linear_model import LogisticRegression
# 参数estimator为基模型
# 参数n_features_to_select为选择的特征个数
RFE(estimator= LogisticRegression(), n_features_to_select = 2).fit_transform(iris.data, iris.target)
```

## 4、降维

**PCA是一种无监督的降维方法，LDA是一种有监督的降维方法。**

* 主成分分析法

```
from sklearn.decomposition import PCA
# 参数n_components为主成分数目
PCA(n_components = 2).fit_transform(iris.data)
```

* 线性判别分析法



