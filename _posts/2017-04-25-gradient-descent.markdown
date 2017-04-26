---
layout: post
title:  "梯度下降法 BGD、SGD、MBGD"
date:   2017-04-25 13:43:00 +0800
tags: [Machine Learning, Algorithm, Mathematics]
---
梯度下降法的计算过程就是沿梯度下降的方向求解极小值，重复地计算梯度然后对参数进行更新，这一过程称为梯度下降。


假设线性回归函数为：

$$h_{\theta}=\sum_{j=0}^{n}\theta_{j}x_{j}=\theta^Tx$$

其损失函数为：

$$J_{train}(\theta)=\frac{1}{2m}\sum_{i=1}^{m}(h_{\theta}(x^{(i)})-y^{(i)})^{2}$$

某二维参数组（$$\theta_{0}$$ 和 $$\theta_{1}$$）对应损失函数可视化图为：
![pic_001]({{"/assets/images/gradient-descent-pic001.png" | site.baseurl }})

## 批量梯度下降法（Batch Gradient Descent，BGD）
梯度下降的最原始的形式，数学形式如下：

（1）对损失函数求偏导

$$\frac{\partial J(\theta)}{\partial \theta_j} \\
=\frac{\partial}{\partial \theta_j} \frac{1}{2m} (h_{\theta}(x^{(i)})-y^{(i)})^2 \\
=2\dot\frac{1}{2m}(h_{\theta}(x{(i)})-y{(i)})\dot\frac{\partial}{\partial \theta_j}(h_{\theta}(x^{(i)})-y^{(i)}) \\
=\frac{1}{m}(h_{\theta}(x^{(i)})-y^{(i)})\dot\frac{\partial}{\partial \theta_j}(\sum_{j=0}^n\theta_jx_j^{(i)}-y^{(i)}) \\
=-\frac{1}{m}\sum_{i=1}^{m}(y^{(i)}-h_{\theta}(x^{(i)}))x_j^{(i)}$$

（2）按照每个参数$$\theta$$的梯度负方向更新每个参数$$\theta$$

$$\theta_j':=\theta_j+\frac{1}{m}\sum_{i=1}^{m}(y^i-h_{\theta}(x^i))x_j^i$$

最终得到的是一个全局最优解，但是每迭代一步，都要用到训练集所有的数据，如果样本数目很大，那么这种方法的迭代速度会很慢

优点：全局最优解；易于并行实现；

缺点：样本数目过多，训练过程会很慢。

从迭代的次数上来看，BGD迭代的次数相对较少。其迭代的收敛曲线示意图可以表示如下：

![pic_002]({{"/assets/images/gradient-descent-pic002.png" | site.baseurl }})


## 随机梯度下降法（Stochastic Gradient Descent，SGD）
解决BGD在大规模下速度减慢的问题，数学形式如下：

（1）损失函数表示为

$$
 \begin{equation}\begin{split}
 J(\theta)
 =\frac{1}{m}\sum_{i=1}^{m}\frac{1}{2}(y^i-h_{\theta}(x^i))^2 \\
 =\frac{1}{m}\sum_{i=1}^{m}cost(\theta,(x^i,y^i))
 \end{split}\end{equation} \\
 cost(\theta,(x^i,y^i))=\frac{1}{2}(y^i-h_{\theta}(x^i))^2
$$

（2）利用每个样本的损失函数对$$\theta$$求骗到得到对应梯度来更新$$\theta$$

$$\theta_j':=\theta_j+(y^i-h_{\theta}(x^i))x_j^i$$

随机梯度下降是通过每个样本来迭代更新一次，如果样本量很大的情况（例如几十万），那么可能只用其中几万条或者几千条的样本，就已经将$$\theta$$迭代到最优解了，对比上面的批量梯度下降，迭代一次需要用到十几万训练样本，一次迭代不可能最优，如果迭代10次的话就需要遍历训练样本10次。但是，SGD伴随的一个问题是噪音较BGD要多，使得SGD并不是每次迭代都向着整体最优化方向。

优点：训练速度快；

缺点：准确度下降，不是全局最优；不易并行实现。

从迭代的次数上来看，SGD迭代的次数较多，在解空间的搜索过程看起来很盲目。其迭代的收敛曲线示意图可以表示如下：

![pic_003]({{"/assets/images/gradient-descent-pic003.png" | site.baseurl }})

## 小批量梯度下降法（Mini-atch Gradient Descent，MBGD）
MBGD是BGD和SGD的折衷，MBGD在每次更新参数时使用b个样本，迭代公式为：

$$\theta_j':=\theta_j-\alpha\frac{1}{b}\sum_{k=i}^{i+9}(h_{\theta}(x^{(k)})-y^{(k)})x_j^{(k)}$$

其中，$$\alpha$$表示_学习率_(_Learning Rate_)

## 总结
　　Batch gradient descent: Use all examples in each iteration；

　　Stochastic gradient descent: Use 1 example in each iteration；

　　Mini-batch gradient descent: Use b examples in each iteration.
## 参考

[[Machine Learning] 梯度下降法的三种形式BGD、SGD以及MBGD](http://www.cnblogs.com/maybe2030/p/5089753.html)

[An overview of gradient descent optimization algorithms](http://sebastianruder.com/optimizing-gradient-descent/)

[An overview of gradient descent optimization algorithms(arXiv)](https://arxiv.org/abs/1609.04747)