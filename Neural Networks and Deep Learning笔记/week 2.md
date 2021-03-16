## Logistic Regression as a Nerual Network

### Binary Classification

it turns out that when you're implementing a neural network, you usually want to process your entire training set without using an explicit four loop to loop over your entire training set.

Logistic regression is an algorithm for binary classification. 逻辑回归是一个二分类算法。

__RGB__   o store an image your computer stores three separate matrices corresponding to the red, green, and blue color channels of this image.        每个图片的每个像素点由red green blue三种颜色组成，如果说一个图片64 * 64的像素组成的话，那么这个图片所对应的3个64 * 64的矩阵

#### Notation

$(x,y)\quad x\in R^{n_x},y\in \{0,1\} $

m: the number of training samples

$X = [x_1,x_2,...,x_m],x_1,x_2...,x_m有n行$      矩阵X 为n*m的矩阵

$Y=[y^{(1)},y^{(2)},...y^{(m)}]\quad Y\in R^{1 * m}$

### Logistic Regression

Given X, to get $\hat{y}=P\{y=1|x\}$

W is a dimensionals vector, b is a real number.

$X\in R^{n_x},W\in R^x,b\in R$ 

$\hat{y}=activation function(W^TX+b)$

### Logistic Regression Cost Function

Given ${(x_1,y_1),...,(x_m,y_m)}$, want $\hat{y}^{(i)}\approx y^{(i)}$

$Z^{(i)}=W^TX^{(i)}+b$

#### Loss function in Logistic Regression:

$L(\hat{y},y)=-(ylog\hat{y}+(1-y)log(1-\hat{y}))$

#### cost function :

$J(W,b)=\frac{1}{m}\sum_{i=0}^mL(\hat{y},y)$



### Gradient Descent

#### explain: 

​	gradient:梯度   descent:下降  convex:凸的 steep:陡峭的

​	:=表示迭代 derivative:导数的 converge:收敛的 slope:斜率 calculus:微积分 foray:初步尝试

 

And for logistic regression almost any initialization method works, usually you initialize the value to zero. Random initialization also works, but people don't usually do that for logistic regression. But because this function is convex, no matter where you initialize, you should get to the same point or roughly the same point. And what gradient descent does is it starts at that initial point and then takes a step in the steepest downhill direction.

$W:=W-\frac{dJ(W)}{dW}$



### Logistic Regression Gradient Descent

$$
Z=W^TX+b
$$


$$
\hat{y}=a=sigmoid(Z)
$$

$$
L(a,y)=-(ylog(a)+(1-y)log(1-a))
$$

the example has two features $W1,X1,W2,X2,b$

$Z=W_1X_1+W_2X_2+b\quad->\quad\hat{y} = sigmoid(Z)=a\quad -> \quad L(a,y) \quad$

通过modify W,B来decent loss

$da=\frac{dL(a,y)}{da}=-\frac{y}{a}+\frac{1-y}{1-a}$

$dz=\frac{dL(a,y)}{dz}=\frac{dL(a,y)}{da}\frac{da}{dz} =a-y$     链式法则来完成！sigmoid函数性质$f'=f(1-f)$

$dw_1=\frac{dL(a,y)}{dw_1}=x_1dz$

$dw_2=\frac{dL(a,y)}{dw_2}=x_2dz$

$db=dz$



## python and vectorization

### vectorization

Vectorization can significantly speed up code in deep learning.

Whenever possible, avoid explicit for-loops.

 non-loop

```python
import numpy as np
def sigmoid(x):
	return  1/(1 + np.exp(-x)) 
Z=np.dot(W.T,X)+b
A=sigmoid(Z)
```



$dZ^{(1)}=a^{(1)}-y^{(1)}\quad dZ^{(2)}=a^{(2)}-y^{(2)}...$

$dZ=[dZ^{(1)},dZ^{(2)}...dZ^{(m)}]$

$A=[a^{(1)},a^{(2)}...a^{(m)}]\quad Y=[y^{(1)},y^{(2)}...,y^{(m)}]$

$dZ=A-Y$

```python
Z=np.dot(W.T,X)+b
A=sigmoid(Z)
dZ=A-Y
dW=1/m*np.dot(X,dZ.T)
db=1/m*np.sum(dZ)
W=W-rate*dW
b=b-rate*db
```



不要这样写，这样写的话是秩为一的向量

```python
a=np.random.randn(5)#如果得到这种情况的话，reshape下
```

应这样写：

```python
a=np.random.randn(5,1)#column vector
```

或者

```python
a=np.random.randn(1,5)#row vector
```

每当不确定某一矩阵或者向量的维度时，使用assert来进行操作一下

```python
assert(a.shape==(5,1))
```

$\hat{y}=P(y=1|x)$

If $y==1$: $P(y|x)=\hat{y}$

If $y==0$:$P(y|x)=1-\hat{y}$

上面的两个方程整理为一个方程：

$P(y|x)=\hat{y}^y(1-\hat{y})^{(1-y)}$

$max\quad P(y|x)$，log是一个严格单调递增函数，因此，$max\quad logP(y|x)=ylog\hat{y}+(1-y)log(1-\hat{y})$

在训练集中：

$log\prod_\limits{i=1}^\limits{m}P(y^{(i)}|x^{(i)})=\sum_\limits{i=1}^\limits{m}logP(y^{(i)}|x^{(i)})$





