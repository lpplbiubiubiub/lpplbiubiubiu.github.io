---
title: Broad cast 描述
description: 对 Numpy的broadcast进行描述
categories: numpy
comments: true
 - 日记 积累
tags: python
---
broadcast描述了numpy是如何对待不同shape的array的数学运算的。
broadcast方便了满足一定条件的不同形状矩阵之间的操作，不再需要做额外的复制，节省了memory
一个比较简单的例子为：
```shell
>>> a = np.array([1.0, 2.0, 3.0])
>>> b = np.array([2.0, 2.0, 2.0])
>>> a * b
array([ 2.,  4.,  6.])
```
对于不同形状之间的broadcast
```shell
>>> a = np.array([1.0, 2.0, 3.0])
>>> b = 2.0
>>> a * b
array([ 2.,  4.,  6.])
```
该例子与上例得到了相同的结果。
这里面就相当于简单的broadcast
实际上numpy可以满足更加复杂的broadcast
但是需要满足相关的条件
###条件
当操作两个array时，numpy会逐维度匹配，从维度的最后开始，需要满足的条件是：
> 1. they are equal, or
> 2. one of them is 1

如果这些条件不满足，就会报错：**ValueError: frames are not aligned**
如果满足上述条件，就会输出对应维度较大的维度。
下面是个简单的例子：
```shell
Image  (3d array): 256 x 256 x 3
Scale  (1d array):             3
Result (3d array): 256 x 256 x 3
```
更加general的例子是：
```shell
A      (4d array):  8 x 1 x 6 x 1
B      (3d array):      7 x 1 x 5
Result (4d array):  8 x 7 x 6 x 5

A      (2d array):  5 x 4
B      (1d array):      1
Result (2d array):  5 x 4

A      (2d array):  5 x 4
B      (1d array):      4
Result (2d array):  5 x 4

A      (3d array):  15 x 3 x 5
B      (3d array):  15 x 1 x 5
Result (3d array):  15 x 3 x 5

A      (3d array):  15 x 3 x 5
B      (2d array):       3 x 5
Result (3d array):  15 x 3 x 5

A      (3d array):  15 x 3 x 5
B      (2d array):       3 x 1
Result (3d array):  15 x 3 x 5
```
Reference
> https://docs.scipy.org/doc/numpy-1.13.0/user/basics.broadcasting.html
