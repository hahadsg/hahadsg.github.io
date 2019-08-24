过拟合的表象就是在训练集上取得不错的性能，而在验证集上性能很差，也称作出现高方差问题

那么，引起高方差的原因主要是，模型太复杂而数据太少

针对模型复杂：那么在线性模型上，一般调高惩罚项系数（L1、L2）；svm也调整惩罚项系数C；树模型调整max_depth、列采样，提升树可以设置early_stopping；神经网络可以设置惩罚项（L1、L2）、dropout、early_stopping、较少层或者节点数、batchnormalization也有一定的效果（不过主要还是提升训练速度）

针对数据太少：增加数据、或者数据增广

同时，需要注意一下train/val是否分割的不合理
如果数据少的话，CV也会有不错的效果

另外，我不认为减少特征是个好选择（好不容易找的特征。。），至少不能为了解决过拟合而减少特征（为了速度时可以考虑），还是在负责度下功夫比较好


* 防止过拟合文章参考

http://dataunion.org/21691.html


