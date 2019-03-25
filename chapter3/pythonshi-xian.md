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
