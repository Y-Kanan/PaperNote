# Decoding EEG by Visual-guided Deep Neural Networks

> Paper Info:
>
> IJCAI2019
>
> University of North Carolina at Chapel Hill, USA
>
> School of Software, Tsinghua University, China

## 1. 简介

在本文中，我们提出使用视觉表示来指导脑电的解码。我们的解码框架包含两个阶段:

(1)视觉引导的脑电分类阶段;

(2)视觉引导刺激产生阶段。

在第一步中，以视觉表征为指导建立分类网络，将脑电信号分类为相关的视觉刺激类别。然后，在生成阶段，一个改进的生成对抗网络(GAN) 通过视觉引导的脑电图表象产生相应的视觉刺激。

## 2. 方法

**==stage1: Visual-guided EEG Classifification==** 对看到的图像时的脑电信号进行分类

在认知领域，脑电信号首先被组织成EEG maps $X_{cog}$，其中轴表示EEG通道和每个通道的记录

<img src="C:\Users\YJN\AppData\Roaming\Typora\typora-user-images\image-20200523110242292.png" alt="image-20200523110242292" style="zoom:67%;" />

<img src="C:\Users\YJN\AppData\Roaming\Typora\typora-user-images\image-20200523144244658.png" alt="image-20200523144244658" style="zoom:67%;" />

<img src="C:\Users\YJN\AppData\Roaming\Typora\typora-user-images\image-20200523144421054.png" alt="image-20200523144421054" style="zoom:50%;" />

**==stage2: Visual-guided Stimuli Generation==** 根据脑电信号生成意识图

<img src="C:\Users\YJN\AppData\Roaming\Typora\typora-user-images\image-20200523151017948.png" alt="image-20200523151017948" style="zoom:67%;" />

整个模型$Loss$

<img src="C:\Users\YJN\AppData\Roaming\Typora\typora-user-images\image-20200523150918172.png" alt="image-20200523150918172" style="zoom: 50%;" />

## 2. 实验

我们的解码方法不仅可以分类，还可以从单次试验的脑电图数据中重建视觉刺激。因此，我们实验的==第一个目的==是研究代表不同类别的视觉刺激的脑电图数据能否被准确地分类。==另一个目标==是评估我们的方法是否能够重建相关的图像脑电图记录。下面将分别详细介绍分类和生成的性能。

<img src="C:\Users\YJN\AppData\Roaming\Typora\typora-user-images\image-20200523152128215.png" alt="image-20200523152128215" style="zoom:50%;" />



