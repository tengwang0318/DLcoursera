### Computing a Neural Network's Output

$a^{[i]}_j$表示的是第i个hidden layer中的第j个node

hidden layer中的节点的运算可以看作两次运算：

	1. 执行$Z^{[i]}=(W^{[i]})^Ta^{[i-1]}+b^{[i]}$
 	2. 执行$a^{[i]}=activation\quad function(Z^{[i]})$

其中$X=a^{[0]}$

### activation function

$tanh(z)=\frac{e^z-e^{-z}}{e^z+e^{-z}}$  值域：[-1,1] 大多数情况下要比sigmoid更优，其均值集中于0

$sigmoid(z)=\frac{1}{1+e^{-z}}$值域：[0,1] 基本上不会用，除非用在输出层，在二分类问题中使用较多！因为一个类设为1，另一个类设为0，符合sigmoid的值域范围

$tanh(z),sigmoid(z)$都存在一个问题，当z特别大或者特别小的时候，激活函数的导数、梯度或者斜率就会变化特别小

$ReLu\quad function(rectify\quad linear\quad unit):a=max(0,z)$

$leaky Relu function:a=max(0.01z,z)$

### Why do you need non-linear activation functions?

无论hidden layer 有多少层，如果没有非线性的激活函数，那么最终都可以转换成一个线性的激活函数



$sigmoid:g'(x)=g(x)(1-g(x))$

$tanh:g'(x)=1-g(x)^2$

### Gradient descent for Neural Networks

前提：一个hidden layer

Parameters: 

$W^{[1]},b^{[1]},W^{[2]},b^{[2]},N_x=N^{[0]}:input\quad feature,N^{[1]}: hidden \quad units,N^{[2]}:output \quad units$

$W^{[1]}:(N^{[1]}*N^{[0]}),b^{[1]}:(N^{[1]},1),W^{[2]}:(N^{[2]},N^{[1]}),b^{[2]}:(N^{[2]},1)$

$cost\quad function:J=\frac{1}{m}\sum_\limits{i=1}^mL(\hat{y},y)$

$forward\quad propagation:$

1. $Z^{[1]}=W^{[1]}X+b^{[1]}$
2. $A^{[1]}=g^{[1]}(Z^{[1]})$
3. $Z^{[2]}=W^{[2]}A^{[1]}+b^{[2]}$
4. $A^{[2]}=g^{[2]}(Z^{[2]})$

$backward\quad propagation:$

1. $dZ^{[2]}=A^{[2]}-Y$
2. $dW^{[2]}=\frac{1}{m}dZ^{[2]}A^{[1]T}$
3. $db^{[2]}=\frac{1}{m}np.sum(dz^{[2]},axis=1,keepdims=True)$
4. $dZ^{[1]}=W^{[2]T}dZ^{[2]}* g^{[1]'}(Z^{[1]})$
5. $dW^{[1]}=\frac{1}{m}dZ^{[1]}X^T$
6. $db^{[1]}=\frac{1}{m}np.sum(dZ^{[1]},axis=1,keepdims=True)$

### Random Initialization

it's possible to construct a proof by induction that if you initialize all the ways, all the values of w to 0, then because both hidden units start off computing the same function. And both hidden the units have the same influence on the output unit, then after one iteration, that same statement is still true, the two hidden units are still symmetric.

```python
#一般来说这样写
W1=np.random.randn((2,2))*0.01
b1=np.zero((2,1))
```

初始权重W应设置小一点，所有会选择乘以0.01，要不然Z=WX+b的话太大了，通过激活函数时g(Z)，此时曲线斜率特别小，梯度的下降就会十分缓慢