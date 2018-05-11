---
layout: post

title: 'batch Normalization 学习'

subtitle: '15331404 张益强'

date: 2018-03-10

categories: tensorflow datamining

cover: 'https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcSJmUnN6ur0wCWy1Nb_U_v4GN4CbryYxmmRA7G5QDMdeZSP0-v0'

tags: datamining tensorflow
---

# batch Normalization 学习

## 1. 背景意义
讲解2015年非常值得学习的一篇文献《Batch Normalization: Accelerating Deep Network Training by  Reducing Internal Covariate Shift》

### 1.1 BN之前
> 饱和问题（saturationproblem）和导致的消失梯度通常通过使用Rectified Linear Units（ReLU）来解决

BN出现之前，需要我们人为的去选择参数，比如学习率、参数初始化、权重衰减系数、Drop out比例等。这些参数的选择对训练结果至关重要，以至于我们很多时间都浪费在这些的调参上

### 1.2 BN的强大

(1) 你可以选择比较大的初始学习率，让你的训练速度飙涨。以前还需要慢慢调整学习率，甚至在网络训练到一半的时候，还需要想着学习率进一步调小的比例选择多少比较合适，现在我们可以采用初始很大的学习率，然后学习率的衰减速度也很大，因为这个算法收敛很快。当然这个算法即使你选择了较小的学习率，也比以前的收敛速度快，因为它具有快速训练收敛的特性；

(2) 你再也不用去理会过拟合中drop out、L2正则项参数的选择问题，采用BN算法后，你可以移除这两项了参数，或者可以选择更小的L2正则约束参数了，因为BN具有**提高网络泛化能力**的特性；

(3) 再也不需要使用使用局部响应归一化层了（局部响应归一化是Alexnet网络用到的方法，搞视觉的估计比较熟悉），因为BN本身就是一个归一化网络层；

(4) 可以把训练数据彻底打乱

### 1.3 normalization 预处理（数据归一化）

>  解决了Internal Covariate Shift。:数据分布在激活函数的收敛区的问题

作用：使得输入x的变化范围不会太大，让输入值经过激励函数的敏感部分。解决了Internal Covariate Shift。

归一化最简单的办法就是减均值/标准差。虽然这种方法可以让网络的输入层避免梯度消失的问题，但中间层的数据分布依然不可控

其他的办法：白化等

![](https://ws1.sinaimg.cn/large/c3af64f1gy1fqk0wl5fpxj20fv0kvq57.jpg)


## 2. BN简述

在网络的每一层输入的时候，又插入了一个归一化层，也就是先做一个归一化处理，然后再进入网络的下一层
**BN的想法：让网络中间每一层的数据都归一化。通过在训练过程中保持层输入X的分布来提高训练速度**

## 3. BN实现
![](https://ws1.sinaimg.cn/large/c3af64f1gy1fqi7pn737ij20d108jmyz.jpg)



## 4. BN在tensorflow中的实现


## 5. 参考
[jermmy.BN论文笔记](http://jermmy.xyz/2017/09/02/2017-9-2-paper-notes-batch-normalization/)


[hjimce-机器学习笔记](https://blog.csdn.net/hjimce/article/details/50866313)

