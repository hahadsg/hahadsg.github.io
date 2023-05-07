## 参考文章

* sklearn model evaluation \([http://scikit-learn.org/stable/modules/model\_evaluation.html](http://scikit-learn.org/stable/modules/model_evaluation.html)\)

## 过拟合

* VC维的意义

VC维的实践意义是给机器学习可学性提供了理论支撑。
1. 测试集合的loss是否和训练集合的loss接近？VC维越小，理论越接近。
2. 训练集合的loss是否足够小？VC维越大，loss理论越小。
一般工业实践中通过引入正则对模型复杂度(VC维)进行控制，平衡这两个问题的矛盾。
http://www.flickering.cn/machine_learning/2015/04/vc%E7%BB%B4%E7%9A%84%E6%9D%A5%E9%BE%99%E5%8E%BB%E8%84%89/