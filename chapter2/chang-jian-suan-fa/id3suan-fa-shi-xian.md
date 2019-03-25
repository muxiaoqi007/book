# ID3算法实现

## 方法1

### 先创建数据集

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

### 划分数据集

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

### 选择最好的划分

```python
def chooseBestFeatureToSplit(dataSet):
        numFeatures = len(dataSet[0]) - 1     # 特征个数 
        baseEntropy = calcShannonEnt(dataSet)
        bestInfoGain = 0.0; bestFeature = -1
        for i in range(numFeatures):        
                #（以下两行）创建唯一的分类标签列表 
                featList = [example[i] for example in dataSet]
                print('当前属性特征值列表：',featList)
                uniqueVals = set(featList) 
                print('当前属性特征值去重后：',uniqueVals)
                newEntropy = 0.0
                #（以下五行）计算每种划分方式的信息熵  
                for value in uniqueVals:
                        subDataSet = splitDataSet(dataSet, i, value)
                        prob = len(subDataSet)/float(len(dataSet))
                        newEntropy += prob * calcShannonEnt(subDataSet)     

                infoGain = baseEntropy - newEntropy   

                if (infoGain > bestInfoGain):   
                #计算最好的信息增益    
                        bestInfoGain = infoGain         
                        bestFeature = i
            
        return bestFeature

def calcShannonEnt(dataSet):
        numEntries = len(dataSet)
        labelCounts = {}
        for featVec in dataSet: #the the number of unique elements and their occurance
                currentLabel = featVec[-1]
                if currentLabel not in labelCounts.keys(): labelCounts[currentLabel] = 0
                labelCounts[currentLabel] += 1
        shannonEnt = 0.0
        print('统计结果：',labelCounts)
        for key in labelCounts:
                prob = float(labelCounts[key])/numEntries
                shannonEnt -= prob * math.log(prob,2) #log base 2
        return shannonEnt
```

### 构建决策树

```python
def majortyCnt(classList):        
        classCount = {}
        for vote in classList:
                if vote not in classCount.keys():
                        classCount[vote] = 0
                classCount[vote] +=1
        sortedClassCount = sorted(classCount.iteritems(), key=operator.itemgetter(1), reverse=True)
        return sortedClassCount

def createTree(dataSet,labels):
        classList = [example[-1] for example in dataSet] # 类别
        # 类别完全相同则停止继续划分
        if classList.count(classList[0]) == len(classList): 
                return classList[0]
        # 遍历完所有特征时返回出现次数最多的
        if len(dataSet[0]) == 1: 
                return majorityCnt(classList)
        bestFeat = chooseBestFeatureToSplit(dataSet)
        bestFeatLabel = labels[bestFeat]
        myTree = {bestFeatLabel:{}}
        # 得到列表包含的所有属性值
        del(labels[bestFeat])
        featValues = [example[bestFeat] for example in dataSet]
        uniqueVals = set(featValues)
        for value in uniqueVals:
                subLabels = labels[:]       
                myTree[bestFeatLabel][value] = createTree(splitDataSet
                                   (dataSet, bestFeat, value),subLabels)
        return myTree
```

## 方法2

1. 划分数据

```python
def split(X, y, d, value):
    index_a = (X[:,d] <= value)
    index_b = (X[:,d] > value)
    return X[index_a], X[index_b], y[index_a], y[index_b]
```
2.计算信息熵


```python
from collections import Counter
from math import log

def entropy(y):
    """计算信息熵"""
    counter = Counter(y)
    Ent = 0.0
    for num in counter.values():
        p = num / len(y)
        Ent += -p * log(p)
    return Ent
```

3.选择最优


```python
def try_split(X, y):
    
    best_entropy = float('inf')
    best_d, best_v = -1, -1
    for d in range(X.shape[1]):
        sorted_index = np.argsort(X[:,d])
        for i in range(1, len(X)):
            if X[sorted_index[i], d] != X[sorted_index[i-1], d]:
                v = (X[sorted_index[i], d] + X[sorted_index[i-1], d])/2
                X_l, X_r, y_l, y_r = split(X, y, d, v)
                p_l, p_r = len(X_l) / len(X), len(X_r) / len(X)
                e = p_l * entropy(y_l) + p_r * entropy(y_r)
                if e < best_entropy:
                    best_entropy, best_d, best_v = e, d, v
                
    return best_entropy, best_d, best_v
```




































