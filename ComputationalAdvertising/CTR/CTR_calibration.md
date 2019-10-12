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

参考：[Logistic Regression in Rare
Events Data](https://gking.harvard.edu/files/0s.pdf)

## Weighting

直接调整class weights，不过好像基本都用上面的方法

