## 极大似然估计解释

$$\hat{y}$$是给定$$x$$对$$y=1$$的估计:
$$\hat{y} = P(y=1\rvert x)$$

所以，$$1-\hat{y} = P(y=0\rvert x)$$

归纳起来，$$P(y\rvert x)=\hat{y}^y (1-\hat{y})^{1-y}$$

则$$log(P(y\rvert x))=y*log(\hat{y})+(1-y)*log(1-\hat{y})$$

那对于所有的样本，用极大似然估计：

$$L=\prod P(y^{(i)}\rvert x^{(i)})$$

取对数似然，

$$l=log(\prod P(y^{(i)}\rvert x^{(i)}))=\sum y*log(\hat{y})+(1-y)*log(1-\hat{y})$$

由于要最大化$$l$$，那我们的损失函数要加上负号，

$$J=-\sum y*log(\hat{y})+(1-y)*log(1-\hat{y})$$

## 求导

$$z = Wx + b$$

$$\hat{y} = \sigma(z) = \sigma(Wx + b)$$

$$J = -y \bullet log(\hat{y}) - (1-y) \bullet log(1-\hat{y})$$

$$\frac{\partial J}{\partial \hat{y}} = \frac{\hat{y} - y}{\hat{y}(1-\hat{y})}$$

$$\frac{\partial \hat{y}}{\partial z} = \hat{y}(1-\hat{y})$$

$$\frac{\partial J}{\partial z} = \frac{\partial J}{\partial \hat{y}} \bullet \frac{\partial \hat{y}}{\partial z} = \hat{y} - y$$

$$\frac{\partial J}{\partial W} = \frac{\partial J}{\partial z} \bullet \frac{\partial z}{\partial W} = (\hat{y} - y)x$$

$$\frac{\partial J}{\partial b} = \frac{\partial J}{\partial z} \bullet \frac{\partial z}{\partial b} = \hat{y} - y$$

## Softmax

$$
\begin{aligned}
&\hat{y_j} = \frac{e^{z_j}}{\sum\limits^K_k e^{z_k}} \\
&L = -\sum\limits^M_i \sum\limits^K_k 1\{y^{(i)}=k\} ln\hat{y}^{(i)} \\
\end{aligned}
$$

对于单个样本，第j类求导：

$$
\begin{aligned}
&\frac{ \partial{L_i} }{ \partial{\hat{y_j}} } = \frac{1}{ \hat{y_j} } \\
&\frac{ \partial{\hat{y_j}} }{ \partial{z_j} } = \frac{ \partial }{ \partial{z_j} } \frac{ e^{z_j} }{ \sum\limits^K_k e^{z_k} } \\
&\qquad = \frac{ e^{z_j} . \sum\limits^K_k e^{z_k} - e^{z_j} . e^{z_j} }{ {(\sum\limits^K_k e^{z_k})}^2 } \\
&\qquad = \hat{y_j} . (1 - \hat{y_j}) \\
&\frac{ \partial{L_i} }{ \partial{z_j} } = 1 - \hat{y_j} \\
\end{aligned}
$$

## Softmax and Sigmoid

Sigmoid: $$\hat{y} = \frac{1}{1+e^{-z}}$$

Softmax: $$\hat{y_j} = \frac{e^{z_j}}{\sum e^{z_k}}$$

对于Softmax类别数量为2的情况，

$$\hat{y_1} = \frac{e^{z_1}}{e^{z_0} + e^{z_1}} = \frac{1}{e^{z_0-z_1} + 1}$$

所以，Sigmoid是Softmax类别数量为2的特殊情况，但是Softmax要比Sigmoid浪费2倍的参数空间

## logstic loss的形式

label是0和1时，$$L = -ylog\hat{y} -(1-y)log(1-\hat{y})$$

label是-1和1时，$$\hat{y} = \sigma(y_r), L = -log(\sigma(yy_r))$$，或者$$L = log(1+e^{-yy_r})$$

作为对比，hinge loss（label是-1和1）是$$L = max(1-y\hat{y}, 0)$$
