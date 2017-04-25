---
layout: post
title:  "梯度下降法 BGD、SGD、MBGD"
date:   2017-04-25 13:43:00 +0800
tags: [machine learning]
---

假设线性回归函数为：

$$h_{\theta}=\sum_{j=0}^{n}\theta_{j}x_{j}$$

其损失函数为：

$$J_{train}(\theta)=\frac{1}{2m}\sum_{i=1}^{m}(h_{\theta}(x^{(i)})-y^{(i)})^{2}$$

某二维参数组（$$\theta_{0}$$ 和 $$\theta_{1}$$）对应损失函数可视化图为：
![pic_001]({{"/assets/images/gradient-descent-pic001.png" | site.baseurl }})

## 批量梯度下降法（Batch Gradient Descent，BGD）
梯度下降的最原始的形式，数学形式如下

（1）对损失函数求偏导

$$\frac{\partial J(\theta)}{\partial \theta_j}=-\frac{1}{m}\sum_{i=1}^{m}(y^1-h_{\theta}(x^i))x_j^i$$

（2）按照每个参数$$\theta$$的梯度负方向更新每个$$\theta$$

$$\theta_j^`:=\theta_j+\frac{1}{m}\sun_{i=1}{m}(y^1-h_{\theta}(x^i))x_j^i$$

## 随机梯度下降法（Stochastic Gradient Descent，SGD）
## 小批量梯度下降法（Mini-atch Gradient Descent，MBGD）
## 总结
　　Batch gradient descent: Use all examples in each iteration；
　　Stochastic gradient descent: Use 1 example in each iteration；
　　Mini-batch gradient descent: Use b examples in each iteration.



[原帖](http://www.cnblogs.com/maybe2030/p/5089753.html)