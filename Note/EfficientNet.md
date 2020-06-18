# **EfficientNet: Rethinking Model Scaling for Convolutional Neural Networks**

[toc]

> ### **Paper Info: **
>
> ICML2019
>
> **Mingxing Tan** ；**Quoc V. Le** 

## Background

卷积神经网络(ConvNets)通常是在固定的资源预算下开发的，如果有更多的资源可用，则会进行扩展以获得更高的精度。在文中，作者系统地研究了模型缩放，并发现仔细平衡网络的深度、宽度和分辨率可以获得更好的性能。基于这一观察结果，我们提出了一种新的标度方法，使用简单而高效的复合系数来均匀地标度深度/宽度/分辨率的所有维度。我们证明了该方法的有效性

论文提出了一种**多维度混合的模型放缩方法**

## Motivation

作者希望找到一个可以同时兼顾**速度与精度**的模型放缩方法，为此，作者重新审视了前人提出的模型放缩的几个维度：**网络深度、网络宽度、图像分辨率**，前人的文章多是放大其中的一个维度以达到更高的准确率，比如 ResNet-18 到 ResNet-152 是通过增加网络深度的方法来提高准确率。

作者跳出了前人对放缩模型的理解，作者认为这三个维度之间是互相影响的并探索出了三者之间最好的组合，在此基础上提出了最新的网络 EfficientNet，该网络的表现如下

<img src="C:\Users\YJN\AppData\Roaming\Typora\typora-user-images\image-20200505201123881.png" alt="image-20200505201123881" style="zoom:67%;" />

大大提高了网络的实用性以及工业落地可能。

## 问题抽象

下面要将这个问题用公式的方式表示出来，符号会比较多，不过并不难理解。我们将整个卷积网络称为 N，它的第 i 个卷积层可以看作是下面的函数映射：
                                                                            ![Y_i=F_i(X_i)](https://math.jianshu.com/math?formula=Y_i%3DF_i(X_i))

![Y_i](https://math.jianshu.com/math?formula=Y_i)为输出张量，![X_i](https://math.jianshu.com/math?formula=X_i)为输入张量，设其维度为 ![<H_i, W_i, C_i>](https://math.jianshu.com/math?formula=%3CH_i%2C%20W_i%2C%20C_i%3E) (这里为了方便叙述省略了 Batch 维度)，那么整个卷积网络 N，由 k 个卷积层组成，可以表示为：
										 ![N=F_k \odot ...\odot F_2 \odot F_1(X_1) = \odot_{j=1...k} F_j(X_1)](https://math.jianshu.com/math?formula=N%3DF_k%20%5Codot%20...%5Codot%20F_2%20%5Codot%20F_1(X_1)%20%3D%20%5Codot_%7Bj%3D1...k%7D%20F_j(X_1))

优化目标函数：

<img src="C:\Users\YJN\AppData\Roaming\Typora\typora-user-images\image-20200505202142126.png" alt="image-20200505202142126" style="zoom: 67%;" />

为了减小搜索空间，作者固定了网络的基本结构，而只变动上面提到的三个放缩维度，**网络深度(Li)，网络宽度(Ci)，输入分辨率大小(Hi, Wi)**。然而就算只搜索这三个维度，搜索空间也很大，因此作者又加了一个限制，网络的放大只能在初识网络(就是后面的 EfficientNet-B0)的基础上乘上常数倍率

## Experiment

1. **只在一个维度上进行放缩**

<img src="C:\Users\YJN\AppData\Roaming\Typora\typora-user-images\image-20200505141557629.png" alt="image-20200505141557629" style="zoom:50%;" />

扩展网络宽度、深度或分辨率的任何维度都可以提高精度，但是对于较大的模型，精度增益会降低。

2. **多维度的放缩组合**

<img src="C:\Users\YJN\AppData\Roaming\Typora\typora-user-images\image-20200505142100988.png" alt="image-20200505142100988" style="zoom:67%;" />

为了追求更高的精度和效率，在ConvNet缩放期间平衡网络宽度、深度和分辨率的所有维度是至关重要的。

由此，作者提出了一种**混合维度放大法(compound scaling method)**，该方法使用一个混合系数来决定3个维度的放大倍率Φ。

<img src="C:\Users\YJN\AppData\Roaming\Typora\typora-user-images\image-20200505145124505.png" alt="image-20200505145124505" style="zoom: 67%;" />

其中，α，β，γ均为常数(不是无限大的因为三者对应了计算量)，可通过网格搜索获得。混合系数 ![\phi](https://math.jianshu.com/math?formula=%5Cphi) 可以人工调节。考虑到如果网络深度翻番那么对应计算量会翻番，而网络宽度或者图像分辨率翻番对应计算量会翻 4 番，即卷积操作的计算量(FLOPS) 与 ![d,w^2,r^2](https://math.jianshu.com/math?formula=d%2Cw%5E2%2Cr%5E2) 成正比，因此上图中的约束条件中有两个平方项。在该约束条件下，指定混合系数 ![\phi](https://math.jianshu.com/math?formula=%5Cphi) 之后，网络的计算量大概会是之前的 ![2^\phi](https://math.jianshu.com/math?formula=2%5E%5Cphi) 倍。

## EfficientNet网络结构

主要借鉴了 MnasNet，采取了同时优化精度(ACC)以及计算量(FLOPS)的方法，由此产生了初代 EfficientNet-B0，其结构如下图:

![image-20200505203138478](C:\Users\YJN\AppData\Roaming\Typora\typora-user-images\image-20200505203138478.png)

有了初代模型以后进行scale，分两步：

第一步，首先固定 ![\phi](https://math.jianshu.com/math?formula=%5Cphi) 为 1，即设定计算量为原来的 2 倍，在这样一个小模型上做网格搜索(grid search)，得到了最佳系数为 ![\alpha=1.2,\beta=1.1,\gamma=1.15](https://math.jianshu.com/math?formula=%5Calpha%3D1.2%2C%5Cbeta%3D1.1%2C%5Cgamma%3D1.15) 。

第二步，固定  ![\alpha=1.2,\beta=1.1,\gamma=1.15](https://math.jianshu.com/math?formula=%5Calpha%3D1.2%2C%5Cbeta%3D1.1%2C%5Cgamma%3D1.15)，使用不同的混合系数 ![\phi](https://math.jianshu.com/math?formula=%5Cphi) 来放大初代网络得到 EfficientNet-B1 ～ EfficientNet-B7。

我们的方法在小基线网络上只做一次搜索(步骤1)，然后对所有其他模型使用相同的比例系数(步骤2)。

## Result

- EfficientNet 和其他流行的网络结构在imageNet上的比较

![image-20200505203809190](C:\Users\YJN\AppData\Roaming\Typora\typora-user-images\image-20200505203809190.png)

- 不同scale方法在MobileNets和ResNets上的效果

  <img src="C:\Users\YJN\AppData\Roaming\Typora\typora-user-images\image-20200505210252483.png" alt="image-20200505210252483" style="zoom:67%;" />

- 方法的可迁移性探究，在多个数据集上进行实验，对比准确率与参数规模

  <img src="C:\Users\YJN\AppData\Roaming\Typora\typora-user-images\image-20200505210506849.png" alt="image-20200505210506849" style="zoom:150%;" />

论文提出的新网络兼顾了速度和精度，非常实用，可以作为通用的 baseline