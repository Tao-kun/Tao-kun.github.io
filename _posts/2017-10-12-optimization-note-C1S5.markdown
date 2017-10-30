---
layout: post
title:  "C1S5 - 超平面"
date:   2017-10-12 18:04:00 +0800
tags: [Mathematics]
---

《凸优化理论》笔记

$\mathbb{R}^n$中的 超平面 是将整个空间分成两个闭半空间的$n-1$维 仿射集 ，在凸优化的很多地方，包括对偶，都会涉及这个概念.例如， 闭凸集可以看成所有包含它的闭半空间的交集 ，进一步，将这个想法用到闭凸函数的上境图上，就可得到原函数的一个很重要的对偶描述：共轭函数.

![C1S5 Pic1][C1S5-pic1]

一个超平面对应如下形式的线性方程$$\begin{align*} H = \{ \boldsymbol{x} \ \vert \ \boldsymbol{a}^\top \boldsymbol{x} = b \}, \end{align*}$$其中$\boldsymbol{a}$是一个$\mathbb{R}^n$中的非零向量，$b$是一个标量.若$\bar{\boldsymbol{x}}$是超平面上的任意向量，则$\boldsymbol{a}^\top \bar{\boldsymbol{x}} = b$，于是上式中的超平面可等价定义为$$\begin{align*} H = \{ \boldsymbol{x} \ \vert \ \boldsymbol{a}^\top \boldsymbol{x} = \boldsymbol{a}^\top \bar{\boldsymbol{x}} \}, \end{align*}$$或者$$\begin{align*} H = \bar{\boldsymbol{x}} + \{ \boldsymbol{x} \ \vert \ \boldsymbol{a}^\top \boldsymbol{x} = 0 \}, \end{align*}$$故超平面是平行于子空间$\{ \boldsymbol{x} \ \vert \ \boldsymbol{a}^\top \boldsymbol{x} = 0 \}$的仿射集，$\boldsymbol{a}$是其 法向量 (normal vector)，如右图所示.

集合$$\begin{align*} \{ \boldsymbol{a}^\top \boldsymbol{x} \geq b \}, \ \{ \boldsymbol{a}^\top \boldsymbol{x} \leq b \}, \end{align*}$$分别称为超平面对应的 正闭半空间 和 负闭半空间 ；集合$$\begin{align*} \{ \boldsymbol{a}^\top \boldsymbol{x} > b \}, \ \{ \boldsymbol{a}^\top \boldsymbol{x} < b \}, \end{align*}$$分别称为超平面对应的 正开半空间 和 负开半空间 .

对于集合$C_1$、$C_2$和超平面$H = \{ \boldsymbol{x} \ \vert \ \boldsymbol{a}^\top \boldsymbol{x} = b \}$，若$$\begin{align*} \boldsymbol{a}^\top \boldsymbol{x}_1 \leq b \leq \boldsymbol{a}^\top \boldsymbol{x}_2, \ \forall x_1 \in C_1, \forall x_2 \in C_2, \end{align*}$$或$$\begin{align*} \boldsymbol{a}^\top \boldsymbol{x}_2 \leq b \leq \boldsymbol{a}^\top \boldsymbol{x}_1, \ \forall x_1 \in C_1, \forall x_2 \in C_2, \end{align*}$$成立，则称$H$是$C_1$和$C_2$的 分离超平面 (separating hyperplane)或$H$分离$C_1$和$C_2$.一个等价的描述是存在向量$\boldsymbol{a} \neq \boldsymbol{0}$满足$$\begin{align*} \sup_{\boldsymbol{x} \in C_1} \boldsymbol{a}^\top \boldsymbol{x} \leq \inf_{\boldsymbol{x} \in C_2} \boldsymbol{a}^\top \boldsymbol{x}, \end{align*}$$如下图(a)所示.

![C1S5 Pic2][C1S5-pic2]

若$\bar{\boldsymbol{x}} \in cl(C)$，超平面$H$分离集合$C$和单点集$\{ \bar{\boldsymbol{x}} \}$，则称$H$是$C$在$\bar{\boldsymbol{x}}$处的 支撑超平面 (supporting hyperplane)，即存在向量$\boldsymbol{a} \neq \boldsymbol{0}$满足$$\begin{align*} \boldsymbol{a}^\top \bar{\boldsymbol{x}} \leq \boldsymbol{a}^\top \boldsymbol{x}, \ \forall \boldsymbol{x} \in C, \end{align*}$$或$$\begin{align*} \boldsymbol{a}^\top \bar{\boldsymbol{x}} = \inf_{\boldsymbol{x} \in C} \boldsymbol{a}^\top \boldsymbol{x}, \end{align*}$$如上图(b)所示.

下面给出一些关于超平面分离两个凸集的理论结果，这些结果保证了满足某种性质的分离超平面的存在性，在之后的章节中会多次用到这些结果.在此之前先给出一个工具：投影定理.

命题1.5.1[投影定理]：设$C$是$\mathbb{R}^n$中的非空闭凸集，向量$\boldsymbol{z} \in \mathbb{R}^n$，则存在唯一的向量$\boldsymbol{x} \in C$最小化$\\vert \boldsymbol{z} - \boldsymbol{x} \\vert$，$\boldsymbol{x}$称为$\boldsymbol{z}$在$C$上的投影，进一步的，$\boldsymbol{x}^*$称为$\boldsymbol{z}$在$C$上的投影当且仅当$$\begin{align*} (\boldsymbol{z} - \boldsymbol{x}^*)^\top (\boldsymbol{x} - \boldsymbol{x}^*) \leq 0, \ \forall \boldsymbol{x} \in C. \end{align*}$$

**证明**：一方面，对于任意$\boldsymbol{x} \in C$，由$C$的凸性知对于$\forall \alpha \in [0, 1]$有$\alpha \boldsymbol{x} + (1 - \alpha) \boldsymbol{x}^* \in C$，于是若$\boldsymbol{x}^*$是$\boldsymbol{z}$在$C$上的投影，则有$$\begin{align*} \\vert \boldsymbol{z} - \boldsymbol{x}^* \\vert^2 & \leq \\vert \boldsymbol{z} - (\alpha \boldsymbol{x} + (1 - \alpha) \boldsymbol{x}^*) \\vert^2 = \\vert \boldsymbol{z} - \boldsymbol{x}^* - \alpha (\boldsymbol{x} - \boldsymbol{x}^*)\\vert^2 \\ & = \\vert \boldsymbol{z} - \boldsymbol{x}^* \\vert^2 - 2 \alpha (\boldsymbol{z} - \boldsymbol{x}^*)^\top (\boldsymbol{x} - \boldsymbol{x}^*) + \alpha^2 \\vert\boldsymbol{x} - \boldsymbol{x}^*\\vert^2. \end{align*}$$于是$$\begin{align*} (\boldsymbol{z} - \boldsymbol{x}^*)^\top (\boldsymbol{x} - \boldsymbol{x}^*) \leq \frac{\alpha}{2} \\vert\boldsymbol{x} - \boldsymbol{x}^*\\vert^2. \end{align*}$$令$\alpha=0$可得$(\boldsymbol{z} - \boldsymbol{x}^*)^\top (\boldsymbol{x} - \boldsymbol{x}^*) \leq 0$.

另一方面，若$(\boldsymbol{z} - \boldsymbol{x}^*)^\top (\boldsymbol{x} - \boldsymbol{x}^*) \leq 0$，则对任意$\boldsymbol{x} \in C$有$$\begin{align*} \\vert \boldsymbol{z} - \boldsymbol{x} \\vert^2 = \\vert \boldsymbol{z} - \boldsymbol{x}^* - (\boldsymbol{x} - \boldsymbol{x}^*) \\vert^2 = \\vert \boldsymbol{z} - \boldsymbol{x}^* \\vert^2 - 2 (\boldsymbol{z} - \boldsymbol{x}^*)^\top (\boldsymbol{x} - \boldsymbol{x}^*) + \\vert\boldsymbol{x} - \boldsymbol{x}^*\\vert^2 \geq \\vert \boldsymbol{z} - \boldsymbol{x}^* \\vert^2, \end{align*}$$故$\boldsymbol{x}^*$是$\boldsymbol{z}$在$C$上的投影.下面证明唯一性，设$\boldsymbol{x}_1^*$和$\boldsymbol{x}_2^*$都是$\boldsymbol{z}$在$C$上的投影，则$$\begin{align*}(\boldsymbol{z} - \boldsymbol{x}_1^*)^\top (\boldsymbol{x}_2^* - \boldsymbol{x}_1^*) \leq 0, \ (\boldsymbol{z} - \boldsymbol{x}_2^*)^\top (\boldsymbol{x}_1^* - \boldsymbol{x}_2^*) \leq 0. \end{align*}$$将上面两式相加可得$$\begin{align*} (\boldsymbol{x}_2^* - \boldsymbol{x}_1^*)^\top (\boldsymbol{x}_2^* - \boldsymbol{x}_1^*) = \\vert \boldsymbol{x}_2^* - \boldsymbol{x}_1^* \\vert^2 \leq 0, \end{align*}$$故$\boldsymbol{x}_1^* = \boldsymbol{x}_2^*$.

命题1.5.2[支撑超平面定理]：设$C$是$\mathbb{R}^n$中的非空凸子集，向量$\bar{\boldsymbol{x}} \in \mathbb{R}^n$，若$\bar{\boldsymbol{x}} \not \in ri(C)$，则存在一个穿过$\bar{\boldsymbol{x}}$的超平面使得$X$属于它的一个闭半空间，即存在向量$\boldsymbol{a} \neq \boldsymbol{0}$满足$$\begin{align*} \boldsymbol{a}^\top \bar{\boldsymbol{x}} \leq \boldsymbol{a}^\top \boldsymbol{x}, \ \forall \boldsymbol{x} \in C. \end{align*}$$

![C1S5 Pic3][C1S5-pic3]

**证明**：由命题1.1.2(d)知$cl(C)$是凸集，又由命题1.3.5(b)知$\bar{\boldsymbol{x}} \not \in ri(C) = ri(cl(C))$，故存在序列$\{\boldsymbol{x}_k\}$收敛于$\bar{\boldsymbol{x}}$且对于$\forall k$有$\boldsymbol{x}_k \not \in cl(C)$.记$\bar{\boldsymbol{x}}_k$为$\boldsymbol{x}_k$在$cl(C)$上的投影，由投影定理知$$\begin{align*} (\boldsymbol{x}_k - \bar{\boldsymbol{x}}_k)^\top (\boldsymbol{x} - \bar{\boldsymbol{x}}_k) \leq 0, \ \forall \boldsymbol{x} \in cl(C). \end{align*}$$故对于$\forall \boldsymbol{x} \in cl(C)$和$\forall k$有$$\begin{align*} (\bar{\boldsymbol{x}}_k - \boldsymbol{x}_k)^\top \boldsymbol{x} \geq (\bar{\boldsymbol{x}}_k - \boldsymbol{x}_k)^\top \bar{\boldsymbol{x}}_k = (\bar{\boldsymbol{x}}_k - \boldsymbol{x}_k)^\top (\bar{\boldsymbol{x}}_k - \boldsymbol{x}_k) + (\bar{\boldsymbol{x}}_k - \boldsymbol{x}_k)^\top \boldsymbol{x}_k \geq (\bar{\boldsymbol{x}}_k - \boldsymbol{x}_k)^\top \boldsymbol{x}_k. \end{align*}$$将其简写为$$\begin{align*} \label{equ: supporting hyperplane} \boldsymbol{a}_k^\top \boldsymbol{x} \geq \boldsymbol{a}_k^\top \boldsymbol{x}_k, \ \forall \boldsymbol{x} \in cl(C), \forall k,\end{align*}$$其中$$\begin{align*} \boldsymbol{a}_k = \frac{\bar{\boldsymbol{x}}_k - \boldsymbol{x}_k}{\\vert\bar{\boldsymbol{x}}_k - \boldsymbol{x}_k\\vert}. \end{align*}$$故对$\forall k$有$\\vert \boldsymbol{a}_k \\vert = 1$，于是序列$\{\boldsymbol{a}_k\}$存在一个子序列收敛于$\boldsymbol{a} \neq \boldsymbol{0}$，令$k \rightarrow \infty$可得$$\begin{align*} \boldsymbol{a}^\top \bar{\boldsymbol{x}} \leq \boldsymbol{a}^\top \boldsymbol{x}, \ \forall \boldsymbol{x} \in C. \end{align*}$$

若$\bar{\boldsymbol{x}}$是$C$的边界点，那么命题中的超平面就是$C$在$\bar{\boldsymbol{x}}$处的支撑超平面.

命题1.5.3[分离超平面定理]：设$C_1$和$C_2$是$\mathbb{R}^n$的两个非空凸子集，若$C_1$和$C_2$不相交，则存在一个的超平面分离$C_1$和$C_2$，即存在向量$\boldsymbol{a} \neq \boldsymbol{0}$满足$$\begin{align*} \boldsymbol{a}^\top \boldsymbol{x}_1 \leq \boldsymbol{a}^\top \boldsymbol{x}_2, \ \forall \boldsymbol{x}_1 \in C_1, \forall \boldsymbol{x}_2 \in C_2. \end{align*}$$

**证明**：显然集合$$\begin{align*} C = C_2 + (- C_1) = C_2 - C_1 = \{ \boldsymbol{x} \ \vert \ \boldsymbol{x} = \boldsymbol{x}_2 - \boldsymbol{x}_1, \boldsymbol{x}_1 \in C_1, \boldsymbol{x}_2 \in C_2 \} \end{align*}$$是凸集.又$C_1$和$C_2$不相交，故原点不属于$C$，由命题1.5.2知存在向量$\boldsymbol{a} \neq \boldsymbol{0}$满足$$\begin{align*} 0 = \boldsymbol{a}^\top \boldsymbol{0} \leq \boldsymbol{a}^\top \boldsymbol{x} = \boldsymbol{a}^\top (\boldsymbol{x}_2 - \boldsymbol{x}_1), \ \forall \boldsymbol{x}_1 \in C_1, \forall \boldsymbol{x}_2 \in C_2, \end{align*}$$即$$\begin{align*} \boldsymbol{a}^\top \boldsymbol{x}_1 \leq \boldsymbol{a}^\top \boldsymbol{x}_2, \ \forall \boldsymbol{x}_1 \in C_1, \forall \boldsymbol{x}_2 \in C_2. \end{align*}$$

下面考虑分离超平面定理更强的形式.

对于集合$C_1$、$C_2$和超平面$H = \{ \boldsymbol{x} \ \vert \ \boldsymbol{a}^\top \boldsymbol{x} = b \}$，若$$\begin{align*} \boldsymbol{a}^\top \boldsymbol{x}_1 < b < \boldsymbol{a}^\top \boldsymbol{x}_2, \ \forall \boldsymbol{x}_1 \in C_1, \forall \boldsymbol{x}_2 \in C_2, \end{align*}$$或$$\begin{align*} \boldsymbol{a}^\top \boldsymbol{x}_2 < b < \boldsymbol{a}^\top \boldsymbol{x}_1, \ \forall \boldsymbol{x}_1 \in C_1, \forall \boldsymbol{x}_2 \in C_2, \end{align*}$$成立，则称$H$是$C_1$和$C_2$的严格分离超平面或$H$严格分离$C_1$和$C_2$.

![C1S5 Pic4][C1S5-pic4]

命题1.5.4[严格分离超平面定理]：设$C_1$和$C_2$是$\mathbb{R}^n$的两个非空凸子集，若$C_1$和$C_2$不相交，则当下面5个条件之一满足时，存在一个的超平面严格分离$C_1$和$C_2$，

$C_2 - C_1$是闭集.
$C_1$是闭集，$C_2$是紧集.
$C_1$和$C_2$都是多面体.
$C_1$和$C_2$都是闭集，且$R_{C_1} \cap R_{C_2} = L_{C_1} \cap L_{C_2}$.
$C_1$是闭集，$C_2$是多面体，且$R_{C_1} \cap R_{C_2} \subseteq L_{C_1}$.
**证明**：由命题1.4.21之后的讨论知条件2345均可推出条件1，故下面只考虑条件1.

考虑集合$C_2 - C_1$中范数最小的向量(原点在$C_2 - C_1$上的投影)，设其为$\bar{\boldsymbol{x}}_2 - \bar{\boldsymbol{x}}_1$，其中$\bar{\boldsymbol{x}}_1 \in C_1$，$\bar{\boldsymbol{x}}_2 \in C_2$.令$$\begin{align*} \boldsymbol{a} = \frac{\bar{\boldsymbol{x}}_2 - \bar{\boldsymbol{x}}_1}{2}, \ \bar{\boldsymbol{x}} = \frac{\bar{\boldsymbol{x}}_1 + \bar{\boldsymbol{x}}_2}{2}, \ b = \boldsymbol{a}^\top \bar{\boldsymbol{x}}, \end{align*}$$如上图(b)所示.由于$C_1$和$C_2$不相交，故$\boldsymbol{a} \neq \boldsymbol{0}$，下面证明超平面$H = \{ \boldsymbol{x} \ \vert \ \boldsymbol{a}^\top \boldsymbol{x} = b \}$严格分离$C_1$和$C_2$，即

$$
\begin{align*}
\boldsymbol{a}^\top \boldsymbol{x}_1 < b < \boldsymbol{a}^\top \boldsymbol{x}_2, 
\forall \boldsymbol{x}_1 \in C_1, 
\forall \boldsymbol{x}_2 \in C_2.
\end{align*}
$$

由于$\bar{\boldsymbol{x}}_2 - \bar{\boldsymbol{x}}_1$是$C_2 - C_1$中范数最小的向量，故$\bar{\boldsymbol{x}}_1$是$\bar{\boldsymbol{x}}_2$在$cl(C_1)$上的投影，由投影定理知$$\begin{align*} (\bar{\boldsymbol{x}}_2 - \bar{\boldsymbol{x}}_1)^\top (\boldsymbol{x}_1 - \bar{\boldsymbol{x}}_1) \leq 0, \ \forall \boldsymbol{x}_1 \in C_1, \end{align*}$$注意$\bar{\boldsymbol{x}} - \bar{\boldsymbol{x}}_1 = \boldsymbol{a}$，于是$$\begin{align*} \boldsymbol{a}^\top \boldsymbol{x}_1 \leq \boldsymbol{a}^\top \bar{\boldsymbol{x}}_1 = \boldsymbol{a}^\top \bar{\boldsymbol{x}} + \boldsymbol{a}^\top (\bar{\boldsymbol{x}}_1 - \bar{\boldsymbol{x}}) = b - \\vert \boldsymbol{a} \\vert^2 < b, \ \forall \boldsymbol{x}_1 \in C_1. \end{align*}$$同理，由于$\bar{\boldsymbol{x}}_2$是$\bar{\boldsymbol{x}}_1$在$cl(C_2)$上的投影，由投影定理知$$\begin{align*} (\bar{\boldsymbol{x}}_1 - \bar{\boldsymbol{x}}_2)^\top (\boldsymbol{x}_2 - \bar{\boldsymbol{x}}_2) \leq 0, \ \forall \boldsymbol{x}_2 \in C_2, \end{align*}$$注意$\bar{\boldsymbol{x}}_2 - \bar{\boldsymbol{x}} = \boldsymbol{a}$，于是$$\begin{align*} \boldsymbol{a}^\top \boldsymbol{x}_2 \geq \boldsymbol{a}^\top \bar{\boldsymbol{x}}_2 = \boldsymbol{a}^\top \bar{\boldsymbol{x}} + \boldsymbol{a}^\top (\bar{\boldsymbol{x}}_2 - \bar{\boldsymbol{x}}) = b + \\vert \boldsymbol{a} \\vert^2 > b, \ \forall \boldsymbol{x}_2 \in C_2. \end{align*}$$

由此可知，若向量$\boldsymbol{x}$不属于闭凸集$C$，那么必然存在一个超平面严格分离$\boldsymbol{x}$和$C$，基于这点，我们可以得出如下推论.

**命题1.5.5**：集合$C$的闭凸包是所有包含$C$的闭半空间的交集，特别地，闭凸集合$C$是所有包含$C$的闭半空间的交集.

**证明**：一方面，设$H$是所有包含$C$的闭半平面的交集，由于$H$是闭凸集，故$cl(conv(C)) \subseteq H$.

另一方面，设向量$\boldsymbol{x} \not \in cl(conv(C))$，那么存在一个超平面严格分离$\boldsymbol{x}$和$cl(conv(C))$，于是其对应的闭半空间包含$cl(conv(C))$而不包含$\boldsymbol{x}$，这意味着$\boldsymbol{x} \not \in H$，故$H \subseteq cl(conv(C))$.

  对于集合$C_1$、$C_2$和超平面$H = \{ \boldsymbol{x} \ \vert \ \boldsymbol{a}^\top \boldsymbol{x} = b \}$，若$$\begin{align*} \sup_{\boldsymbol{x}_1 \in C_1} \boldsymbol{a}^\top \boldsymbol{x}_1 \leq \inf_{\boldsymbol{x}_2 \in C_2} \boldsymbol{a}^\top \boldsymbol{x}_2, \ \inf_{\boldsymbol{x}_1 \in C_1} \boldsymbol{a}^\top \boldsymbol{x}_1 < \sup_{\boldsymbol{x}_2 \in C_2} \boldsymbol{a}^\top \boldsymbol{x}_2. \end{align*}$$或$$\begin{align*} \boldsymbol{a}^\top \boldsymbol{x}_2 < b < \boldsymbol{a}^\top \boldsymbol{x}_1, \ \forall \boldsymbol{x}_1 \in C_1, \forall \boldsymbol{x}_2 \in C_2, \end{align*}$$成立，则称$H$是$C_1$和$C_2$的正常分离超平面或$H$正常分离$C_1$和$C_2$.

直观地讲，$H$正常分离$C_1$和$C_2$意味着$H$不能同时包含$C_1$和$C_2$，如下图所示.注意若$\mathbb{R}^n$中的凸集内部非空，则其维度为$n$，显然是不可能被某个超平面包含的，于是两个不相交的凸集，若其中一个内部非空，那么它们可以被正常分离.进一步，若两个凸集的并的仿射包的维度是$n$，那么它们可以被正常分离.

![C1S5 Pic5][C1S5-pic5]

正常分离超平面的存在性是和集合相对内部紧密相关的.事实上，非空凸集$C$属于超平面$H$当且仅当$ri(C) \cap H \neq \emptyset$.设超平面$H = \{ \boldsymbol{x} \ \vert \ \boldsymbol{a}^\top \boldsymbol{x} = b \}$且对于$\forall \boldsymbol{x} \in C$有$\boldsymbol{a}^\top \boldsymbol{x} \geq b$，那么对于$\forall \bar{\boldsymbol{x}} \in ri(C)$，$\bar{\boldsymbol{x}} \in H$当且仅当$\boldsymbol{a}^\top \bar{\boldsymbol{x}} = b$，这意味着$\boldsymbol{a}^\top \boldsymbol{x}$在$C$上的最小值在$\bar{\boldsymbol{x}}$处取得，由命题1.3.4知对于$\forall \boldsymbol{x} \in C$有$\boldsymbol{a}^\top \boldsymbol{x} = b$，故$C \subseteq H$.

下面的三个命题对应了如下三种情况下：单个向量和非空凸集、两个非空凸集、凸集和多面体的正常分离超平面存在的条件.

**命题1.5.6**：集合$C$是$\mathbb{R}^n$的非空凸子集，$\bar{\boldsymbol{x}} \in \mathbb{R}^n$，那么存在超平面正常分离$C$和$\bar{\boldsymbol{x}}$当且仅当$\bar{\boldsymbol{x}} \not \in ri(C)$.

**证明**：一方面，若存在超平面$H$正常分离$C$和$\bar{\boldsymbol{x}}$，那么要么$\bar{\boldsymbol{x}} \not \in H$，这意味着$\bar{\boldsymbol{x}} \not \in C \Rightarrow \bar{\boldsymbol{x}} \not \in ri(C)$；要么$\bar{\boldsymbol{x}} \in H$但是$H$不包含$C$，故此时有$ri(C) \cap H = \emptyset$，这意味着$\bar{\boldsymbol{x}} \not \in ri(C)$.

另一方面，若$\bar{\boldsymbol{x}} \not \in ri(C)$，只需考虑如下两种情况：

$\bar{\boldsymbol{x}} \not \in aff(C)$，由于$aff(C)$是闭凸集，单点集是紧凸集，由命题1.5.4(b)知存在超平面严格分离$\{\bar{\boldsymbol{x}}\}$和$aff(C)$，那么该超平面正常分离$\{\bar{\boldsymbol{x}}\}$和$C$.
$\bar{\boldsymbol{x}} \in aff(C)$，设$S$是平行于$aff(C)$的子空间，考虑集合$\hat{C} = C + S^\perp$，由命题1.3.7(b)知$ri(\hat{C}) = ri(C) + ri(S^\perp) = ri(C) + S^\perp$，于是$\bar{\boldsymbol{x}} \not \in ri(\hat{C})$(否则存在$\boldsymbol{x} \in ri(C)$使得$\bar{\boldsymbol{x}} - \boldsymbol{x} \in S^\perp$，又$\bar{\boldsymbol{x}} \in aff(C)$，$\boldsymbol{x} \in ri(C) \subseteq aff(C)$，故$\bar{\boldsymbol{x}} - \boldsymbol{x} \in S$，于是$\bar{\boldsymbol{x}} - \boldsymbol{x} \in \boldsymbol{0}$，这意味着$\bar{\boldsymbol{x}} = \boldsymbol{x} \in ri(C)$，矛盾)，由命题1.5.2知存在向量$\boldsymbol{a} \neq \boldsymbol{0}$满足对于$\forall \boldsymbol{x} \in \hat{C}$有$\boldsymbol{a}^\top \boldsymbol{x} \geq \boldsymbol{a}^\top \bar{\boldsymbol{x}}$.由于$\hat{C}$内部非空，$\boldsymbol{a}^\top \boldsymbol{x}$不可能包含$\hat{C}$，故$$\begin{align*} \boldsymbol{a}^\top \bar{\boldsymbol{x}} < \sup_{\boldsymbol{x} \in \hat{C}} \boldsymbol{a}^\top \boldsymbol{x} = \sup_{\boldsymbol{x} \in C, \boldsymbol{z} \in S^\perp} \boldsymbol{a}^\top (\boldsymbol{x} + \boldsymbol{z}) = \sup_{\boldsymbol{x} \in C} \boldsymbol{a}^\top \boldsymbol{x} + \sup_{\boldsymbol{z} \in S^\perp} \boldsymbol{a}^\top \boldsymbol{z}. \end{align*}$$若对于某个$\bar{\boldsymbol{z}} \in S^\perp$使得$\boldsymbol{a}^\top \bar{\boldsymbol{z}} \neq 0$，那么$$\begin{align*} \inf_{\alpha \in \mathbb{R}} \boldsymbol{a}^\top (\boldsymbol{x} + \alpha \bar{\boldsymbol{z}}) = - \infty, \end{align*}$$这与对于$\forall \boldsymbol{x} \in C$和$\forall \boldsymbol{z} \in S^\perp$有$\boldsymbol{a}^\top (\boldsymbol{x} + \boldsymbol{z}) \geq \boldsymbol{a}^\top \bar{\boldsymbol{x}}$矛盾，故$$\begin{align*} \boldsymbol{a}^\top \boldsymbol{z} = 0, \ \forall \boldsymbol{z} \in S^\perp, \end{align*}$$于是$$\begin{align*} \boldsymbol{a}^\top \bar{\boldsymbol{x}} < \sup_{\boldsymbol{x} \in C} \boldsymbol{a}^\top \boldsymbol{x}, \end{align*}$$故超平面$\{ \boldsymbol{x} \ \vert \ \boldsymbol{a}^\top \boldsymbol{x} = \boldsymbol{a}^\top \bar{\boldsymbol{x}} \}$正常分离$\{\bar{\boldsymbol{x}}\}$和$C$.

**命题1.5.7**：集合$C_1$和$C_2$是$\mathbb{R}^n$的非空凸子集，那么存在超平面正常分离$C_1$和$C_2$当且仅当$ri(C_1) \cap ri(C_2) = \emptyset$.

**证明**：考虑集合$C = C_2 - C_1$，显然是$C$是凸集，由命题1.3.7(b)知$$\begin{align*} ri(C) = ri(C_2) - ri(C_1), \end{align*}$$于是$ri(C_1) \cap ri(C_2) = \emptyset \Leftrightarrow \boldsymbol{0} \not \in ri(C)$，由命题1.5.6知存在超平面正常分离$C$和$\boldsymbol{0}$，故$$\begin{align*} 0 \leq \inf_{\boldsymbol{x}_1 \in C_1, \boldsymbol{x}_2 \in C_2} \boldsymbol{a}^\top (\boldsymbol{x}_2 - \boldsymbol{x}_1), \ 0 < \sup_{\boldsymbol{x}_1 \in C_1, \boldsymbol{x}_2 \in C_2} \boldsymbol{a}^\top (\boldsymbol{x}_2 - \boldsymbol{x}_1), \end{align*}$$这等价于$$\begin{align*} \sup_{\boldsymbol{x}_1 \in C_1} \boldsymbol{a}^\top \boldsymbol{x}_1 \leq \inf_{\boldsymbol{x}_2 \in C_2} \boldsymbol{a}^\top \boldsymbol{x}_2, \ \inf_{\boldsymbol{x}_1 \in C_1} \boldsymbol{a}^\top \boldsymbol{x}_1 < \sup_{\boldsymbol{x}_2 \in C_2} \boldsymbol{a}^\top \boldsymbol{x}_2, \end{align*}$$故存在超平面正常分离$C_1$和$C_2$.

![C1S5 Pic6][C1S5-pic6]

**命题1.5.8**：集合$C$和$P$是$\mathbb{R}^n$的非空凸子集且$P$是多面体，那么存在超平面正常分离$C$和$P$且不包含$C$当且仅当$ri(C) \cap P = \emptyset$.

**证明**：一方面，若存在超平面$H$正常分离$C$和$P$且不包含$C$，由$C \not \subseteq H \Leftrightarrow ri(C) \cap H = \emptyset$知$ri(C) \cap P = \emptyset$.

另一方面，若$ri(C) \cap P = \emptyset$，记$D = P \cap aff(C)$，若$D = \emptyset$，又$aff(C)$和$P$都是多面体，由命题1.5.4(c)知存在超平面严格分离$aff(C)$和$P$，显然该超平面正常分离$C$和$P$且不包含$C$.故不妨设$D \neq \emptyset$，证明思路是分两步，先构造一个超平面正常分离$C$和$D$，以此为基础再构造一个超平面正常分离$C$和$P$(若$C$内部非空，则$aff(C) = \mathbb{R}^n$，故$D = P$，此时只需第一步就行了).

易知有$$\begin{align*} ri(C) \cap ri(D) \subseteq ri(C) \cap (P \cap aff(C)) = (ri(C) \cap P) \cap aff(C) = \emptyset \cap aff(C) = \emptyset, \end{align*}$$由命题1.5.7知存在超平面$H$正常分离$C$和$D$，且进一步的，$H$不包含$C$，否则$H$将包含$aff(C)$，从而包含$D$，这与$H$正常分离$C$和$D$矛盾，因此$C$属于$H$对应的两个闭半空间中的一个.记$\bar{C}$为$aff(C)$与$H$对应的包含$C$的闭半空间的交集，由于$H$不包含$C$，故$H$不包含$aff(C)$，从而不包含$\bar{C}$，由$\bar{C} \not \subseteq H \Leftrightarrow ri(\bar{C}) \cap H = \emptyset$知$$\begin{align*} P \cap ri(\bar{C}) = \emptyset. \end{align*}$$

若$P \cap \bar{C} = \emptyset$，由于$\bar{C}$多面体的交集，故$\bar{C}$也是多面体(事实上，$\bar{C}$还是一个闭半空间)，由命题1.5.4(c) 知存在超平面严格分离$P$和$\bar{C}$，显然该超平面正常分离$C$和$P$且不包含$C$.不妨设$P \cap \bar{C} \neq \emptyset$，进一步的，不妨设$\boldsymbol{0} \in P \cap \bar{C}$，否则经过适当的平移即可，那么此时超平面$H$是一个子空间，$aff(C)$也是一个子空间.多面体$P$是闭半平面$\{ \boldsymbol{x} \ \vert \ \boldsymbol{a}_j^\top \boldsymbol{x} \leq b_j, b_j \geq 0 \}$的交集，其中$b_j \geq 0$是由于$\boldsymbol{0} \in P$，又$\boldsymbol{0}$是$P$的边界点，故至少有一个$j$满足$b_j = 0$，于是$P$可表示为$$\begin{align*} P = \{ \boldsymbol{x} \ \vert \ \boldsymbol{a}_j^\top \boldsymbol{x} \leq 0, j = 1, \dots, m \} \cap \{ \boldsymbol{x} \ \vert \ \boldsymbol{a}_j^\top \boldsymbol{x} \leq b_j, j = m+1, \dots, \bar{m} \}, \end{align*}$$其中$m \geq 1$，$\bar{m} \geq m$，$\boldsymbol{a}_j \neq \boldsymbol{0}$，$b_j > 0$.

记$M$为$\bar{C}$的相对边界，即$$\begin{align*} M = H \cap aff(C), \end{align*}$$注意$M$是子空间的交集，故$M$也是个子空间.考虑集合$$\begin{align*} K = \{ \boldsymbol{x} \ \vert \ \boldsymbol{a}_j^\top \boldsymbol{x} \leq 0, j = 1, \dots, m \} + M, \end{align*}$$注意$K = cone(P) + M$，故$K$是个锥.下面证明$K \cap ri(\bar{C}) = \emptyset$，用反证法，设$\bar{\boldsymbol{x}} \in K \cap ri(\bar{C})$.一方面，由于$\bar{\boldsymbol{x}} \in K$， 那么$\bar{\boldsymbol{x}}$可表示为$\bar{\boldsymbol{x}} = \alpha \boldsymbol{w} + \boldsymbol{v}$，其中$\alpha > 0$，$\boldsymbol{w} \in P$，$\boldsymbol{v} \in M$，故$(\bar{\boldsymbol{x}} / \alpha) - (\boldsymbol{v} / \alpha) \in P$. 另一方面，由于$\bar{\boldsymbol{x}} \in ri(\bar{C})$，$\boldsymbol{0} \in \bar{C}$，$M$是$\bar{C}$的回收锥的线性空间的子集，从而也是$ri(\bar{C})$的回收锥的线性空间的子集，故如下形式的向量$\bar{\alpha} \bar{\boldsymbol{x}} + \bar{\boldsymbol{v}}$，其中$\bar{\alpha} > 0$，$\boldsymbol{v} \in M$，均属于$ri(\bar{C})$，那么$(\bar{\boldsymbol{x}} / \alpha) - (\boldsymbol{v} / \alpha)$也属于$ri(\bar{C})$，这与$P \cap ri(\bar{C}) = \emptyset$矛盾.

由于$K$是一个多面体，故$K$是经过$\boldsymbol{0}$的闭半空间$F_1, \dots, F_r$的交集，又$K = cone(P) + M$，故每一个闭半空间都包含$M$，如果某个闭半空间包含$ri(\bar{C})$中的某个向量，则将包含$ri(\bar{C})$，又$K \cap ri(\bar{C}) = \emptyset$，故$F_1, \dots, F_r$中至少有一个闭半空间不包含$ri(\bar{C})$中的任意向量，不妨设为$F_1$，那么$F_1$不包含$ri(C)$中的任意向量，于是该超平面正常分离$K$和$C$且不包含$C$，又$K$包含$P$，故该超平面正常分离$P$和$C$且不包含$C$.

证明中$M$的引入是必需的，若定义$K = cone(P)$，则对应的闭半空间$F_1, \dots, F_r$可能都与$ri(\bar{C})$有交集，则证明就无法完成了.

在优化领域中，支撑超平面和$\mathbb{R}^n$中函数的上境图有很大关系，由于$\mathbb{R}^n$中函数的上境图是$\mathbb{R}^{n+1}$的子集，故这里考虑$\mathbb{R}^{n+1}$中的超平面，易知每个这样的超平面都对应着的一个法向量$(\boldsymbol{\mu}, \beta)$，其中$\boldsymbol{\mu} \in \mathbb{R}^n$，$\beta \in \mathbb{R}$，若$\beta = 0$，则超平面是垂直的.

![C1S5 Pic7][C1S5-pic7]

如右图所示，若超平面是非垂直的，则其必与$n+1$轴交于唯一的一点.若$(\bar{\boldsymbol{u}}, \bar{w})$是超平面上一点，由于超平面与$n+1$轴的交点是$(\boldsymbol{0} , \xi)$也是超平面上的一点，故有$\bar{\boldsymbol{u}}^\top \bar{\boldsymbol{\mu}} + \beta \bar{w} = \boldsymbol{\mu}^\top \boldsymbol{0} + \beta \xi$，于是$$\begin{align*} \xi = \frac{1}{\beta} \bar{\boldsymbol{u}}^\top \bar{\boldsymbol{\mu}} + \bar{w}. \end{align*}$$若超平面是垂直的，则其要么与$n+1$轴无交点，要么包含整个$n+1$轴.进一步，超平面$H$垂直当且仅当$H$和其对应的闭半空间的回收锥都包含$n+1$轴.

命题1.5.9[非垂直超平面分离定理]：集合$C$是$\mathbb{R}^{n+1}$的非空凸子集且不包含垂直直线，将$\mathbb{R}^{n+1}$中的任意向量都表示成如下形式$(\bar{\boldsymbol{u}}, w)$，其中$\bar{\boldsymbol{u}} \in \mathbb{R}^n$，$w \in \mathbb{R}$，那么

$C$属于某个非垂直超平面对应的闭半空间，即存在$\boldsymbol{\mu} \in \mathbb{R}^n$，标量$\beta \neq 0$和标量$\gamma$满足$$\begin{align*} \boldsymbol{\mu}^\top \boldsymbol{u} + \beta w \geq \gamma, \ \forall (\boldsymbol{u}, w) \in C. \end{align*}$$
若$(\bar{\boldsymbol{u}}, \bar{w}) \not \in cl(C)$，那么存在非垂直超平面严格分离$(\bar{\boldsymbol{u}}, \bar{w})$和$C$.
**证明**：

用反证法，假设所有包含$C$的闭半空间对应的超平面都是垂直的，那么所有包含$cl(C)$的闭半空间对应的超平面也都是垂直的，故其回收锥都包含$n+1$轴.由命题1.5.5知$cl(C)$是所有包含$cl(C)$的闭半空间的交集，故$cl(C)$的回收锥也包含$n+1$轴，由命题1.4.3(b)知$R_{cl(C)} = R_{ri(C)}$，故$ri(C)$的回收锥也包含$n+1$轴，于是对于任意$( \bar{\boldsymbol{u}}, \bar{w}) \in ri(C)$，垂直直线$\{ (\bar{\boldsymbol{u}}, w) \ \vert \ w \in \mathbb{R} \} \subseteq ri(C) \subseteq C$，这与$C$不包含垂直直线矛盾.
若$(\bar{\boldsymbol{u}}, \bar{w}) \not \in cl(C)$，那么由命题1.5.4(b)知存在超平面严格分离$(\bar{\boldsymbol{u}}, \bar{w})$和$cl(C)$，若该超平面是非垂直的，由于$C \subseteq cl(C)$，结论已证.故不妨设该超平面是垂直的，则其法向量为$(\bar{\boldsymbol{\mu}}, 0)$，于是存在标量$\bar{\gamma}$满足

$$\begin{align}
\label{equ: nonvertical hyperplane} \bar{\boldsymbol{\mu}}^\top \boldsymbol{u} > \bar{\gamma} > \bar{\boldsymbol{\mu}}^\top \bar{\boldsymbol{u}}, \ \forall (\boldsymbol{u}, w) \in cl(C).
\end{align}$$

由(a)知$$\begin{align*} \boldsymbol{\mu}^\top \boldsymbol{u} + \beta w \geq \gamma, \ \forall (\boldsymbol{u}, w) \in cl(C), \end{align*}$$将上式乘以$\epsilon > 0$加上式(\ref{equ: nonvertical hyperplane})可得$$\begin{align*} (\bar{\boldsymbol{\mu}} + \epsilon \boldsymbol{\mu})^\top \boldsymbol{u} + \epsilon \beta w > \bar{\gamma} + \epsilon \gamma, \ \forall (\boldsymbol{u}, w) \in cl(C), \forall \epsilon > 0. \end{align*}$$又$\bar{\gamma} > \bar{\boldsymbol{\mu}}^\top \bar{\boldsymbol{u}}$，故对于充分小的$\epsilon$有$$\begin{align*} \bar{\gamma} + \epsilon \gamma > (\bar{\boldsymbol{\mu}} + \epsilon \boldsymbol{\mu})^\top \bar{\boldsymbol{u}} + \epsilon \beta \bar{w}. \end{align*}$$结合上面两式可得$$\begin{align*} (\bar{\boldsymbol{\mu}} + \epsilon \mu)^\top \boldsymbol{u} + \epsilon \beta w > (\bar{\boldsymbol{\mu}} + \epsilon \mu)^\top \bar{\boldsymbol{u}} + \epsilon \beta \bar{w}, \ \forall (\boldsymbol{u}, w) \in cl(C), \end{align*}$$故存在非垂直超平面严格分离$(\bar{\boldsymbol{u}}, \bar{w})$和$cl(C)$，其对应的法向量为$(\bar{\boldsymbol{\mu}} + \epsilon \mu, \epsilon \beta)$，又$C \subseteq  cl(C)$，故该超平面严格分离$(\bar{\boldsymbol{u}}, \bar{w})$和$C$.


[C1S5-pic1]: {{"/assets/images/C1S5-pic1.png" | site.baseurl }}
[C1S5-pic2]: {{"/assets/images/C1S5-pic2.png" | site.baseurl }}
[C1S5-pic3]: {{"/assets/images/C1S5-pic3.png" | site.baseurl }}
[C1S5-pic4]: {{"/assets/images/C1S5-pic4.png" | site.baseurl }}
[C1S5-pic5]: {{"/assets/images/C1S5-pic5.png" | site.baseurl }}
[C1S5-pic6]: {{"/assets/images/C1S5-pic6.png" | site.baseurl }}
[C1S5-pic7]: {{"/assets/images/C1S5-pic7.png" | site.baseurl }}

