## Linear Regression

损失函数：
$$ J(\theta) = \frac{1}{2}\sum(Wx+b-y)^2 $$

## Ridge

损失函数增加了L2惩罚项：
$$ J(\theta) = \frac{1}{2}\sum(Wx+b-y)^2 + \lambda ||W||_2 $$

## Lasso

损失函数增加了L1惩罚项：
$$ J(\theta) = \frac{1}{2}\sum(Wx+b-y)^2 + \lambda ||W||_1 $$

## ElasticNet

损失函数：
$$ J(\theta) = \frac{1}{2}\sum(Wx+b-y)^2 + \alpha\lambda ||W||_1 + \frac{1}{2}\alpha(1-\lambda)||W||_2 $$