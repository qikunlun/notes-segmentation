# Notes Semantic Segmentation

本文记录一些关于图像语义分割的经典论文的相关内容，主要因本人需要准备博后基金，记录一些想法相关的内容。

- [Fully Convolutional Networks](#fully-convolutional-networks)
- [Conditional Random Field](#conditional-random-field)
- [Markov Random Field](#markov-random-field)

----

## Fully Convolutional Networks
当前语义分割从深度学习引入FCN到现在，基本上形成一个通用的框架，即FCN+CRF/MRF，FCN进行特征粗提取，CRF/MRF优化输出结果。


### 2017-E.Shelhamer-Fully Convolutional Networks for Semantic Segmentation
由于分类网络中最后几层全连接层会会将矩阵转化为一维向量，从而丢失了空间信息。本文提出一种端到端、像素到像素训练的全卷积网络，能够基于预训练的AlexNet、VGGNet或者GoogLeNet，实现任意尺寸输入图像的像素级预测。语义分割中，全局信息解决“是什么”的问题，而局部信息解决“在哪里”的问题，方法集合了深层、粗粒度的语义信息和浅层细粒度的表征信息，并实现跨层架构。卷积层以平移不变性为基础，其基本组成部分（卷积层、池化层和激励函数）一般作用在局部输入域，只依赖于相对空间坐标。


FCN中的三个主要技术：
* 卷积（Convolutional），即丢弃传统CNN，如VGG等网络的全连接层；
* 上采样（Upsample），即反卷积（Deconvolution）或conv_transpose；
* 跳跃结构（Skip Layer），对不同池化层结果进行上采样从而优化结果。


### 2016-L.Chen-DeepLab: Semantic Image Segmentation with Deep Convolutional Nets, Atrous Convolution, and Fully Connected CRFs
FCN结构为了保证输出的尺寸和原图一致，直接对原图加了100的padding，难免引入噪声。DeepLab的做法：将pooling的stride修改为1，再加上1的padding，这样池化后的图片尺寸就不会减少，但依然保留池化层整合特征的性质。
但是随之而来的问题是，池化层的变化导致卷积层的感受野发生相应的改变，这样就无法fine-tune。DeepLab的做法是提出一种新的卷积：带孔的卷积（Atrous Convolution）。

----

## Conditional Random Field 
CRF（条件随机场）用于优化输出结果，论文一般针对不同的能量函数进行优化。


### 2014-L.Chen-Semantic Image Segmentation with Deep Convolutional Nets and Fully Connected CRFs
出发点：DCNNs的不变性使其适合于高层次的任务，但在分割任务上表现一般。CRF的能量函数由一元势函数（FCN的输出）和二元势函数（像素点之间的关系）两部分组成。本文采用的全连接条件随机场的创新在于，二元势函数描述每一个像素与其他所有像素之间的关系，所以叫“全连接”。


### 2015-S.Zheng-Conditional Random Fields as Recurrent Neural Networks
深度学习一般追求end-to-end的系统，

----

## Markov Random Field


### 2015-Z.Liu-Semantic Image Segmentation via Deep Parsing Network
Deep Parsing Network中使用MRF，作者对二元势函数进行了修改，不仅包含两个像素同时出现的概率，而且对一些可能性较小的情况进行惩罚；并且引入了triple penalty，即附近的附近这样三方关系便于得到更充足的局部上下文。Deep Parsing Network结构的优点在于：将平均场构造成CNN；联合训练可以one-pass interface，无需迭代。

