## ID3算法

每次迭代选择信息增益最大的特征属性作为划分属性
$$
Ent(D) = -\sum_{k=1}^{|y|}p_k\log_{2}{p_k} \\
Gain(D,a) = Ent(D)-\sum_{v=1}^{V}\frac{|D^v|}{D}Ent(D^v)
$$
输入：训练数据集D，特征集A，阈值ε；

输出：决策树T.

**Step1：**若D中所有实例属于同一类$$C_k​$$，则T为单结点树，并将类![img](https://shuwoom.com/wp-content/uploads/2018/10/9a2d62e98799d878be2e3d6133772b3c.png)作为该节点的类标记，返回T；

**Step2：**若A=Ø，则T为单结点树，并将D中实例数最大的类![img](https://shuwoom.com/wp-content/uploads/2018/10/9a2d62e98799d878be2e3d6133772b3c.png)作为该节点的类标记，返回T；

**Step3：**否则，2.1.1（3）计算A中个特征对D的信息增益，选择信息增益最大的特征![img](https://shuwoom.com/wp-content/uploads/2018/10/2ec429afd34217f1c3677724fa8fb15b.png)；

**Step4：**如果![img](https://shuwoom.com/wp-content/uploads/2018/10/07879f0e470512329a1ca3eff7be1cb0.png)的信息增益小于阈值ε，则T为单节点树，并将D中实例数最大的类![img](https://shuwoom.com/wp-content/uploads/2018/10/9a2d62e98799d878be2e3d6133772b3c.png)作为该节点的类标记，返回T

**Step5：**否则，对![img](https://shuwoom.com/wp-content/uploads/2018/10/07879f0e470512329a1ca3eff7be1cb0.png)的每一种可能值![img](https://shuwoom.com/wp-content/uploads/2018/10/676a8c839495baa86c594cbd06039139.png)，依![img](https://shuwoom.com/wp-content/uploads/2018/10/ba8c5b3f3d3f616ee756237cef210963.png)将D分割为若干非空子集![img](https://shuwoom.com/wp-content/uploads/2018/10/8c90311426a3327e30c3664e1d2e9ef8.png)，将![img](https://shuwoom.com/wp-content/uploads/2018/10/8c90311426a3327e30c3664e1d2e9ef8.png)中实例数最大的类作为标记，构建子结点，由结点及其子树构成树T，返回T；

**Step6：**对第i个子节点，以![img](https://shuwoom.com/wp-content/uploads/2018/10/8c90311426a3327e30c3664e1d2e9ef8.png)为训练集，以![img](https://shuwoom.com/wp-content/uploads/2018/10/6176289f227123f374bc1c33f6a0cb6b.png)为特征集合，递归调用**Step1~step5**，得到子树![img](https://shuwoom.com/wp-content/uploads/2018/10/6109eab53b1abe5b2eb330cf3427b86a.png)，返回![img](https://shuwoom.com/wp-content/uploads/2018/10/6109eab53b1abe5b2eb330cf3427b86a.png)；

**优点**：

- 决策结构造速度快，实现简单

**缺点**:

- 计算依赖于特征数目较多的特征，而属性值最多的属性差不一定最优
- 不是递增算法
- 是单变量决策树，不考虑其他属性之前的关系
- 抗噪性差
- 只适合小规模数据集，需要将数据放到内存中



## C4.5
基于ID3,进行了优化，使用信息增益率，在树的构造过程中会进行**剪枝**操作进行优化，能够自动完成对连续属性的离散化处理，
$$
Gain\_ratio(D,a) = \frac{Gain(D,a)}{IV(a)},
\\其中,IV(a)=-\sum_{v=1}^{V}\frac{|D^v|}{|D|}\log_2\frac{|D^v|}{|D|}
$$
**优点**：

- 产生的规则易于理解

- 准确率较高

- 实现简单

**缺点**：

- 对数据集需要进行多次顺序扫描和排序，效率低
- 只适合小规模数据集，需要将数据放到内存中

## CART算法

使用GINI增益作为划分选择的标准，可用于分类和回归，**构建是二叉树**
$$
\begin{align}
Gini(D)&=\sum_{k=1}^{|y|}\sum_{k'\neq{k}}p_kp_{k'}\\
&=1-\sum_{k=1}^{|y|}p_k^2
\end{align}
$$

$$
Gini\_index(D,a)=\sum_{v=1}^{V}\frac{|D^v|}{|D|}Gini(D^v)
$$

## 总结

| 算法 | 模型       | 树结构 | 特征选择 | 连续值处理 | 缺失值处理 | 剪枝 | 特征属性多次使用 |
| ---- | ---------- | ------ | -------- | ---------- | ---------- | ---- | ---------------- |
| ID3  | 分类       | 多叉树 | 信息增益 | 不支持     | 不支持     |  不支持    |    不支持              |
| C4.5 | 分类       |    多叉树    |   信息增益率       |     支持       | 支持 |    支持  |    不支持              |
| CART | 分类、回归 |    二叉树    | 基尼系数、均方差         | 支持           |   支持         |支持      |   支持               |

