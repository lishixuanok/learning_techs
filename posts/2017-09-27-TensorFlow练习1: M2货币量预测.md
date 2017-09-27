## 概要

|  算法  |  功能  |  
|  :----:  |  :----:  | 
| RNN-LSTM | 预测未来一年数据走向 | 


1. 数据源
2. 计算过程
3. 结果

## 1. 数据源
[国家统计局](http://www.stats.gov.cn/tjsj/)，用csv格式导出

样例
```csv
2017年6月,1631282.53
2017年5月,1601360.42
...
2005年2月,259357.29
2005年1月,257708.47
```

## 2. 计算过程

* 预处理

```python
import numpy as np
import pandas as pd
from datetime import datetime
import matplotlib.pyplot as plt

def _parser(date_string):
    return datetime.strptime(date_string, '%Y年%m月')


# pre process data
df = pd.read_csv('M2供应量.csv', delimiter=',',
                 header=None, dtype={1: np.float}, parse_dates=[0],
                 date_parser=_parser)

# plot
sorted_df = df.sort_index(axis=0, ascending=False)
data = sorted_df[1]
normalized_data = (data - np.mean(data)) / np.std(data)
plt.subplot(1, 1, 1)
plt.plot(sorted_df[0], normalized_data)
plt.xlabel(u'time (month)')
plt.ylabel(u'M2 supply')
plt.show()

```

* 计算

```python
import tensorflow as tf
# normalize
seq_size = 3
train_x, train_y = [], []
for i in range(len(normalized_data) - seq_size - 1):
    train_x.append(np.expand_dims(normalized_data[i: i + seq_size], axis=1).tolist())
    train_y.append(normalized_data[i + 1: i + seq_size + 1].tolist())

input_dim = 1
X = tf.placeholder(tf.float32, [None, seq_size, input_dim])
Y = tf.placeholder(tf.float32, [None, seq_size])

# regression
def ass_rnn(hidden_layer_size=6):
    W = tf.Variable(tf.random_normal([hidden_layer_size, 1]), name='W')
    b = tf.Variable(tf.random_normal([1]), name='b')
    cell = tf.nn.rnn_cell.BasicLSTMCell(hidden_layer_size)
    outputs, states = tf.nn.dynamic_rnn(cell, X, dtype=tf.float32)
    W_repeated = tf.tile(tf.expand_dims(W, 0), [tf.shape(X)[0], 1, 1])
    out = tf.matmul(outputs, W_repeated) + b
    out = tf.squeeze(out)
    return out


def train_rnn():
    learning_rate = 0.0005
    out = ass_rnn()

    # optimizer
    loss = tf.reduce_mean(tf.square(out - Y))
    train_op = tf.train.AdamOptimizer(learning_rate=learning_rate).minimize(loss)

    saver = tf.train.Saver(tf.global_variables())
    with tf.Session() as sess:
        # tf.get_variable_scope().reuse_variables()
        sess.run(tf.global_variables_initializer())
        for step in range(20000):
            _, loss_ = sess.run([train_op, loss], feed_dict={X: train_x, Y: train_y})
            if step % 10 == 0:
                # 用测试数据评估loss
                print(step, loss_)
        print("保存模型: ", saver.save(sess, 'ass.model'))

train_rnn()
```

* 预测
```python
def prediction():
    out = ass_rnn()

    saver = tf.train.Saver(tf.global_variables())
    with tf.Session() as sess:
        # tf.get_variable_scope().reuse_variables()
        saver.restore(sess, './ass.model')

        prev_seq = train_x[-1]
        predict = []
        for i in range(12):
            next_seq = sess.run(out, feed_dict={X: [prev_seq]})
            predict.append(next_seq[-1])
            prev_seq = np.vstack((prev_seq[1:], next_seq[-1]))

        plt.subplot(1, 1, 1)
        plt.plot(sorted_df[0], normalized_data, color='b')
        ix = pd.DatetimeIndex(start=datetime(2017, 6, 1), end=datetime(2018, 6, 1), freq='M')
        plt.plot(ix, predict, color='r')
        plt.xlabel(u'time (month)')
        plt.ylabel(u'M2 supply')
        plt.show()

prediction()
```

### 3. 结果
绘图
