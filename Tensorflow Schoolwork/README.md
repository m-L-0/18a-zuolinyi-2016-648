# TensorFlow Schoolwork

使用TensorFlow设计K近邻模型，并使用鸢尾花数据集训练、验证模型。

## 基本思想

给定一个训练数据集，对新的输入样本，在训练数据集中找到与该样本最邻近的K个实例， 这K个实例的多数属于某个类，就把该输入样本分类到这个类中。

## 任务实现

1.将数据集分为训练集和验证集（8：2）：

```python
#导入模型包
import tensorflow as tf
import numpy as np
import matplotlib.pyplot as plt
```

```python
#加载鸢尾花数据集
from sklearn.datasets import load_iris
iris = load_iris()
data = iris.data
target = iris.target
featrue_names = iris.feature_names
```

```python 
#划分数据集为训练集和验证集
from sklearn.model_selection import train_test_split
x_train, x_test, y_train, y_test = train_test_split(iris.data, iris.target, test_size = 0.2, random_state = 1)
```

2.设计模型和训练模型：

```python
#占位符
x = tf.placeholder(tf.float32) #训练集
y = tf.placeholder(tf.float32) #验证集
#计算输入样本和训练样本的距离
dist = tf.sqrt(tf.reduce_sum(tf.abs(tf.add(x, tf.negative(y))), 1))
```

```python
def train_knn(k): #传入超参数k
    with tf.Session() as sess:
        #测试集所有样本的预测类别
        pred = []
        for i in range(len(x_test)):
            #计算输入的测试样本与训练集的距离
            dists = sess.run(dist, feed_dict = {x : x_train, y : x_test[i]})
            #将距离按顺序排好，去其中前k个
            knn = np.argsort(dists)[ : k]
            #类别矩阵，计算各类别的样本数量
            labels = [0, 0, 0]
            for j in knn:
                if(y_train[j] == 0):
                    #若样本为第0类
                    labels[0] = labels[0] + 1
                elif(y_train[j] == 1):
                    #若样本为第1类
                    labels[1] = labels[1] + 1
                else:
                    #若样本为第2类
                    labels[2] = labels[2] + 1
            #返回类别矩阵中最大值的索引，即为该样本的预测类别
            max_labels = np.argmax(labels)
            #添加预测类别
            pred.append(max_labels)
        return pred
```

3.验证模型：

```python
def test_knn():
    #不同k值的正确率
    k_test = []
    # k取值从0到10
    k_range = range(0, 10)
    for i in k_range:
        # k值为i时的预测类别
        i_pred = train_knn(i)
        y_true = y_test
        #计算正确率
        acc = np.sum(np.equal(i_pred, y_true)) / len(y_test)
        k_test.append([i, acc])
    #输出最优的k值
    for j in k_range:
        acc_max = np.max(k_test[:2])
        if(k_test[j][1] == acc_max):
            print([j, k_test[j][1]])
```

```python
test_knn()
```

```
[1, 1.0]
[3, 1.0]
[4, 1.0]
```