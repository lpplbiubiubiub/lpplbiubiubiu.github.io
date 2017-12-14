---
title: Person re-identification using visual attention
description: 对该论文笔记
categories: 论文
comments: true
 - 日记 reid
tags: 论文
---
## 摘要
作者在reid问题中使用了attention的思想，在cuhk01与cuhk03数据集中取得了不错的效果
## 模型结构
![model architecture | center](data/person_reid_attention/1.png)
模型结构如上所示，由两部分组成 Global attention layer以及local deep cnn
attention通过global模型的梯度传播来实现。
m
### Global attention layer
global attention layer由两个卷积层以及全连接层，maxpooling层及softmax层组成。
将前两个卷积层的操作以符号fg(I)来表示，其中I表示图像
其实现的操作为![1](data/person_reid_attention/2.png) ![2](data/person_reid_attention/3.png)来实现
经过两层卷积，得到的结果为![3](data/person_reid_attention/4.png)
其中s1，s2表示相应的空间位置。然后得到gi,j(feature map)经过全连接层等得到一个向量输出
![5](data/person_reid_attention/5.png)
计算熵![6](data/person_reid_attention/6.png)，由熵求对应位置的梯度，将梯度作为相应的激活map
![7](data/person_reid_attention/7.png)
那么attention图像即可得到![8](data/person_reid_attention/8.png)
那么attention机制就是这样实现的，通过选取attention较高的区域，进一步输入到local deep cnn中去，提取局部特征。
![9](data/person_reid_attention/9.png)
混合特征可以如此实现
![10](data/person_reid_attention/10.png)
we are replacing the global features corresponding to the attended regions with the rich local features.
关于训练，这里面提了一下
![11](data/person_reid_attention/11.png)
