# Awesome Semantic Segmentation

本文记录一些关于图像语义分割的经典论文的相关内容，主要因本人需要准备博后基金，记录一些想法相关的内容。

**Table Of Contents**
- [Fully Convolutional Networks](#fully-convolutional-networks)
- [Conditional Random Field](#conditional-random-field)

----

## Fully Convolutional Networks
当前语义分割从深度学习引入FCN到现在，基本上形成一个通用的框架，即FCN+CRF/MRF，前端FCN进行特征粗提取，后端作用CRF/MRF优化前端的输出。


### 2017_E.Shelhamer_Fully Convolutional Networks for Semantic Segmentation
由于分类网络中最后几层全连接层会会将矩阵转化为一维向量，从而丢失了空间信息。本文提出一种端到端、像素到像素训练的全卷积网络，能够基于预训练的AlexNet、VGGNet或者GoogLeNet，实现任意尺寸输入图像的像素级预测。语义分割中，全局信息解决“是什么”的问题，而局部信息解决“在哪里”的问题，方法集合了深层、粗粒度的语义信息和浅层细粒度的表征信息，并实现跨层架构。卷积层以平移不变性为基础，其基本组成部分（卷积层、池化层和激励函数）一般作用在局部输入域，只依赖于相对空间坐标。


FCN中的三个主要技术：
* 卷积（Convolutional），即丢弃传统CNN，如VGG等网络的全连接层；
* 上采样（Upsample），即反卷积（Deconvolution）或conv_transpose；
* 跳跃结构（Skip Layer），对不同池化层结果进行上采样从而优化结果。

----

## Conditional Random Field 
