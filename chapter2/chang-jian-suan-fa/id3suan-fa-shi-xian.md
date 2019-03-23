ID3算法实现

- 1 先创建数据集,

```python
def createDataSet():
    dataSet = [[1, 1, 'yes'],
               [1, 1, 'yes'],
               [1, 0, 'no'],
               [0, 1, 'no'],
               [0, 1, 'no']]
    labels = ['no surfacing','flippers']
    return dataSet, labels
```

- 2 划分数据集

 ```python
  def splitDataSet(dataSet, axis, value):
    """
    dataSet: 待划分的数据集
    axis:划分数据集的特征
    value:需要返回的特征的值 
    """
    retDataSet = []
    for featVec in dataSet:
        if featVec[axis] == value:
            reducedFeatVec = featVec[:axis]    
            reducedFeatVec.extend(featVec[axis+1:])
            retDataSet.append(reducedFeatVec)
    return retDataSet
 ```

  测试

```python
->splitDataSet(myDat, 0, 1)
->[[1, 'maybe'], [1, 'yes'], [0, 'no']]
```