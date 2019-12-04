## BatchNorm 的坑

https://blog.csdn.net/qq_25737169/article/details/79616671

### mini-batch 实现

```python
data_size = 8
batch_size = 2

dataset = tf.data.Dataset.range(data_size).shuffle(1).batch(batch_size)

iterator = tf.data.Iterator.from_structure(tf.int64, tf.TensorShape([batch_size, ]))
sess.run(iterator.make_initializer(dataset))

for _ in range(data_size // batch_size):
    i = sess.run(iterator.get_next())
    print(i)

# Output:
# [0 1]
# [2 3]
# [4 5]
# [6 7]

# Shuffle的参数代表采样区buffer大小，1代表buffer大小为1，即不随机
```

### flops and params

```python
run_meta = tf.RunMetadata()

opts = tf.profiler.ProfileOptionBuilder.float_operation()    
flops = tf.profiler.profile(sess.graph, run_meta=run_meta, cmd='op', options=opts)

opts = tf.profiler.ProfileOptionBuilder.trainable_variables_parameter()    
params = tf.profiler.profile(sess.graph, run_meta=run_meta, cmd='op', options=opts)

flops.total_float_ops
params.total_parameters
```

## demo

### show cpu or gpu

```shell
import tensorflow as tf; sess = tf.Session(config=tf.ConfigProto(log_device_placement=True))
```

如果显示CPU的信息，就是CPU版本
