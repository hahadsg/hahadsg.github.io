### confusion matrix 混淆矩阵

| | 预测结果 | |
| :--- | :--- | :--- |
| 真实情况 | 正例 | 反例 |
| 正例 | TP（真正例） | FN（假反例） |
| 反例 | FP（假正例） | TN（真反例） |

$$
TPR = \frac{TP}{TP+FN} = recall \\
TNR = \frac{TN}{FP+TN} \\
FNR = \frac{FN}{TP+FN} \\
FPR = \frac{FP}{FP+TN} \\
$$

### precision 精确率 查准率

$$precision=\frac{TP}{TP+FP}$$

分母就是预测为正的，预测出为正，其中实际为正的比例

### recall 召回率 查全率

$$recall=\frac{TP}{TP+FN}$$

分母就是实际为正的，实际为正，其中被预测为正的比例

### F1

$$F1 
= \frac{1}{\frac{1}{2} \times (\frac{1}{P} + \frac{1}{R})}
= \frac{2\times P\times R}{P+R}
$$

其中，$$P=precision, R=recall$$

F1是基于precision和recall的调和平均值

https://github.com/hahadsg/Practice/blob/master/MachineLearning/python/metrics/F1_score.ipynb

### Fbeta

$$Fbeta
= \frac{1}{\frac{1}{1+\beta^2} \times (\frac{1}{P} + \frac{\beta^2}{R})}
= \frac{(1+\beta^2)\times P\times R}{(\beta^2\times P)+R}
$$

其中，$$P=precision, R=recall$$

$$\beta=1$$时退化为标准的$$F1$$；$$\beta\lt 1$$时$$P$$有更大影响；$$\beta\gt 1$$时$$R$$有更大影响

### ROC

https://github.com/hahadsg/Practice/blob/master/MachineLearning/python/metrics/ROC.ipynb

纵轴是TPR，横轴是FPR

### KS

$$KS = max(TPR - FPR)$$

### Cohen's Kappa

$$\kappa = \frac{p_o - p_e}{1 - p_e}
= 1 - \frac{1 - p_o}{1 - p_e}
$$

其中，
$$p_o = \frac{TP+TN}{TP+FP+FN+TN}$$

$$marginal_a = \frac{(TP+FN)(TP+FP)}{TP+FP+FN+TN}$$

$$marginal_b = \frac{(TN+FN)(TN+FP)}{TP+FP+FN+TN}$$

$$p_e = marginal_a + marginal_b$$

直观解释，$$p_o$$是准确率，$$p_e$$是baseline，也就是$$\kappa = 1 - \frac{error_{accuracy}}{error_{baseline}}$$

从这个角度看，当$$accuracy=baseline$$时，评分为0；当$$accuracy < baseline$$时，评分为负数；当$$accuracy > baseline$$时，评分为正数。也就是kappa衡量了准确率与baseline的差距

然后解释baseline是什么，它是一个基准线，假设一个二分类问题，正类占0.9，负类占0.1，如果预测的label中，正类占0.8，负类占0.2。那么随便进行预测的准确率是$$0.9*0.8+0.1*0.2=0.74$$，以这个值为基准线
