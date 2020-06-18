# Aftershock Detection with Multi-Scale Description based Neural Network

> **Paper info:**
>
> ICDM2019
>
> Qi Zhang, Tong Xu,  Lifu Zhang, Hui Xiong, Enhong Chen, Qi Liu

## Contribution

- We propose a novel neural network based solution, i.e., MSDNN, for the aftershock detection task, which adapts the traditional STA/LTA methods with integrating the advanced neural networks, and fully exploits the seismic features with multi-scale description.

- We design a multi-task learning strategy to better describe the relationship between seismic waveforms recorded by different monitoring stations, which further refifines the performance of aftershock detection.

- We evaluate our framework with extensive experiments on the data set from aftershocks of the Wenchuan M8.0 Earthquake. The experimental results clearly validate the effectiveness of MSDNN, compared with several state-of-the-art baselines.

  > the neural network approach we proposed in this paper is based on the multi-scale description structure and the multi-task learning strategy.

## Dataset description

The seismic data set used in our paper is the monitoring signal from aftershocks of the Wenchuan M8.0 Earthquake.

- 2833 aftershocks——9891pieces of seismic waveforms in short time window

- Three channel: Z, N, E (from 15 station)

- Frequency: 100Hz

  ![image-20200513201138890](C:\Users\YJN\AppData\Roaming\Typora\typora-user-images\image-20200513201138890.png)

同时考虑三个信道

==STA== 10s 可以反映信号的实时变化，没有随机波动，但趋势信息不明确。

==LTA== 0.5s 反映趋势信息

==引入$\frac{STA}{LTA}$==

![image-20200513212810967](C:\Users\YJN\AppData\Roaming\Typora\typora-user-images\image-20200513212810967.png)

## Model

$$
D=\{d_1,d_2...d_n\}\\
d_i=\{z_i,e_i,n_i\}\\
l=\{0,1\}
$$

![image-20200513213944230](C:\Users\YJN\AppData\Roaming\Typora\typora-user-images\image-20200513213944230.png)

### MSD Cell

- function
  - 在不同尺度上记住先前的特征并增添新的特征 (like LSTM)
  - 比较并融合两种特征（like inception net）

- input: $S_i$(*memory status)*, $F_i$*(feature status)*

### MSDNN

<img src="C:\Users\YJN\AppData\Roaming\Typora\typora-user-images\image-20200514110238558.png" alt="image-20200514110238558" style="zoom:67%;" />

- Shared part 

  the *shared part* will be shared in multi-task learning strategy

- Detection part

- Auxiliary part

- loss
  $$
  L_{main}=-\frac{1}{n}\sum_{i=1}^n[l_ilogy_i+(1-l_i)log(1-y_i)]+\frac{\lambda}{2n}\sum{||\omega||}^2\\
  L_{multi}=L_{main}+\frac{\lambda}{2k}\sum_{w^h}{||{\omega}^h||}^2-\frac{1}{k}\sum_{i=1}^k[l_i^hlogy_i^h+(1-l_i^h)log(1-y_i^h)]
  $$

**multi-task learning**

> The objective of this auxiliary task is to determine whether the two seismic waveforms are homologous. 

## Experiment

multi-task learning task 和 main task交替训练

**Baseline**

- *ConvNetQuake*

- *Inception Net*

- *XGboost*  and *Random Forest*

- *Support Vector Machine* and *Logistic Regression*

![image-20200514151015989](C:\Users\YJN\AppData\Roaming\Typora\typora-user-images\image-20200514151015989.png)



验证多任务学习的作用

1. 计算正样本与负样本的欧氏距离，多任务学习4.3/3.7
2. PCA对网络的特征进行可视化
3. 可优化特征分布，提高余震检测准确率

