### CNN中会出现一模一样的卷积的filter么？

### 人脸在图片不同位置都能识别的原因？

fast-ai-course：pooling会让图越来越小，所以不管在哪个位置最后都会缩小，神经网络会学习到

### 防止深度学习过拟合的方法？

1、增加数据集

2、数据增广

3、标准化（BatchNormalization）

4、正则化（Dropout、L1、L2）

5、减少模型复杂度

### 数据增广

旋转、放大最小、颜色调整

### Pseudo labeling

预测测试数据，然后将这些数据加入到训练集中

### 做额外的output 帮助模型预测更准(multi-task)

比如，fastai-lesson7中，识别鱼的类型时，增加包围框的识别，会提升鱼类型识别的准确度

### 局部最优解问题

深度学习一般参数会比较多，在高维度的学习中，不太会出现局部最优解，反而，最容易出现的是鞍点，在鞍点处，梯度下降得很慢

### 训练经验

https://towardsdatascience.com/a-bunch-of-tips-and-tricks-for-training-deep-neural-networks-3ca24c31ddc8



