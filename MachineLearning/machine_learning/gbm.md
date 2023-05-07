## GBM对比

参考：https://www.kaggle.com/nschneider/gbm-vs-xgboost-vs-lightgbm

## Tree Traverse

### level-wise

![](./assets/gbm/level-wise.png)

逐层的生长（类似BFS），每次选取最优分割

### leaf-wise(best-first)

![](./assets/gbm/leaf-wise.png)

选择对减少loss贡献最大的节点生长（类似DFS）

## Decision Tree

gini and entropy: https://www.garysieling.com/blog/sklearn-gini-vs-entropy-criteria
