---
layout: post
title:  "实验 Markdown + MathJax 数学公式排版"
date:   2017-04-22 12:25:02 +0800
categories: analysis algebra
---

### 一元二次方程 求根公式

对于一元二次方程$$ax^2+bx+c=0$$，其根为$$x_{1,2}=\frac{-b\pm\sqrt{b^2-4ac}}{2a}$$

### 二元函数的二重积分 计算公式

$$
 \iint_{D}f(x,y)\mathrm{d}\sigma \\
  = \int_{a}^{b}\mathrm{d}x\int_{\phi_{1}(x)}^{\phi_{2}(x)}f(x,y)\mathrm{d}y \\
  = \int_{c}^{d}\mathrm{d}y\int_{\psi_{1}(y)}^{\psi_{2}(y)}f(x,y)\mathrm{d}x
$$

D 是由 $$x=a$$、$$x=b$$、$$y=\phi_{1}(x)$$、$$y=\phi_{2}(x)$$ （或 $$y=c$$、$$y=d$$、$$x=\psi_{1}(y)$$、$$x=\psi_{2}(y)$$） 围成的二维平面区域

### 线性代数

The definition of linear independence:

The vectors in a subset $$S=\{\vec v_1, \vec v_2, \dots, \vec v_n\}$$ of a vector space _V_ are said to be linearly dependent, if there exist a finite number of distinct vectors $$\vec v_1,\vec v_2,\dots,\vec v_k$$ in **S** and scalars $$a_1, a_2, \dots, a_k$$, not all zero, such that

$$a_1\vec v_1+a_2\vec v_2+\dots+a_k\vec v_k=\vec 0$$

where $$\vec 0$$ denotes the zero vector.

### 极限 级数

$$\sum_{n=1}^{\infty}\frac{1}{n}=\lim_{k\to\infty}\sum_{n=1}^{k}\frac{1}{n}$$