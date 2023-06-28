---
title: 用tensorflow实现简单的猫猫识别
date: 2022-05-08 16:50:24
categories: 
- python
tags: 
- 深度学习
- tensorflow
---



# 简单神经网络实现猫猫识别（不含卷积层）
<!--more-->
**tips:**
1. 输入样本的尺寸可以在传入神经网络第一层的参数中，不需要额外添加输入层。在传入输入尺寸时不需要传入batchsize
2. 当标签为01标签时，metric的精度应该选择tf.keras.metrics.BinaryAccuracy()，使用tf.keras,Accuracy()时精度始终为0。
3. 样本的标签应该以列向量的形式传入model.fit函数中，model.evaluate同理。



完整代码：
```python
import tensorflow as tf
from lr_utils import load_dataset


train_set_x_orig , train_set_y , test_set_x_orig , test_set_y , classes = load_dataset()
print(train_set_x_orig.shape, test_set_x_orig.shape, train_set_y.shape, test_set_y.shape) # 输出原始数据的维度
train_set_x = train_set_x_orig / 255
test_set_x = test_set_x_orig / 255
model = tf.keras.models.Sequential([
    tf.keras.layers.Flatten(input_shape=(64, 64, 3)), # input_shape中无需传入batchsize
    tf.keras.layers.Dense(10, activation='relu'),
    tf.keras.layers.Dense(5, activation='relu'),
    tf.keras.layers.Dense(1, activation='sigmoid'),
])

print(model.summary())

model.compile(
  optimizer='Adam',
  loss=tf.keras.losses.BinaryCrossentropy(),
  metrics=[tf.keras.metrics.BinaryAccuracy(),
           tf.keras.metrics.FalsePositives(),
           tf.keras.metrics.FalseNegatives(),
])
model.fit(train_set_x, train_set_y.T, epochs=50, batch_size=train_set_x.shape[0]) # 标签需要是列向量
model.evaluate(test_set_x, test_set_y.T, batch_size=train_set_x.shape[0])
```