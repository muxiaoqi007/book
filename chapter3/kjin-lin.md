# K 近邻

k近邻是**监督学习**，是基于某种距离试题找出训练集中与其最靠近的k个训练样本，然后基于这k个邻居的信息来进行预测。通常，

- 分类任务：投票法
- 回归任务：平均法

k近邻不具有显式的学习过程，它是**直接预测**，

## 一般流程

1. 收集数据：可以使用任何方法。
2. 准备数据：距离计算所需要的数值，最好是结构化的数据格式。
3. 分析数据：可以使用任何方法。
4. 训练算法：此步骤不适用于k近邻算法。
5. 测试算法：计算错误率。
6. 使用算法：首先需要输入样本数据和结构化的输出结果，然后运行k近邻算法判定输入数据分别属于哪个分类，最后应用对计算出的分类执行后续的处理。

## 三要素

- k值选择
- 距离度量
- 分类决策规则

### k值选择

当k=1时，称为最近邻算法

1. 若k值较小，相当于用较小的邻域中的训练实例进行预测，学习的近似误差减少
   - 优点：只有与输入实例较近的训练实例才会对预测起作用

   - 缺点：学习的估计误差会增大，预测结果会对近邻的实例点非常敏感。若近邻的训练实例点刚好是噪声，则预测会出错。即k值的减小意味着模型整体变复杂，易发生过拟合

2. 若k值较大，则相当于用较大的领域中的训练实例进行预测
   - 优点：减少学习估计误差
   - 缺点：近似误差增大，输入实例较远的训练实例也会对预测起作用，即意味着**模型变得简单**。
所以通常采用交叉验证法来选取最优的k,比较不同k时的平均优酷大率，选择误差率最小的那个k值。

### 距离度量
要求**所有特征**都可以做**可比较的量化**。即若特征中存在非数值类型，必须将其量化为数值。K近邻一般为欧氏距离（只适用于连续变量） 。

### 分类决策规划

通常采用多数表决，也可基于距离远近进行加权投票。

多数表决规则等价于经验风险最小化，误分类率就是训练数据的经验风险。

**优点**

- 精度高
- 对异常值不敏感
- 无数据输入假定

**缺点**
- 计算复杂度高
- 空间复杂度高

**适用类型**
- 数值型
- 标称型



## python实现

### 创建数据集

```python
def createDataSet():
    group = np.array([[1.0,1.1],[1.0,1.0],[0,0],[0,0.1]])
    labels = ['A','A','B','B']
    return group, labels
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
    dataSetSize = dataSet.shape[0]
    # 计算距离 
    diffMat = np.tile(inx, (dataSetSize, 1)) - dataSet
    sqDiffMat = diffMat ** 2
    sqDistances = sqDiffMat.sum(axis=1)
    distances = sqDistances ** 0.5
    
    sortedDistIndicies = distances.argsort()
    classCount = {}
    # 选择距离最小的K个点
    for i in range(k):
        voteIlabel = labels[sortedDistIndicies[i]]
        classCount[voteIlabel] = classCount.get(voteIlabel,0) + 1
    sortedClassCount = sorted(classCount.items(),
                              key = operator.itemgetter(1), reverse=True)
    return sortedClassCount[0][0]
```

