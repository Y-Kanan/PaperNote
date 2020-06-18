# 论文集整理

[TOC]

> **==A类会议==**

## IJCAI

- ### 2019

  - :eye:**Decoding EEG by Visual-guided Deep Neural Networks**==已阅==

    ==通过视觉信息引导的EEG解码，图像转变为feature,EEG转变为feature, ，根据EEG的feature vec生成image,by GAN训练==

  - **Outlier Detection for Time Series with Recurrent Autoencoder Ensembles**

  - **E²GAN: End-to-End Generative Adversarial Network for Multivariate Time Series Imputation**

  - **CLVSA: A Convolutional LSTM Based Variational Sequence-to-Sequence Model with Attention for Predicting Trends of Financial Markets**

  - ~~**ATTAIN: Attention-based Time-Aware LSTM Networks for Disease Progression Modeling**~~==EHR数据集==

  - **BeatGAN: Anomalous Rhythm Detection using Adversarially Generated Time Series** 

  - **Prediction of Mild Cognitive Impairment Conversion Using Auxiliary Information**（利用fMRI数据）

  - ~~**Daytime Sleepiness Level Prediction Using Respiratory Information** ==弃之，司机睡眠状态检测，预测白天嗜睡 HMM==~~

  - ~~**MNN: Multimodal Attentional Neural Networks for Diagnosis Prediction**~~

    ==EHR记录中多模态信息的表示，文本，离散医疗代码，更像文本预测==

  **demo**

  Explainable Deep Neural Networks for Multivariate Time Series Predictions



- ### 2018

## WWW

## NIPS

## ICML

## KDD

## SIGMOD

## AAAI

**==B类会议==**

## CIKM

## ICDM

1. ~~**Temporal Self-Attention Network for Medical Concept Embedding**~~ 

   讲medical concept embedding。。==弃之==

2. :eye:**Aftershock Detection with Multi-scale Description Based Neural Network** ==已阅== multi-task

3. ~~**Know Your Mind: Adaptive Cognitive Activity Recognition with Reinforced CNN**  强化学习  ==弃之==~~

4. **Matrix Profile XVIII: Time Series Mining in the Face of Fast Moving Streams using a Learned Approximate Matrix Profile**

5. **MTEX-CNN: Multivariate Time Series EXplanations for Predictions with Convolutional Neural Networks**

6. :eye:**Triple-Shapelet Networks for Time Series Classification【已下载】**==已阅==

## 偶然看到

【NIPS2016】Dynamic Filter Networks

【CoRR2018】Tempral convolutional network(TCN)

【AAAI2018】Attend and Diagnose: Clinical Time Series Analysis using Attention Models

【CVPR2020】Supervised Contrastive Learning

时间序列补全【南开 罗永洪】https://github.com/Luoyonghong

- 【NIPS2018】Multivariate time series imputation with generative adversarial networks.

- 【IJCAI2019】$E^2GAN$: end-to-end generative adversarial network for multivariate time series imputation.

- :eye:[arXiv2019]Inception Time review

  引：

  - :book:**【PKDD2016】Data Augmentation for Time Series Classification using Convolutional Neural Networks** 

    ——T-LeNet提出(仿照LeNet)，数据增强技术，混合数据集的半监督训练方式

    - :book:[BSPC2013]Bag-of-words representation for biomedical time series classifification

      提出应用于生理时间序列特征表示方法（Bow）

  - **:book:【CoRR2016】MSCNN Multi-scale convolutional neural networks for TSC**

    ——基于CNN，多尺度体现在将原始序列第一层用多个分支不同方式提取特征（时域相同映射，时域下采样，频域变换），卷积并融合特征，最后全卷积，softmax

  - **:eye:【IJCAI2015】Imaging Time-Series to Improve Classification and Imputation**

    ——将TS转化为图像处理

  - :book:【ICLR2014】Network in Network [经典] ——多个mlpconv的叠加

    1. MLP Convolution Layers（创新点1）

    MLPConv其实就是在常规卷积（感受野大于1的）后接若干1x1卷积，每个特征图视为一个神经元，特征图通过1x1卷积就类似多个神经元线性组合，这样就像是MLP（多层感知机）了，这是文章最大的创新点，也就是Network in Network（网络中内嵌微型网络）。

    2. Global Average Pooling（创新点2）

    

医疗时序相关

- **ML-ResNet: A novel network to detect and locate myocardial infarction using 12 leads** ECG （CMPB2020）

- **Multi-branch fusion network for Myocardial infarction screening from 12-lead ECG images.** [Comput. Methods Programs Biomed. 184](https://dblp.uni-trier.de/db/journals/cmpb/cmpb184.html#HaoGLZWB20): 105286 (2020)