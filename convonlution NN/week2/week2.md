### Classic Networks

![picture1](picture1.png)

![picture13](picture13.png)

### ResNets

ResNets are built out of something called a residual block

![picture2](picture2.png)![picture3](picture3.png)

### Why ResNets work?

if you make a network deeper, it can hurt your ability to train the network to do well on the training set. 

![picture4](picture4.png)

### Why dose a 1*1 convolution do?

![picture5](picture5.png)缩小Chanel 的数量(n_c)

Pooling layer 可以缩小n_h & n_w

you've now seen how a one by one convolution operation is actually doing a pretty non-trivial operation and it allows you to shrink the number of channels in your volumes or keep it the same or even increase it if you want. 

### Inception Network Motivation

![picture6](picture6.png)

![picture7](picture7.png)减少计算量做法，其中28*28*16被称为bottleneck layer

![picture8](picture8.png)

### Inception Network

![picture9](picture9.png)

## Practical advices for using ConvNets

### Data Augmentation

![picture10](picture10.png)![picture11](picture11.png)

![picture12](picture12.png)![picture14](picture14.png)