---
title: CTR_calibration
date: 2019-10-12
update_date: 2019-10-12
---

## Prior Correction

原始CTR为：

$$
CTR = \sigma\left( \beta \right)
$$

校准后为：

$$
CTR' = \sigma\left\{ \beta - ln\left[ \left(\frac{1-\tau}{\tau}\right) \left(\frac{\bar{y}}{1-\bar{y}}\right) \right]\right\}
\approx \sigma\left[ \beta - ln\left( \frac{\bar{y}}{\tau}\right) \right]
$$

其中，$$\tau$$是真实正样本比例，$$\bar{y}$$是训练集中正样本比例

此方法认为CTR由于采样比例以及正负样本比例的原因引起误差，一般用于LR的CTR校准

参考：[Logistic Regression in Rare
Events Data](https://gking.harvard.edu/files/0s.pdf)

facebook用了此方法：[Practical Lessons from Predicting Clicks on Ads at Facebook](http://quinonero.net/Publications/predicting-clicks-facebook.pdf)

## Weighting

直接调整class weights

## Isotonic Regression (保序回归)

流程（生成reliability diagram，运行Isotonic Regression）：

1. 准备一份验证集（为了防止过拟合）
2. 将点击率[0, 1]的区间划分为N个桶，每个桶长度小童，比如$$N = 10^5$$
3. 将点击率放入这些桶中
4. 对于每一个桶，都计算其真实的点击率，做一个映射，这N个桶构成了reliability diagram
5. 使用生成的reliability diagram运行Isotonic Regression（比如PAV算法）

pool adjacent violators algorithm (PAVA, PAV)：

  待补充

google用了此方法：[Ad click prediction: a view from the trenches](https://static.googleusercontent.com/media/research.google.com/zh-CN//pubs/archive/41159.pdf)
