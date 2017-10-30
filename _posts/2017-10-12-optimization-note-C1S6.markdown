---
layout: post
title:  "C1S6 - 共轭函数"
date:   2017-10-12 18:04:00 +0800
tags: [Mathematics]
---

《凸优化理论》笔记

![C1S6 Pic1][C1S6-pic1]

这一节将介绍凸优化里一个很重要的概念——共轭变换，它给我们提供了另一个研究凸函数的视角.其背后想法是，对于凸函数$f$，通过它的共轭函数(conjugate function)，即一系列和$f$相关的仿射函数来描述它.此外，当$f$是正常闭凸函数时，这种变换还是对称的，也即$f$的共轭函数的共轭函数就是它本身，这个有趣的性质会给后面的计算和分析带来便利.

扩展实值函数$f: \mathbb{R}^n \mapsto [-\infty, \infty]$的共轭函数$f^*: \mathbb{R}^n \mapsto [-\infty, \infty]$是$$\begin{align*} f^*(\boldsymbol{y}) = \sup_{\boldsymbol{x} \in \mathbb{R}^n} \{ \boldsymbol{x}^\top \boldsymbol{y} - f(\boldsymbol{x}) \}, \ \boldsymbol{y} \in \mathbb{R}^n. \end{align*}$$如右图所示，$f$的上境图的法向量为$( -\boldsymbol{y}, 1)$的支撑超平面与竖轴的交点是$-f^*(\boldsymbol{y})$.由于$f^*$是对仿射函数逐点取上确界，故由命题1.1.10知不管$f$是何形式，$f^*$都是闭凸函数.注意即使$f$是正常函数，$f^*$也不一定是正常函数，但若$f$是凸函数，那么$f^*$是正常闭凸函数当且仅当$f$是正常函数.

扩展实值函数$f: \mathbb{R}^n \mapsto [-\infty, \infty]$的二次共轭函数$f^{**}: \mathbb{R}^n \mapsto [-\infty, \infty]$是其共轭函数$f^*$的共轭函数，$$\begin{align*} f^{**}(\boldsymbol{x}) = \sup_{\boldsymbol{y} \in \mathbb{R}^n} \{ \boldsymbol{y}^\top \boldsymbol{x} - f^*(\boldsymbol{y}) \}, \ \boldsymbol{x} \in \mathbb{R}^n. \end{align*}$$

![C1S6 Pic2][C1S6-pic2]

如上图所示，对于$\forall \boldsymbol{x} \in \mathbb{R}^n$，考虑过$(\boldsymbol{x}, 0)$的垂直直线，对于$\forall \boldsymbol{y} \in dom(f^*)$，考虑$f$上境图的法向量为$( -\boldsymbol{y}, 1)$的支撑超平面，这两条直线的交点即是$(\boldsymbol{x}, \boldsymbol{y}^\top \boldsymbol{x} - f^*(\boldsymbol{y}))$，故$f^{**}$就是这个交点能达到的上确界，从图上能看到，$f^{**}$是$f$的闭凸包.

![C1S6 Pic3][C1S6-pic3]

**例1.6.1**：下面来看几个简单例子，如右图所示

$f(x) = \alpha x - \beta$，则$$\begin{align*} f^*(y) = \sup_{x \in \mathbb{R}} \{ yx - \alpha x + \beta \} = \sup_{x \in \mathbb{R}} \{ (y - \alpha) x \} + \beta = \begin{cases} \beta, & y = \alpha; \\ \infty, & y \neq \alpha.\end{cases} \end{align*}$$且$$\begin{align*} f^{**}(x) = \sup_{y \in \mathbb{R}} \{ xy - f^*(y) \} = x \alpha - f^*(\alpha) = \alpha x - \beta = f(x). \end{align*}$$
$f(x) = \vert x\vert$，则$$\begin{align*} f^*(y)  = \sup_{x \in \mathbb{R}} \{ yx - \vert x\vert \} = \begin{cases} \sup_{x \geq 0} (y - 1)x \\ \sup_{x \leq 0} (y + 1)x \end{cases} = \begin{cases} 0, & \vert y\vert \leq 1; \\ \infty, & \vert y\vert > 1. \end{cases} \end{align*}$$且$$\begin{align*} f^{**}(x) = \sup_{y \in \mathbb{R}} \{ xy - f^*(y) \} = \sup_{\vert y\vert \leq 1} \{ xy - 0 \} = \vert x\vert = f(x). \end{align*}$$
$f(x) = \frac{c}{2}x^2$，则$$\begin{align*} f^*(y) = \sup_{x \in \mathbb{R}} \{ yx - \frac{c}{2}x^2 \} = y \frac{y}{c} - \frac{c}{2} \frac{y}{c} \frac{y}{c} = \frac{y^2}{c} - \frac{y^2}{2c} = \frac{y^2}{2c}. \end{align*}$$且$$\begin{align*} f^{**}(x) = \sup_{y \in \mathbb{R}} \{ xy - f^*(y) \} = \sup_{y \in \mathbb{R}} \{ xy - \frac{y^2}{2c} \} = x (cx) - \frac{(cx)^2}{2c} = \frac{c}{2}x^2 = f(x). \end{align*}$$
命题1.6.2[共轭定理]：扩展实值函数$f: \mathbb{R}^n \mapsto [-\infty, \infty]$的共轭函数和二次共轭函数分别是$f^*$和$f^{**}$，那么

$f(\boldsymbol{x}) \geq f^{**}(\boldsymbol{x}), \forall \boldsymbol{x} \in \mathbb{R}^n$.
当$f$是凸函数时，$f$，$f^*$和$f^{**}$这三个函数中若有一个是正常函数，则其它两个也是正常函数.
若$f$是正常闭凸函数，则$f(\boldsymbol{x}) = f^{**}(\boldsymbol{x}), \forall \boldsymbol{x} \in \mathbb{R}^n$.
$f$的共轭函数与其闭凸包的共轭函数等价，若$cl(conv(f))$是正常函数，则$cl(conv(f))(\boldsymbol{x}) = f^{**}(\boldsymbol{x}), \forall \boldsymbol{x} \in \mathbb{R}^n$.

**证明**：

由共轭函数的定义易知有$$\begin{align*} f^*(\boldsymbol{y}) \geq \boldsymbol{x}^\top \boldsymbol{y} - f(\boldsymbol{x}), \end{align*}$$即$$\begin{align*} f(\boldsymbol{x}) \geq \boldsymbol{x}^\top \boldsymbol{y} - f^*(\boldsymbol{y}), \forall \boldsymbol{x}, \boldsymbol{y} \in \mathbb{R}^n. \end{align*}$$因此$$\begin{align*} f(\boldsymbol{x}) \geq \sup_{\boldsymbol{y} \in \mathbb{R}^n} \{ \boldsymbol{x}^\top \boldsymbol{y} - f^*(\boldsymbol{y}) \} = f^{**}(\boldsymbol{x}), \forall \boldsymbol{x} \in \mathbb{R}^n. \end{align*}$$
假设$f$是正常凸函数，则其上境图$epi(f)$是非空凸集且不包含垂直直线，由命题1.5.9(a)知$epi(f)$属于某个非垂直超平面对应的闭半空间，事实上，$epi(f)$只可能属于正闭半空间，即存在向量$\boldsymbol{y} \neq \boldsymbol{0}$和标量$c$满足$$\begin{align*} \boldsymbol{y}^\top \boldsymbol{x} + f(\boldsymbol{x}) \geq c, \forall \boldsymbol{x} \in \mathbb{R}^n. \end{align*}$$因此可得$$\begin{align*} f^*(- \boldsymbol{y}) = \sup_{\boldsymbol{x} \in \mathbb{R}^n} \{ - \boldsymbol{y}^\top \boldsymbol{x} - f(\boldsymbol{x}) \} \leq -c, \end{align*}$$故$f^*$不是恒取$\infty$.又$f$是正常函数，故存在$\bar{\boldsymbol{x}}$使得$f(\bar{\boldsymbol{x}})$为有限值，由于$$\begin{align*} f^*(\boldsymbol{y}) \geq \bar{\boldsymbol{x}}^\top \boldsymbol{y} - f(\bar{\boldsymbol{x}}), \forall \boldsymbol{y} \in \mathbb{R}^n, \end{align*}$$故对于$\forall \boldsymbol{y} \in \mathbb{R}^n$有$f^*(\boldsymbol{y}) > - \infty$，故$f^*$是正常函数. 
若$f^*$是正常函数(注意$f^*$必是凸函数)，由上面的证明知$f^{**}$是正常函数，故$\forall \boldsymbol{x} \in \mathbb{R}^n$有$f^{**}(\boldsymbol{x}) > - \infty$，由(a)的结论知$f(\boldsymbol{x}) \geq f^{**}(\boldsymbol{x}) > - \infty$. 另一方面，若$f$恒取$\infty$，则$f^*$恒取$-\infty$，这是不可能的，故$f$是正常函数. 
综上，当$f$是凸函数时，$f$是正常函数当且仅当$f^*$是正常函数.那么同理可得$f^*$是正常函数当且仅当$f^{**}$是正常函数，于是结论得证.
用反证法，由(1)的结论知$f(\boldsymbol{x}) \geq f^{**}(\boldsymbol{x}), \forall \boldsymbol{x} \in \mathbb{R}^n$，故$epi(f) \subseteq epi(f^{**})$，若结论不成立，则只可能存在$(\boldsymbol{x}, \gamma) \in epi(f^{**})$但是$(\boldsymbol{x}, \gamma) \not \in epi(f)$.由于$f$是正常闭凸函数，其上境图$epi(f)$是闭凸集且不包含垂直直线，由命题1.5.9(b)知存在非垂直超平面严格分离$(\boldsymbol{x}, \gamma)$和$epi(f)$，即存在向量$(\boldsymbol{y}, \zeta), \zeta \neq 0$和标量$c$满足$$\begin{align*} \boldsymbol{y}^\top \boldsymbol{z} + \zeta w < c < \boldsymbol{y}^\top \boldsymbol{x} + \zeta \gamma, \forall (\boldsymbol{z}, w) \in epi(f). \end{align*}$$由于$w$可以任意的大，故$\zeta < 0$，不妨设$\zeta = -1$，否则可将$\boldsymbol{y}$和$\zeta$同除以$\vert\zeta\vert$即可，于是$$\begin{align*} \boldsymbol{y}^\top \boldsymbol{z} - w < c < \boldsymbol{y}^\top \boldsymbol{x} - \gamma, \forall (\boldsymbol{z}, w) \in epi(f). \end{align*}$$由于$\gamma \geq f^{**}(\boldsymbol{x})$，$(\boldsymbol{z}, f(\boldsymbol{z})) \in epi(f)$，故$$\begin{align*} \boldsymbol{y}^\top \boldsymbol{z} - f(\boldsymbol{z}) < c < \boldsymbol{y}^\top \boldsymbol{x} - f^{**}(\boldsymbol{x}), \forall \boldsymbol{z} \in dom(f). \end{align*}$$因此$$\begin{align*} f^*(\boldsymbol{y}) = \sup_{\boldsymbol{z} \in \mathbb{R}^n} \{ \boldsymbol{y}^\top \boldsymbol{z} - f(\boldsymbol{z}) \} \leq c < \boldsymbol{y}^\top \boldsymbol{x} - f^{**}(\boldsymbol{x}).\end{align*}$$即$$\begin{align*} f^{**}(\boldsymbol{x}) < \boldsymbol{y}^\top \boldsymbol{x} - f^*(\boldsymbol{y}). \end{align*}$$矛盾，故结论成立.
设$cl(conv(f))(\boldsymbol{x})$的共轭函数为$\check{f}^*$，那么对于任意$\boldsymbol{y}$，$-f^*(\boldsymbol{y})$和$-\check{f}^*(\boldsymbol{y})$分别是法向量为$-\boldsymbol{y},1$且对应闭半空间包含$epi(f)$和$cl(conv(epi(f)))$的超平面与竖轴的交点能达到的上确界，由于对于这两个集合，这样的超平面完全相同，故$f^*(\boldsymbol{y}) = \check{f}^*(\boldsymbol{y}), \forall \boldsymbol{y}$.由(c) 知，若$cl(conv(f))(\boldsymbol{x})$是正常函数，则$$\begin{align*} cl(conv(f))(\boldsymbol{x}) = (\check{f}^*(\boldsymbol{x}))^* = (f^*(\boldsymbol{x}))^* = f^{**}(\boldsymbol{x}). \end{align*}$$
(3)和(4)中要求$f$和$cl(conv(f))(\boldsymbol{x})$是正常函数是必须的,考虑如下闭凸非正常函数$$\begin{align*} f(x) = \begin{cases} \infty & x \geq 0, \\ -\infty & x < 0. \end{cases} \end{align*}$$易知有$f = \check{cl}(f)$，且$f^*(y) = \infty$，$f^{**} = -\infty$，而此时$f \neq f^{**}$，$cl(conv(f)) \neq f^{**}$.

例1.6.3[示性函数和支撑函数]：给定非空集合$X$，其示性函数(indicator function)为$$\begin{align*} \delta_X(\boldsymbol{x}) = \begin{cases} 0 & x \in X, \\ \infty & x \not \in X. \end{cases} \end{align*}$$示性函数的共轭函数$$\begin{align*} \sigma_X(\boldsymbol{y}) = \sup_{\boldsymbol{x} \in X} \boldsymbol{y}^\top \boldsymbol{x}, \end{align*}$$称为$X$的支撑函数(support function).由共轭函数的闭凸性知支撑函数是闭凸的，又由$X$是非空集合知示性函数是正常函数，故由共轭定理(b)知支撑函数也是正常函数，综上，支撑函数是正常闭凸函数.

![C1S6 Pic4][C1S6-pic4]

易知$X$的示性函数的闭包是$X$的闭包的示性函数，$X$的示性函数的凸包是$X$的凸包的示性函数，$X$的示性函数的闭凸包是$X$的闭凸包的示性函数，即$$\begin{align*} cl(\delta_X(\boldsymbol{x})) & = \delta_{cl(X)}(\boldsymbol{x}). \\ conv(\delta_X(\boldsymbol{x})) & = \delta_{conv(X)}(\boldsymbol{x}). \\ cl(conv(\delta_X(\boldsymbol{x}))) & = \delta_{cl(conv(X))}(\boldsymbol{x}). \end{align*}$$由共轭定理(d)知$cl(\delta_X(\boldsymbol{x}))$、$conv(\delta_X(\boldsymbol{x}))$、$cl(conv(\delta_X(\boldsymbol{x})))$和$\delta_X(\boldsymbol{x})$的共轭函数相同，也即$cl(X)$、$conv(X)$、$cl(conv(X))$有相同的支撑函数.

支撑函数的几何示意图如右图所示，对于给定非空集合$X$和向量$\boldsymbol{y}$，将$X$投影到$\boldsymbol{y}$上，设$y$方向的极点为$\hat{\boldsymbol{x}}$，那么

$$
\begin{align*}
\sigma_X(\boldsymbol{y})
= \vert \hat {\boldsymbol{x}} \vert \cdot \vert \boldsymbol{y} \vert
\end{align*}
$$

例1.6.4[极锥]：设$C$为凸锥，由例1.6.3知$$\begin{align*} \sigma_C(\boldsymbol{y}) = \sup_{\boldsymbol{x} \in C} \boldsymbol{y}^\top \boldsymbol{x} = \begin{cases} 0 & \boldsymbol{y}^\top \boldsymbol{x} \leq 0, \forall \boldsymbol{x} \in C, \\ \infty & otherwise. \end{cases} \end{align*}$$故$\sigma_C(\boldsymbol{y})$是$C$的极锥(polar cone)$$\begin{align*} C^* = \{ \boldsymbol{y}  \vert  \boldsymbol{y}^\top \boldsymbol{x} \leq 0, \forall \boldsymbol{x} \in C \} \end{align*}$$的示性函数.又$C^*$是闭凸锥，同理可得$C^*$的支撑函数是$(C^*)^*$的示性函数.注意，$C^*$的支撑函数是$C^*$的示性函数的共轭函数，即$C$的示性函数的共轭函数的共轭函数，由共轭定理(d)知这等于$C$的示性函数的闭凸包，又$C$的示性函数的闭凸包是$C$的闭凸包的示性函数，综上，$(C^*)^*$的示性函数等于$C$的闭凸包的示性函数.注意$C$是凸锥，故$C$的闭凸包也即$C$的闭包，于是可得$(C^*)^* = cl(C)$，这是极锥定理的一个特例.

考虑一个特殊的例子，$C = cone({\boldsymbol{a}_1, \dots, \boldsymbol{a}_r})$，于是$C$可以看作正象限集合$\{ \boldsymbol{\alpha}  \vert  \boldsymbol{\alpha} \geq 0 \}$在线性变换$\sum_{j=1}^r \alpha_j \boldsymbol{a}_j$下的象，易知$C$是闭凸锥，那么易知有$(C^*)^* = C$，这就是有名的Farkas'引理.

若$C$是任意集合，除非$C$是锥，否则$C$的支撑函数将不再是示性函数，$(C^*)^* = C$也不会成立，但是若$C$是凸的，仍有$(C^*)^* = cl(cone(C))$成立，这在第二章会给出证明.

[C1S6-pic1]: {{"/assets/images/C1S6-pic1.png" | site.baseurl }}
[C1S6-pic2]: {{"/assets/images/C1S6-pic2.png" | site.baseurl }}
[C1S6-pic3]: {{"/assets/images/C1S6-pic3.png" | site.baseurl }}
[C1S6-pic4]: {{"/assets/images/C1S6-pic4.png" | site.baseurl }}
