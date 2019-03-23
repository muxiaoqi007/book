
## 方式一：输出形成dot文件，然后使用graphviz的dot命令将dot文件转换为pdf

```python

from sklearn import tree
with open('iris.dot', 'w') as f:
    # 将模型model输出到给定的文件中
    f = tree.export_graphviz(model, out_file=f)
# 命令行执行dot命令： dot -Tpdf iris.dot -o iris.pdf

```

## 方式二：直接使用pydotplus插件生成pdf文件

```python
from sklearn import tree
import pydotplus 
dot_data = tree.export_graphviz(model, out_file=None) 
graph = pydotplus.graph_from_dot_data(dot_data) 
# graph.write_pdf("iris2.pdf") 
graph.write_png("0.png")
```


## 方式三：直接生成图片

```python

from sklearn import tree
from IPython.display import Image
import pydotplus
dot_data = tree.export_graphviz(model, out_file=None, 
                         feature_names=['sepal length', 'sepal width', 'petal length', 'petal width'],  
                         class_names=['Iris-setosa', 'Iris-versicolor', 'Iris-virginica'],  
                         filled=True, rounded=True,  
                         special_characters=True)  
graph = pydotplus.graph_from_dot_data(dot_data)  
Image(graph.create_png()) 
```




