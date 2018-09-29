---
layout: post
title:  "实验 Markdown + MathJax 数学公式排版"
date:   2017-04-22 12:25:02 +0800
tags: [Mathematics]
---

测试一下使用MathJax数学公式，不定期更新.

### 一元二次方程 求根公式

对于一元二次方程$ax^2+bx+c=0$，其根为

$$x_{1,2}=\frac{-b\pm\sqrt{b^2-4ac}}{2a}$$

### 二元函数的二重积分 计算公式

$$
 \begin{equation}\begin{split}
 \iint_{D}f(x,y)\mathrm{d}\sigma
 &= \int_{a}^{b}\mathrm{d} x\int_{\phi_{1}(x)}^{\phi_{2}(x)}f(x,y)\mathrm{d}y \\
 &= \int_{c}^{d}\mathrm{d}y\int_{\psi_{1}(y)}^{\psi_{2}(y)}f(x,y)\mathrm{d} x
 \end{split}\end{equation}
$$

D 是由 $x=a$、$x=b$、$y=\phi_{1}(x)$、$y=\phi_{2}(x)$ （或 $y=c$、$y=d$、$x=\psi_{1}(y)$、$x=\psi_{2}(y)$） 围成的二维平面区域

### 线性代数

The definition of linear independence:

The vectors in a subset $S=\{\vec v_1, \vec v_2, \dots, \vec v_n\}$ of a vector space _V_ are said to be linearly dependent, if there exist a finite number of distinct vectors $\vec v_1,\vec v_2,\dots,\vec v_k$ in **S** and scalars $a_1, a_2, \dots, a_k$, not all zero, such that

$$a_1\vec v_1+a_2\vec v_2+\dots+a_k\vec v_k=\vec 0$$

where $\vec 0$ denotes the zero vector.

### 极限 级数

$$\sum_{n=1}^{\infty}\frac{1}{n}=\lim_{k\to\infty}\sum_{n=1}^{k}\frac{1}{n}$$

### 排列组合
+ 因子展开（factorial expression）

$$ C(r,k) = \frac{r!}{k!(r-k)!} $$

+ 对称（symmetry）

$$ C(r,k) = C(r,r-k) $$

+ 吸收（absorption/ extraction）

$$ C(r,k) = \frac{r}{k}C(r-1,k-1) $$

+ 增加（addition/ induction）

$$ C(r,k) = C(r-1,k)+C(r-1,k-1) $$

+ 上标（upper negation）

$$ C(r,k) = (-1)^kC(k-r-1,k) $$

+ 三项式（trinomial revision）

$$ C(r,m)C(m,k) = C(r,k)C(r-k,m-k) $$

+ 二项式定理（binomial theorem）

$$ \sum_k C(r,k) x^k y^{r-k} = (x+y)^r $$

+ 平行叠加（parallel summation）

$$ \sum_{k \leq n} C(r+k,k) = C(r+n+1,n) $$

+ 上叠加（upper summation）

$$ \sum_{0 \leq k \leq n} C(k,m) = C(n+1,m+1) $$

+ 范德蒙恒等式/ 范德蒙德卷积（Vandermonde's identity/ Vandermonde convolution）

$$ \sum_k C(r,k) C(s,n-k) = C(r+s,n) $$
