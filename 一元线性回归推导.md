$$
f(\boldsymbol{x})=w_{1} x_{1}+w_{2} x_{2}+\ldots+w_{d} x_{d}+b
$$

## 一般向量形式
$$
f(\boldsymbol{x})=\boldsymbol{w}^{\mathrm{T}} \boldsymbol{x}+b
$$
## 线性回归试图学得
$$
f\left(x_{i}\right)=w x_{i}+b,使得 f\left(x_{i}\right) \simeq y_{i}      
$$
即
$$
\begin{aligned}\left(w^{*}, b^{*}\right) &=\underset{(w, b)}{\arg \min } \sum_{i=1}^{m}\left(f\left(x_{i}\right)-y_{i}\right)^{2} \\ &=\underset{(w, b)}{\arg \min } \sum_{i=1}^{m}\left(y_{i}-w x_{i}-b\right)^{2} \end{aligned}
$$



## 二元函数判断凹凸性

设 $$f(x, y)​$$ 在区域D上具有二阶连续偏导数，记$$A=f_{x x}^{\prime \prime}(x, y), B=f_{x y}^{\prime \prime}(x, y), C=f_{y y}^{\prime \prime}(x, y)​$$ 则：

- 在D上恒有A>0，且$$A C-B^{2} \geq 0$$ 时，$$f(x, y)​$$  在区域D上是凸函数
- 在D上恒有A<0，且$$A C-B^{2} \geq 0$$ 时，$$f(x, y)​$$  在区域D上是凹函数

## 二元凹凸函数求最值：

设$$f(x, y)$$ 是在开区域D内具有连续偏导数的凸（或者凹）函数，$$\left(x_{0}, y_{0}\right) \in D$$ 且 $$f_{x}^{\prime}\left(x_{0}, y_{0}\right)=0, f_{y}^{\prime}\left(x_{0}, y_{0}\right)=0$$ 则$$f\left(x_{0}, y_{0}\right)$$ 必为$$f(x, y)$$ 在D内的最小值（或最大值）

## 求解偏置b

### 证明损失函数E(w,b)是关于w和b的凸函数-----$$A=f_{x x}^{\prime \prime}(x, y)​$$
$$
\begin{aligned} \frac{\partial E_{(w, b)}}{\partial w} &=\frac{\partial}{\partial w}\left[\sum_{i=1}^{m}\left(y_{i}-w x_{i}-b\right)^{2}\right] \\ &=\sum_{i=1}^{m} \frac{\partial}{\partial w}\left(y_{i}-w x_{i}-b\right)^{2} \\ &=\sum_{i=1}^{m} 2 \cdot\left(y_{i}-w x_{i}-b\right) \cdot\left(-x_{i}\right) \\ &=2\left(w \sum_{i=1}^{m} x_{i}^{2}-\sum_{i=1}^{m}\left(y_{i}-b\right) x_{i}\right) \end{aligned}
$$
aa
$$
\begin{aligned} \frac{\partial^{2} E_{(w, b)}}{\partial w^{2}} &=\frac{\partial}{\partial w}\left(\frac{\partial E_{(w, b)}}{\partial w}\right) \\ &=\frac{\partial}{\partial w}\left[2\left(w \sum_{i=1}^{m} x_{i}^{2}-\sum_{i=1}^{m}\left(y_{i}-\hat{v}\right) x_{i}\right]\right] \\ &=\frac{\partial}{\partial w}\left[2 w \sum_{i=1}^{m} x_{i}^{2}\right] \\ &=2 \sum_{i=1}^{m} x_{i}^{2} \end{aligned}
$$
### 证明损失函数E(w,b)是关于w和b的凸函数-----$$B=f_{x y}^{\prime \prime}(x, y)​$$
$$
\begin{aligned} \frac{\partial^{2} E_{(u, b)}}{\partial u \partial b} &=\frac{\partial}{\partial b}\left(\frac{\partial E_{(u, b)}}{\partial w}\right) \\ &=\frac{\partial}{\partial b}\left[2\left(w \sum_{i=1}^{m} x_{i}^{2}-\sum_{i=1}^{m}\left(y_{i}-b\right) x_{i}\right)\right] \\ &=\frac{\partial}{\partial b}\left[-2 \sum_{i=1}^{m}\left(y_{i}-b\right) x_{i}\right] \\ &=\frac{\partial}{\partial b}\left(-2 \sum_{i=1}^{m} y_{i} x_{i}+2 \sum_{i=1}^{m} b x_{i}\right) \\ &=\frac{\partial}{\partial b}\left(2 \sum_{i=1}^{m} b x_{i}\right)=2 \sum_{i=1}^{m} x_{i} \end{aligned}
$$
#### 证明损失函数E(w,b)是关于w和b的凸函数-----$$C=f_{y y}^{\prime \prime}(x, y)$$ 
$$
\begin{aligned} \frac{\partial E_{(w, b)}}{\partial b} &=\frac{\partial}{\partial b}\left[\sum_{i=1}^{m}\left(y_{i}-w x_{i}-b\right)^{2}\right] \\ &=\sum_{i=1}^{m} \frac{\partial}{\partial b}\left(y_{i}-w x_{i}-b\right)^{2} \\ &=\sum_{i=1}^{m} 2 \cdot\left(y_{i}-w x_{i}-b\right) \cdot(-1) \\ &=2\left(m b-\sum_{i=1}^{m}\left(y_{i}-w x_{i}\right)\right) \end{aligned}
$$
fg 
$$
\begin{aligned} \frac{\partial^{2} E_{(u, b)}}{\partial b^{2}} &=\frac{\partial}{\partial b}\left(\frac{\partial E_{(w, b)}}{\partial b}\right) \\ &=\frac{\partial}{\partial b}\left[2\left(m b-\sum_{i=1}^{m}\left(y_{i}-u x_{i}\right)\right]\right.\\ &=\frac{\partial}{\partial b}(2 \pi b) \\ &=2 m \end{aligned}
$$
aa
$$
A=2 \sum_{i=1}^{m} x_{i}^{2} \quad B=2 \sum_{i=1}^{m} x_{i} \quad C=2 m
$$
则
$$
\begin{aligned} A C-B^{2} &=2 m \cdot 2 \sum_{i=1}^{m} x_{i}^{2}-\left(2 \sum_{i=1}^{m} x_{i}\right)^{2}  \\ &= 4 m \sum_{i=1}^{m} x_{i}^{2}-4\left(\sum_{i=1}^{m} x_{i}\right)^{2} \\ &=4 m \sum_{i=1}^{m} x_{i}^{2}-4 \cdot m \cdot \frac{1}{m} \cdot\left(\sum_{i=1}^{m} x_{i}\right)^{2} \\ &=4 m \sum_{i=1}^{m} x_{i}^{2}-4 m \cdot \bar{x} \cdot \sum_{i=1}^{m} x_{i} \\ &=4 m\left(\sum_{i=1}^{m} x_{i}^{2}-\sum_{i=1}^{m} x_{i} \bar{x}\right) \\ &=4 m \sum_{i=1}^{m}\left(x_{i}^{2}-x_{i} \bar{x}\right) \end{aligned}
$$
又
$$
\sum_{i=1}^{m} x_{i} \bar{x}=\bar{x} \sum_{i=1}^{m} x_{i}=\bar{x} \cdot m \cdot \frac{1}{m} \cdot \sum_{i=1}^{m} x_{i}=m \bar{x}^{2}=\sum_{i=1}^{m} \bar{x}^{2}
$$
则上式可化简为
$$
\begin{aligned} 4 m \sum_{i=1}^{m}\left(x_{i}^{2}-x_{i} \bar{x}\right)\\ &=4 m \sum_{i=1}^{n_{i}}\left(x_{i}^{2}-x_{i} \bar{x}-x_{i} \bar{x}+x_{i} \bar{x}\right)\\ &=4 m \sum_{i=1}^{m}\left(x_{i}^{2}-x_{i} \bar{x}-x_{i} \bar{x}+\bar{x}^{2}\right)\\ &=4 m \sum_{i=1}^{m}\left(x_{i}-\bar{x}\right)^{2} \end{aligned}
$$
所以$$A C-B^{2}=4 m \sum_{i=1}^{m}\left(x_{i}-\bar{x}\right)^{2} \geq 0$$ 是凸函数，即$$E(w, b)​$$

对损失函数  关于b求一阶偏导数
$$
\frac{\partial E_{(w, b)}}{\partial b}=2\left(m b-\sum_{i=1}^{m}\left(y_{i}-w x_{i}\right)\right)
$$
另一阶偏导数为0
$$
\begin{aligned} \frac{\partial E_{(w, b)}}{\partial b} &=2\left(m b-\sum_{i=1}^{m}\left(y_{i}-w x_{i}\right)\right)=0 \\ & m b-\sum_{i=1}^{m}\left(y_{i}-w x_{i}\right)=0 \\ & b=\frac{1}{m} \sum_{i=1}^{m}\left(y_{i}-w x_{i}\right) \end{aligned}
$$

$$
b=\frac{1}{m} \sum_{i=1}^{m} y_{i}-w \cdot \frac{1}{m} \sum_{i=1}^{m} x_{i}=\bar{y}-w \bar{x}
$$

## 求w

另w的一阶偏导数=0
$$
\begin{aligned} \frac{\partial E_{(w, b)}}{\partial w}=& 2\left(w \sum_{i=1}^{m} x_{i}^{2}-\sum_{i=1}^{m}\left(y_{i}-b\right) x_{i}\right)=0 \\ & w \sum_{i=1}^{m} x_{i}^{2}-\sum_{i=1}^{m}\left(y_{i}-b\right) x_{i}=0 \\ & w \sum_{i=1}^{m} x_{i}^{2}=\sum_{i=1}^{m} y_{i} x_{i}-\sum_{i=1}^{m} b x_{i} \end{aligned}
$$
代入b
$$
\begin{array}{l}{w \sum_{i=1}^{m} x_{i}^{2}=\sum_{i=1}^{m} y_{i} x_{i}-\sum_{i=1}^{m}(\bar{y}-w \bar{x}) x_{i}} \\ {w \sum_{i=1}^{m} x_{i}^{2}=\sum_{i=1}^{m} y_{i} x_{i}-\bar{y} \sum_{i=1}^{m} x_{i}+w \bar{x} \sum_{i=1}^{m} x_{i}} \\ {w \sum_{i=1}^{m} x_{i}^{2}-w \bar{x} \sum_{i=1}^{m} x_{i}=\sum_{i=1}^{m} y_{i} x_{i}-\bar{y} \sum_{i=1}^{m} x_{i}} \\ {v\left(\sum_{i=1}^{m} x_{i}^{2}-\bar{x} \sum_{i=1}^{m} x_{i}\right)=\sum_{i=1}^{m} y_{i} x_{i}-\bar{y} \sum_{i=1}^{m} x_{i}}\end{array}
$$
所以
$$
w=\frac{\sum_{i=1}^{m} y_{i} x_{i}-\bar{y} \sum_{i=1}^{m} x_{i}}{\sum_{i=1}^{m} x_{i}^{2}-\bar{x} \sum_{i=1}^{m} x_{i}}
$$
其中$$\bar{y} \sum_{i=1}^{m} x_{i}$$ ，可替换为
$$
\bar{y} \sum_{i=1}^{m} x_{i}=\frac{1}{m} \sum_{i=1}^{m} y_{i} \sum_{i=1}^{m} x_{i}=\bar{x} \sum_{i=1}^{m} y_{i}
$$
  分母 中 $$\bar{x} \sum_{i=1}^{m} x_{i}$$可替换为
$$
\sqrt{\bar{x} \sum_{i=1}^{m} x_{i}}=\frac{1}{m} \sum_{i=1}^{m} x_{i} \sum_{i=1}^{m} x_{i}=\frac{1}{m}\left(\sum_{i=1}^{m} x_{i}\right)^{2}
$$
最终
$$
w=-\frac{\sum_{i=1}^{m} u_{i} x_{i}-\bar{x} \sum_{i=1}^{m} y_{i}}{\sum_{i=1}^{m} x_{i}^{2}-\frac{1}{m}\left(\sum_{i=1}^{m} x_{i}\right)^{2}}=\frac{\sum_{i=1}^{m} y_{i}\left(x_{i}-\bar{x}\right)}{\sum_{i=1}^{m} x_{i}^{2}-\frac{1}{m}\left(\sum_{i=1}^{m} x_{i}\right)^{2}}
$$
