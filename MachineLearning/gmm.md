---
title: GMM
---

## GMM(Gaussian Mixtrue Model)

高斯混合模型是指具有如下形式的概率分布模型：

$$P(y\rvert \theta)=\sum\limits^K_{k=1}\alpha_k f(y\rvert \theta_k)$$

其中，$$\alpha_k$$是系数，$$\sum\limits^K_{k=1}\alpha_k=1$$；$$f(y\rvert \theta_k)$$是高斯分布密度，$$\theta_k=(\mu_k, \Sigma_k)$$，

$$f(y\rvert \theta_k) = \frac{1}{(2\pi)^{d/2} \rvert \Sigma_k\rvert ^{1/2}} exp[-\frac{1}{2} (y-\mu_k)^T \Sigma^{-1}_k (y-\mu_k)]$$


应用：假设样本数据服从k个高斯混合模型，求这k个高斯分布的参数

记观测数据$$Y={y_1,y_2,...}$$，对应隐变量$$Z={z_1,z_2,...}$$

$$P(y_j,z_j \in \gamma_k \rvert  \theta) = \alpha_k f(y_j\rvert \theta_k)$$

$$P(y_j\rvert \theta)=\sum\limits^K_{k=1}\alpha_k f(y_j\rvert \theta_k)$$

$$P(z_j \in \gamma_k \rvert  y_j, \theta) = \frac{\alpha_k f(y_j\rvert \theta_k)}{\sum\limits^K_{k=1}\alpha_k f(y_j\rvert \theta_k)}$$

#### E-Step

构造Q函数，

$$\begin{equation}
\begin{aligned}
Q(\theta,\theta^{(i)})
&= E_Z[logP(Y,Z\rvert \theta)\rvert Y,\theta^{(i)}]\\
&= \sum\limits_Z logP(Y,Z\rvert \theta) P(Z\rvert Y,\theta^{(i)})\\
\end{aligned}
\end{equation}$$

#### M-Step

对各参数优化，

$$\alpha^{(i+1)}_k = \frac{\sum\limits^N_{j=1} P(z_j\in\gamma_k \rvert  y_j,\theta^{(i)})}{N}$$

$$\mu^{(i+1)}_k = \frac{\sum\limits^N_{j=1} y_j P(z_j\in\gamma_k \rvert  y_j,\theta^{(i)})}{\sum\limits^N_{j=1} P(z_j\in\gamma_k \rvert  y_j,\theta^{(i)})}$$

$$\Sigma^{(i+1)}_k = \frac{\sum\limits^N_{j=1} (y_j-\mu_k)^2 P(z_j\in\gamma_k \rvert  y_j,\theta^{(i)})}{\sum\limits^N_{j=1} P(z_j\in\gamma_k \rvert  y_j,\theta^{(i)})}$$

