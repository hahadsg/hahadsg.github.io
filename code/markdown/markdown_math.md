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

