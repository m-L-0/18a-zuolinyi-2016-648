1.导入相关库

```python
import scipy.io as sio
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import spectral
```



2.获取本地数据，将mat数据读取出来

```python
datafile = 'data2_train.mat'
file2 = sio.loadmat(datafile)
data2 = file2['data2_train']
print(data2)
type(data2)
data2.shape
datafile = 'data3_train.mat'
file3 = sio.loadmat(datafile)
data3 = file3['data3_train']
print(data3)
data3.shape
datafile = 'data5_train.mat'
file5 = sio.loadmat(datafile)
data5 = file5['data5_train']
print(data5)
data5.shape
datafile = 'data6_train.mat'
file6 = sio.loadmat(datafile)
data6 = file6['data6_train']
print(data6)
data5.shape
datafile = 'data8_train.mat'
file8 = sio.loadmat(datafile)
data8 = file8['data8_train']
print(data8)
data8.shape
datafile = 'data10_train.mat'
file10 = sio.loadmat(datafile)
data10 = file10['data10_train']
print(data10)
data10.shape
datafile = 'data11_train.mat'
file11 = sio.loadmat(datafile)
data11 = file11['data11_train']
print(data11)
data11.shape
datafile = 'data12_train.mat'
file12 = sio.loadmat(datafile)
data12 = file12['data12_train']
print(data12)
data12.shape
datafile = 'data14_train.mat'
file14 = sio.loadmat(datafile)
data14 = file14['data14_train']
print(data14)
data14.shape
datafile = 'data_test_final'
test_file = sio.loadmat(datafile)
test_data = test_file['data_test_final']
print(test_data)
test_data.shape
```



3.数据集处理

```python
numbers = [1071, 622, 362, 362, 358, 729, 1841, 445, 949]
labels = [2, 3, 5, 6, 8, 10, 11, 12, 14]
data_i = [data2, data3, data5, data6, data8, data10, data11, data12, data14]
all_number = 1071 + 622 + 362 + 362 + 358 + 729 + 1841 + 445 + 949
print(all_number)
```

```python
data = []
data_y = []
for i in range(9):
    for j in range(numbers[i]):
        data.append(data_i[i][j])

for i in range(9):
    for j in range(numbers[i]):
        data_y.append(labels[i])
        
data = np.array(data)
data_y = np.array(data_y)
data.shape
print(data)
```

4.划分数据集和训练集（3：7）

```python
from sklearn.model_selection import train_test_split
x_train, x_test, y_train, y_test = train_test_split(data, data_y, test_size = 0.3, random_state = 3)
```

5.训练模型

```python
from sklearn import svm
svc = svm.SVC(C = 1, gamma = 1)
svc.fit(x_train, y_train)
score = svc.score(x_train, y_train)
print(score)
```

6.使用网格搜索法调参，优化模型

```python
from sklearn.svm import SVC
best_score = 0
for gamma in [0.001,0.01,0.1,1,10,100]:
    for C in [0.001,0.01,0.1,1,10,100]:
        svc = svm.SVC(kernel = 'linear', C = C, gamma = gamma)
        #对于每种参数可能的组合，进行一次训练；
        svc.fit(x_train,y_train)
        score = svc.score(x_test,y_test)
        if score > best_score:
            #找到表现最好的参数
            best_score = score
            best_parameters = {'gamma':gamma,'C':C}

print("Best score:{:.2f}".format(best_score))
print("Best parameters:{}".format(best_parameters))
```

7.对测试集进行预测

```python
result = svc.predict(test_data)
result = np.array(result)
data_result = pd.DataFrame(result)
data_result.to_csv('result.csv')
```

