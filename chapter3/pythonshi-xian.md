## python实现

### 创建数据集

```python
def createDataSet():
    group = np.array([[1.0,1.1],[1.0,1.0],[0,0],[0,0.1]])
    labels = ['A','A','B','B']
    return group, labels
```

```python
- group, labels = createDataSet()
- group
- array([[1. , 1.1],
       [1. , 1. ],
       [0. , 0. ],
       [0. , 0.1]])
```



```python
def classify0(inx, dataSet, labels, k):
    '''
    函数功能：   kNN分类
    Input:      inX: 测试集 (1xN)
                dataSet: 已知数据的特征(NxM)
                labels: 已知数据的标签或类别(1xM vector)
                k: k近邻算法中的k
    Output:     测试样本最可能所属的标签
    '''
    dataSetSize = dataSet.shape[0] # 数据行数
    # 计算距离 
    diffMat = np.tile(inx, (dataSetSize, 1)) - dataSet 
    # 复制inx为和数据集同样的行数，然后求差
    sqDiffMat = diffMat ** 2
    sqDistances = sqDiffMat.sum(axis=1) # 按行求和
    distances = sqDistances ** 0.5 
    
    sortedDistIndicies = distances.argsort() # 对distances的元素从小到大排列，取其index
    classCount = {}
    # 选择距离最小的K个点
    for i in range(k):
        voteIlabel = labels[sortedDistIndicies[i]]
        classCount[voteIlabel] = classCount.get(voteIlabel,0) + 1
    sortedClassCount = sorted(classCount.items(),
                              key = operator.itemgetter(1), reverse=True)
    return sortedClassCount[0][0]
```

可以修改为如下：


```python
def classify1(inx, dataSet, labels, k):
    '''
    函数功能：   kNN分类
    Input:      inX: 测试集 (1xN)
                dataSet: 已知数据的特征(NxM)
                labels: 已知数据的标签或类别(1xM vector)
                k: k近邻算法中的k
    Output:     测试样本最可能所属的标签
    '''
    # 计算距离 
    distances = [np.sqrt(np.sum((x_train - inx)**2)) for x_train in dataSet]
    
    sortedDistIndicies = np.argsort(distances)
    classCount = {}
    # 选择距离最小的K个点
    topK_y = [labels[idx] for idx in sortedDistIndicies[:k]]
    from collections import Counter
    votes = Counter(topK_y)
    return votes.most_common(1)[0][0]

```

## 整理到类里


```python
import numpy as np
from math import sqrt
from collections import Counter


class KNNClassifier:

    def __init__(self, k):
        """初始化kNN分类器"""
        assert k >= 1, "k must be valid"
        self.k = k
        self._X_train = None
        self._y_train = None

    def fit(self, X_train, y_train):
        """根据训练数据集X_train和y_train训练kNN分类器"""
        assert X_train.shape[0] == y_train.shape[0], \
            "the size of X_train must be equal to the size of y_train"
        assert self.k <= X_train.shape[0], \
            "the size of X_train must be at least k."

        self._X_train = X_train
        self._y_train = y_train
        return self

    def predict(self, X_predict):
        """给定待预测数据集X_predict，返回表示X_predict的结果向量"""
        assert self._X_train is not None and self._y_train is not None, \
                "must fit before predict!"
        assert X_predict.shape[1] == self._X_train.shape[1], \
                "the feature number of X_predict must be equal to X_train"

        y_predict = [self._predict(x) for x in X_predict]
        return np.array(y_predict)

    def _predict(self, x):
        """给定单个待预测数据x，返回x的预测结果值"""
        assert x.shape[0] == self._X_train.shape[1], \
            "the feature number of x must be equal to X_train"

        distances = [sqrt(np.sum((x_train - x) ** 2))
                     for x_train in self._X_train]
        nearest = np.argsort(distances)

        topK_y = [self._y_train[i] for i in nearest[:self.k]]
        votes = Counter(topK_y)

        return votes.most_common(1)[0][0]

    def __repr__(self):
        return "KNN(k=%d)" % self.k
```


