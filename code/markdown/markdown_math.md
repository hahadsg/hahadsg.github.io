---
title: markdown math
---

# 基本公式语法

## 公式对齐

使用语法：（`\\`是换行的意思，`&`是对齐的位置）

```markdown
$$
\begin{align}
a &= 1 * 2 + 3 \\
  &= 3 + 3 \\
  &= 6 \\
\end{align}
$$
```

效果如下：

$$
\begin{align}
a &= 1 * 2 + 3 \\
  &= 3 + 3 \\
  &= 6 \\
\end{align}
$$

## 符号

### 四则运算

乘法：`\times`，如$$a \times b$$

### 逻辑运算

| code | symbols |
| ---- | ------- |
| `\gt` | $$\gt$$ |
| `\lt` | $$\lt$$ |
| `\geq` | $$\geq$$ |
| `\leq` | $$\leq$$ |
| `\approx` | $$\approx$$ |

### 集合运算

属于：`\in`，如$$x \in y$$

### 集合符号

实数集合：`\mathbb{N}`，如$$\mathbb{R}$$

### greek letters

| code | symbols |
| ---- | ------- |
| `\alpha` | $$\alpha$$ |
| `\beta` | $$\beta$$ |
| `\gamma` | $$\gamma$$ |
| `\delta` | $$\delta$$ |
| `\epsilon` | $$\epsilon$$ |
| `\varepsilon` | $$\varepsilon$$ |
| `\zeta` | $$\zeta$$ |
| `\eta` | $$\eta$$ |
| `\Gamma` | $$\Gamma$$ |
| `\Delta` | $$\Delta$$ |
| `\Theta` | $$\Theta$$ |
| `\theta` | $$\theta$$ |
| `\vartheta` | $$\vartheta$$ |
| `\iota` | $$\iota$$ |
| `\kappa` | $$\kappa$$ |
| `\lambda` | $$\lambda$$ |
| `\mu` | $$\mu$$ |
| `\nu` | $$\nu$$ |
| `\xi` | $$\xi$$ |
| `\Lambda` | $$\Lambda$$ |
| `\Xi` | $$\Xi$$ |
| `\Pi` | $$\Pi$$ |
| `\pi` | $$\pi$$ |
| `\varpi` | $$\varpi$$ |
| `\rho` | $$\rho$$ |
| `\varrho` | $$\varrho$$ |
| `\sigma` | $$\sigma$$ |
| `\varsigma` | $$\varsigma$$ |
| `\tau` | $$\tau$$ |
| `\Sigma` | $$\Sigma$$ |
| `\Upsilon` | $$\Upsilon$$ |
| `\Phi` | $$\Phi$$ |
| `\upsilon` | $$\upsilon$$ |
| `\phi` | $$\phi$$ |
| `\varphi` | $$\varphi$$ |
| `\chi` | $$\chi$$ |
| `\psi` | $$\psi$$ |
| `\omega` | $$\omega$$ |
| `\Psi` | $$\Psi$$ |
| `\Omega` | $$\Omega$$ |

### 数学常用符号

微分算符：`\nabla`，$$\nabla$$

逐元素乘（Hadamard product）：`\circ`，$$\circ$$

求最小值：`\mathop{\arg\min}_{\theta} f(\theta)`，$$\mathop{\arg\min}_{\theta} f(\theta)$$

内积：`\langle x, y \rangle`，$$\langle x, y \rangle$$

### hat

| code | symbols |
| ---- | ------- |
| `\hat{x}` | $$\hat{x}$$ |
| `\tilde{x}` | $$\tilde{x}$$ |
| `\bar{x}` | $$\bar{x}$$ |
| `\vec{x}` | $$\vec{x}$$ |
| `\overrightarrow{x}` | $$\overrightarrow{x}$$ |
| `\overleftarrow{x}` | $$\overleftarrow{x}$$ |

### 数学公式大括号

```markdown
$$
f(s) = 
\begin{cases}
s &if\ s \gt 0 \\
\alpha s &if\ s \leq 0 \\
\end{cases}
$$
```

$$
f(s) = 
\begin{cases}
s &if\ s \gt 0 \\
\alpha s &if\ s \leq 0 \\
\end{cases}
$$

### 空格

| code | symbols |
| ---- | ------- |
| `a\ b` | $$a\ b$$ |
| `a\quad b` | $$a\quad b$$ |
| `a\qquad b`| $$a\qquad b$$ |

# 更好的写公式

## 竖线

比如条件概率，尽量使用`p(x\mid \theta)`，而不是`p(x|\theta)`

`p(x|\theta)`的效果如下：（另外，如果使用该方法在github page中可能会出现bug，它会认为竖线是table）

$$p(x|\theta)$$

`p(x\mid \theta)`的效果如下：

$$p(x\mid \theta)$$

## 点乘

比如矩阵相乘，尽量使用`\cdot`，而不是`.`

`.`的效果如下：

$$A . B$$

`\cdot`的效果如下：

$$A \cdot B$$

