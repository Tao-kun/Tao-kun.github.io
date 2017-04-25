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