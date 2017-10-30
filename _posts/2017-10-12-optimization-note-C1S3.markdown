---
layout: post
title:  "C1S3 - 相对内部和闭包"
date:   2017-10-12 18:04:00 +0800
tags: [Mathematics]
---

《凸优化理论》笔记

在前两节里已经涉及到集合的相对内部与闭包的概念，这一节我们深入研究它们的性质和计算，之后介绍凸函数的连续性以及函数闭包的概念.

设凸集$C$是$\mathbb{R}^n$的非空子集，由命题1.1.2(4)知，其闭包$cl(C)$是非空凸集，其内部$int(C)$也是凸集，但是可能是空的($\mathbb{R}^3$中的集合$S=\{ \boldsymbol{x} \in \mathbb{R}^3 \ \vert \ x_1^2 + x_2^2 \leq 1, x_3 = 1 \}$就是如此)，为此我们需要引入相对内部的定义.

集合$C$是非空凸集，若$\boldsymbol{x} \in C$且存在一个以$\boldsymbol{x}$为球心的开球$B(\boldsymbol{x}, \varepsilon)$满足$B \cap aff(C) \subseteq C$，则称$\boldsymbol{x}$是$C$的相对内部点(relative interior point)，$C$的所有相对内部点的集合称作$C$的相对内部(relative interior)，记为$ri(C)$.若$ri(X) = X$，则称集合$X$是相对开的，$cl(X)$中不属于$ri(X)$的点称为$X$的相对边界点(relative boundary point)，$C$的所有相对边界点的集合称作$C$的相对边界(relative boundary).

我们约定单点集的相对内部就是它本身.继续考虑之前那个例子，可以发现虽然$int(S) = \emptyset$，但$ri(S) = \{ \boldsymbol{x} \in \mathbb{R}^3 \ \vert \ x_1^2 + x_2^2 < 1, x_3 = 1 \}$，已经不再是空集了.

**命题1.3.1**：集合$C$是非空凸集，若$\boldsymbol{x} \in ri(C)$，$\bar{\boldsymbol{x}} \in cl(C)$，则连接$\boldsymbol{x}$和$\bar{\boldsymbol{x}}$的线段上，除$\bar{\boldsymbol{x}}$外的所有点都属于$ri(C)$.

证明：参考右图，分两种情况：

![C1S3 Pic1][C1S3-pic1]

若$\bar{\boldsymbol{x}} \in C$，由于$\boldsymbol{x} \in ri(C)$，故存在开球$S = \{\boldsymbol{z} \ \vert \ \|\boldsymbol{z} - \boldsymbol{x}\| < \epsilon\}$使得$S \cap aff(C) \subseteq C$.对于任意$\alpha \in (0,1]$，设$\boldsymbol{x}_\alpha = \alpha \boldsymbol{x} + (1 - \alpha) \bar{\boldsymbol{x}}$且$S_\alpha = \{\boldsymbol{z} \ \vert \ \|\boldsymbol{z} - \boldsymbol{x}_\alpha\| < \alpha \epsilon\}$，于是$S_\alpha \cap aff(C)$中的任意一点都可以看成$S \cap aff(C)$中某点与$\bar{\boldsymbol{x}}$的凸组合，由$C$的凸性知$S_\alpha \cap aff(C) \subseteq C$，故$\boldsymbol{x}_\alpha \in ri(C)$.

若$\bar{\boldsymbol{x}} \not \in C$，由于$\boldsymbol{x} \in ri(C)$，故存在开球$S = \{\boldsymbol{z} \ \vert \ \|\boldsymbol{z} - \boldsymbol{x}\| < \epsilon\}$使得$S \cap aff(C) \subseteq C$.对于任意$\alpha \in (0,1]$，设$\boldsymbol{x}_\alpha = \alpha \boldsymbol{x} + (1 - \alpha) \bar{\boldsymbol{x}}$，下面证明$\boldsymbol{x}_\alpha \in ri(C)$.考虑收敛于$\bar{\boldsymbol{x}}$的序列$\{\boldsymbol{x}_k\} \subseteq C$，设$\boldsymbol{x}_{k,\alpha} = \alpha \boldsymbol{x} + (1 - \alpha) \boldsymbol{x}_k$，显然$\{ \boldsymbol{z} \ \vert \ \|\boldsymbol{z} - \boldsymbol{x}_{k,\alpha} \| < \alpha \epsilon\} \cap aff(C) \subseteq C$. 又$\boldsymbol{x}_{k,\alpha} \rightarrow \boldsymbol{x}_\alpha$，故当$k$足够大时有$$\begin{align*} \{ \boldsymbol{z} \ \vert \ \|\boldsymbol{z} - \boldsymbol{x}_\alpha \| < \alpha \epsilon / 2\} \subseteq \{ \boldsymbol{z} \ \vert \ \|\boldsymbol{z} - \boldsymbol{x}_{k,\alpha} \| < \alpha \epsilon \} \end{align*}$$这意味着$\{ \boldsymbol{z} \ \vert \ \|\boldsymbol{z} - \boldsymbol{x}_\alpha \| < \alpha \epsilon / 2\} \cap aff(C) \subseteq C$，故$\boldsymbol{x}_\alpha \in ri(C)$.

直观看来，命题1.3.1很简单，但是证明叙述起来却挺麻烦，它的一个推论是如下命题，也是一个直观很简单证明起来很麻烦的命题.

**命题1.3.2**：集合$C$是非空凸集，则

$ri(C)$是非空凸集且$aff(ri(C)) = aff(C)$.
若$aff(C)$的维度为$m > 0$，那么存在$\boldsymbol{x}_0, \boldsymbol{x}_1, \dots, \boldsymbol{x}_m \in ri(C)$使得$\boldsymbol{x}_1 - \boldsymbol{x}_0, \dots, \boldsymbol{x}_m - \boldsymbol{x}_0$张成平行于$aff(C)$的子空间.
证明：

![C1S3 Pic2][C1S3-pic2]

由命题1.3.1知$ri(C)$是凸的，下面证明其非空，不妨设$\boldsymbol{0} \in C$，否则可以将$C$平移使其包含$\boldsymbol{0}$，这不影响结论，这样$aff(C)$就是一个$m$维子空间了. 
如果$m = 0$，那么$C$和$aff(C)$就是一个点，由于单点集的相对内部就是它本身，故此时$ri(C)$非空.若$m > 0$，那么可以找到$m$个线性无关的向量$\boldsymbol{z}_1, \dots, \boldsymbol{z}_m \in C$张成了$aff(C)$，即$\boldsymbol{z}_1, \dots, \boldsymbol{z}_m$是$aff(C)$的一组基.考虑集合$$\begin{align*}X = \left\{ \boldsymbol{x} \ \vert \ \boldsymbol{x} = \sum_{i=1}^m \alpha_i \boldsymbol{z}_i, \sum_{i=1}^m \alpha_i < 1, \alpha > 0,i = 1, \dots, m \right\},\end{align*}$$如右图所示，由于$C$的凸性，于是$X \subseteq C$(可以将$X$中的所有元素视为$\boldsymbol{z}_1, \dots, \boldsymbol{z}_m, \boldsymbol{0}$的凸组合).下面证明$X$是$aff(C)$中的相对开集，对于$\forall \bar{\boldsymbol{x}} \in X$，设$\boldsymbol{x} \in aff(C)$，那么有$\bar{\boldsymbol{x}} = \boldsymbol{Z} \bar{\boldsymbol{\alpha}}$和$\boldsymbol{x} = \boldsymbol{Z} \boldsymbol{\alpha}$，其中$\boldsymbol{Z} = [\boldsymbol{z}_1, \dots, \boldsymbol{z}_m] \in \mathbb{R}^{n \times m}$，$\bar{\boldsymbol{\alpha}}$和$\boldsymbol{\alpha}$分别是唯一的$m$维向量($\boldsymbol{z}_1, \dots, \boldsymbol{z}_m$是$aff(C)$的一组基).易知$\boldsymbol{Z}^\top \boldsymbol{Z}$对称半正定，又$\boldsymbol{Z}$满秩，故$\boldsymbol{Z}^\top \boldsymbol{Z}$正定，由Rayleigh's不等式知，存在$\gamma \geq \lambda_{min}(\boldsymbol{Z}^\top \boldsymbol{Z})$满足

$$\begin{align} \label{equ: Rayleigh} \| \boldsymbol{x} - \bar{\boldsymbol{x}} \|^2 = (\boldsymbol{\alpha} - \bar{\boldsymbol{\alpha}})^\top \boldsymbol{Z}^\top \boldsymbol{Z}^\top (\boldsymbol{\alpha} - \bar{\boldsymbol{\alpha}}) \geq \gamma \|\boldsymbol{\alpha} - \bar{\boldsymbol{\alpha}}\|^2, \end{align}$$

其中，$\lambda_{min}(\boldsymbol{Z}^\top \boldsymbol{Z})$是$\boldsymbol{Z}^\top \boldsymbol{Z}$的最小特征值.由于$\bar{\boldsymbol{x}} \in X$，故$\bar{\boldsymbol{\alpha}} \in A$，其中$$\begin{align*}A = \left\{ (\alpha_1, \dots, \alpha_m) \ \vert \ \sum_{i=1}^m \alpha_i < 1, \alpha > 0,i = 1, \dots, m \right\}, \end{align*}$$
由式(\ref{equ: Rayleigh})可知$\| \boldsymbol{x} - \bar{\boldsymbol{x}} \|^2\rightarrow0$时有$\| \boldsymbol{\alpha} - \bar{\boldsymbol{\alpha}} \|^2\rightarrow0$，即如果$\boldsymbol{x}$在以$\bar{\boldsymbol{x}}$为球心的充分小的球里，则$\boldsymbol{\alpha} \in A$，故$\boldsymbol{x} \in X$，这意味着存在一个以$\bar{\boldsymbol{x}}$为球心的充分小的球$B$使得$B \cap aff(C) \in X$，由$\bar{\boldsymbol{x}}$的任意性知$X$中的每个点都是$C$的相对内部点，故$ri(C)$是非空.由$X$的构造过程易知$aff(X) = aff(C)$，又$X \subseteq ri(C)$，故$aff(ri(C)) = aff(C)$.
由(a)中证明知$ri(C)$非空，故至少存在$\boldsymbol{x}_0 \in ri(C)$，将$C$平移$\boldsymbol{x}_0$，即将$\boldsymbol{x}_0$移到原点，新的集合为$C - \boldsymbol{x}_0$，设$\boldsymbol{z}_1, \dots, \boldsymbol{z}_m \in C - \boldsymbol{x}_0$且张成了$C - \boldsymbol{x}_0$，$\alpha \in (0, 1)$，因为$\boldsymbol{0} \in ri(C - \boldsymbol{x}_0)$，由命题1.3.1知，$\alpha \boldsymbol{z}_i \in C - \boldsymbol{x}_0, i = 1, \dots, m$，这意味着$\boldsymbol{x}_i = \boldsymbol{x}_0 + \alpha \boldsymbol{z}_i \in ri(C), i = 1, \dots, m$且$\boldsymbol{x}_1 - \boldsymbol{x}_0, \dots, \boldsymbol{x}_m - \boldsymbol{x}_0$张成了$aff(C)$.
下面这个命题也是命题1.3.1的一个推论，直观来说，它陈述了这样一个显而易见的事实，如果一个点是某个非空凸集的相对内部点，那么以该点为端点且属于该凸集的任意线段在该点处延长一小段后都不会离开该凸集.

**命题1.3.3**：集合$C$是非空凸集，$\boldsymbol{x} \in ri(C)$当且仅当对$\forall \bar{\boldsymbol{x}} \in C$，存在$\gamma > 0$使得$\boldsymbol{x} + \gamma(\boldsymbol{x} - \bar{\boldsymbol{x}}) \in C$.

证明：一方面，若$\boldsymbol{x} \in ri(C)$，由相对内部点的定义知对$\forall \bar{\boldsymbol{x}} \in C$，存在$\gamma > 0$使得$\boldsymbol{x} + \gamma(\boldsymbol{x} - \bar{\boldsymbol{x}}) \in C$.

另一方面，若$\boldsymbol{x}$满足所给条件，设$\bar{\boldsymbol{x}} \in ri(C)$(由命题1.3.2知$\bar{\boldsymbol{x}}$存在)，若$\boldsymbol{x} = \bar{\boldsymbol{x}}$，结论已成立，不妨设$\boldsymbol{x} \neq \bar{\boldsymbol{x}}$，由所给条件，存在$\gamma > 0$使得$\boldsymbol{y} = \boldsymbol{x} + \gamma(\boldsymbol{x} - \bar{\boldsymbol{x}}) \in C$，即$\boldsymbol{x}$在以$\boldsymbol{y}$和$\bar{\boldsymbol{x}}$为端点的线段的内部，又$\bar{\boldsymbol{x}} \in ri(C)$，$\boldsymbol{y} \in C$，由命题1.3.1知$\boldsymbol{x} \in ri(C)$.

今后我们将会看到，相对内部这个概念在凸优化和对偶理论里是无处不在的，下面这个命题就是一个例子.

**命题1.3.4**：集合$C$是$\mathbb{R}^n$的非空凸子集，$f: X \mapsto \mathbb{R}$是凹函数，设$$\begin{align*} X^* = \left\{ \boldsymbol{x}^* \in X \ \vert \ f(\boldsymbol{x}^*) = \inf_{\boldsymbol{x} \in X} f(\boldsymbol{x}) \right\}. \end{align*}$$若$X^*$包含$X$的相对内部点，则$f$必是$X$上的常数函数，也即$X^* = X$.

证明：设$\boldsymbol{x}^* \in X^* \cap ri(X)$，$\boldsymbol{x}$是$X$中任意向量，由命题1.3.3知存在$\gamma > 0$使得$$\begin{align*} \hat{\boldsymbol{x}} = \boldsymbol{x}^* + \gamma (\boldsymbol{x}^* - \boldsymbol{x}) \in X \end{align*}$$又$$\begin{align*} \boldsymbol{x}^* = \frac{1}{\gamma+1} \hat{\boldsymbol{x}} + \frac{\gamma}{\gamma+1} \boldsymbol{x} \end{align*}$$由$f$的凹性知$$\begin{align*} f(\boldsymbol{x}^*) \geq \frac{1}{\gamma+1} f(\hat{\boldsymbol{x}}) + \frac{\gamma}{\gamma+1} f(\boldsymbol{x}) \end{align*}$$由于$f(\hat{\boldsymbol{x}}) \geq f(\boldsymbol{x}^*)$，$f(\boldsymbol{x}) \geq f(\boldsymbol{x}^*)$，代入上式可得$$\begin{align*} f(\boldsymbol{x}^*) \geq \frac{1}{\gamma+1} f(\hat{\boldsymbol{x}}) + \frac{\gamma}{\gamma+1} f(\boldsymbol{x}) \geq \frac{1}{\gamma+1} f(\boldsymbol{x}^*) + \frac{\gamma}{\gamma+1} f(\boldsymbol{x}^*) = f(\boldsymbol{x}^*), \end{align*}$$故$f(\boldsymbol{x}) = f(\boldsymbol{x}^*)$.

注意线性函数也是凹函数，因此由命题1.3.4可知，除非线性函数在整个可行域上为常数，否则只可能在可行域的相对边界取得极值.

为了今后处理问题方便，我们有必要建立起相对内部和闭包的运算法则，总结起来就是下面的5个命题.

两个非空凸集有相同的闭包当且仅当它们有相同的相对内部(命题1.3.5).
在线性变换下，相对内部可以保持，闭包不一定能保持，保持的前提是该非空凸集有界(命题1.3.6).
在Cartesian积下，相对内部和闭包都可以保持；在向量加和下，相对内部可以保持，闭包不一定能保持，保持的前提是至少其中一个非空凸集有界(命题1.3.7).
在线性逆变换积下，相对内部和闭包都可以保持(命题1.3.8).
在集合交下，相对内部和闭包都不一定能保持，保持的前提是两个集合的相对内部的交集非空(命题1.3.9).
**命题1.3.5**：集合$C$是非空凸集，那么

$cl(C) = cl(ri(C))$.
$ri(C) = ri(cl(C))$.
设$\bar{C}$是另一个非空凸集，则如下3个条件等价：
$C$和$\bar{C}$有相同的相对内部.
$C$和$\bar{C}$有相同的闭包.
$ri(C) \subseteq \bar{C} \subseteq cl(C)$.
证明：

一方面，由$ri(C) \subseteq C$易知有$cl(ri(C)) \subseteq cl(C)$.另一方面，设$\bar{\boldsymbol{x}} \in cl(C)$，对于$\forall \boldsymbol{x} \in ri(C)$(由命题1.3.2知$\boldsymbol{x}$存在)，若$\boldsymbol{x} = \bar{\boldsymbol{x}}$，结论已成立，不妨设$\boldsymbol{x} \neq \bar{\boldsymbol{x}}$，由命题1.3.1知对于$\forall \alpha \in (0, 1]$有$\alpha \boldsymbol{x} + (1 - \alpha)\bar{\boldsymbol{x}} \in ri(C)$，因此$\bar{\boldsymbol{x}}$是序列$\left\{ \frac{1}{k}\boldsymbol{x} + (1 - \frac{1}{k})\bar{\boldsymbol{x}} \ \vert \ k \geq 1 \right\}$的极限，由于该序列属于$ri(C)$，故$\bar{\boldsymbol{x}} \in cl(ri(C))$，于是$cl(C) \subseteq cl(ri(C))$.
一方面，对于$\forall \boldsymbol{x} \in ri(C)$，存在以$\boldsymbol{x}$为球心的球$B$满足$B \cap aff(C) \subseteq C$，由命题1.2.1知$aff(C) = aff(cl(C))$，故$B \cap aff(cl(C)) \subseteq C \subseteq cl(C)$，这意味着$\boldsymbol{x} \in ri(cl(C))$，于是$ri(C) \subseteq ri(cl(C))$.另一方面，设$\boldsymbol{z} \in ri(cl(C))$，由命题1.3.2知存在$\boldsymbol{x} \in ri(C)$，若$\boldsymbol{x} = \boldsymbol{z}$，结论已成立，不妨设$\boldsymbol{x} \neq \boldsymbol{z}$，由命题1.3.3知对于充分接近$0$的$\gamma > 0$有$\boldsymbol{y} = \boldsymbol{z} + \gamma(\boldsymbol{z} - \boldsymbol{x}) \in cl(C)$，那么$\boldsymbol{z} = (1 - \alpha) \boldsymbol{x} + \alpha \boldsymbol{y}$，其中$\alpha = \frac{1}{\gamma + 1} \in (0, 1)$，由命题1.3.1知$\boldsymbol{z} \in ri(C)$.
先证前两者.一方面，若$ri(C) = ri(\bar{C})$，由(1)知$cl(C) = cl(ri(C)) = cl(ri(\bar{C})) = cl(\bar{C})$).另一方面，若$cl(C) = cl(ri(\bar{C}))$，由(2)知$ri(C) = ri(cl(C)) = ri(cl(\bar{C})) = ri(\bar{C})$. 
再证前两者和第三者等价.一方面，由$ri(\bar{C}) \subseteq \bar{C} \subseteq cl(\bar{C})$知$ri(C) \subseteq \bar{C} \subseteq cl(C)$.另一方面，若$ri(C) \subseteq \bar{C} \subseteq cl(C)$，取闭包知$cl(ri(C)) \subseteq cl(\bar{C}) \subseteq cl(C)$，由(1)知$cl(ri(C)) \subseteq cl(\bar{C}) \subseteq cl(C) = cl(ri(C))$，故$cl(\bar{C}) = cl(C)$.

**命题1.3.6**：集合$C$是$\mathbb{R}^n$的非空凸子集，矩阵$\boldsymbol{A} \in \mathbb{R}^{m \times n}$，那么

$\boldsymbol{A} \cdot ri(C) = ri(\boldsymbol{A} \cdot C)$.
$\boldsymbol{A} \cdot cl(C) \subseteq cl(\boldsymbol{A} \cdot C)$，若$C$有界，则$\boldsymbol{A} \cdot cl(C) = cl(\boldsymbol{A} \cdot C)$.
证明：

设序列$\{\boldsymbol{x}_k\} \in C$，则其极限$\boldsymbol{x} \in cl(C)$，那么序列$\{\boldsymbol{A} \cdot \boldsymbol{x}_k\} \subseteq \boldsymbol{A} \cdot C$，其极限$\boldsymbol{A} \boldsymbol{x} \in cl(\boldsymbol{A} \cdot C)$，故$\boldsymbol{A} \cdot cl(C) \subseteq cl(\boldsymbol{A} \cdot C)$，这就证明了(b)的前半部分. 
一方面，结合命题1.3.5(a)易知有$$\begin{align*}\boldsymbol{A} \cdot ri(C) \subseteq \boldsymbol{A} \cdot C \subseteq \boldsymbol{A} \cdot cl(C) = \boldsymbol{A} \cdot cl(ri(C)) \subseteq cl(\boldsymbol{A} \cdot ri(C)),\end{align*}$$因此凸集$\boldsymbol{A} \cdot C$介于凸集$\boldsymbol{A} \cdot ri(C)$和其闭包$cl(\boldsymbol{A} \cdot ri(C))$之间，由命题1.3.5(c)知$\boldsymbol{A} \cdot C$和$\boldsymbol{A} \cdot ri(C)$有相同的相对内部，故$ri(\boldsymbol{A} \cdot C) = ri(\boldsymbol{A} \cdot ri(C)) \subseteq \boldsymbol{A} \cdot ri(C)$. 
另一方面，对于$\forall \boldsymbol{z} \in \boldsymbol{A} \cdot ri(C)$及$\forall \boldsymbol{x} \in \boldsymbol{A} \cdot C$，存在$\bar{\boldsymbol{z}} \in ri(C)$及$\bar{\boldsymbol{x}} \in C$使得$\boldsymbol{z} = \boldsymbol{A} \bar{\boldsymbol{z}}$及$\boldsymbol{x} = \boldsymbol{A}  \bar{\boldsymbol{x}}$，由$C$的凸性及命题1.3.3知存在$\gamma > 0$使得$\bar{\boldsymbol{y}} = \bar{\boldsymbol{z}} + \gamma (\bar{\boldsymbol{z}} - \bar{\boldsymbol{x}}) \in C$，因此$\boldsymbol{A} \cdot \bar{\boldsymbol{y}} = \boldsymbol{z} + \gamma(\boldsymbol{z} - \boldsymbol{x}) \in \boldsymbol{A} \cdot C$，由$\boldsymbol{x}$的任意性及命题1.3.3知$\boldsymbol{z} \in ri(\boldsymbol{A} \cdot C)$.
由(1)知$\boldsymbol{A} \cdot cl(C) \subseteq cl(\boldsymbol{A} \cdot C)$，对于$\forall \boldsymbol{z} \in cl(\boldsymbol{A} \cdot C)$，存在序列$\{\boldsymbol{x}_k\} \subseteq C$使得$\boldsymbol{A} \boldsymbol{x}_k \rightarrow \boldsymbol{z}$，若$C$有界，则存在$\{\boldsymbol{x}_k\}$的子序列收敛到$\boldsymbol{x} \in cl(C)$，于是$\boldsymbol{z} \in \boldsymbol{A} \cdot cl(C)$.
$C$有界是必须的，否则若$C$是无界闭凸集，$\boldsymbol{A} \cdot C$可能不是闭集.如右图所示，集合

![C1S3 Pic3][C1S3-pic3]

$$\begin{align*}C = \left\{ (x_1, x_2) \ \vert \ x_1 > 0, x_2 > 0, x_1x_2 \geq 1 \right\},\end{align*}$$线性变换$\boldsymbol{A}$表示朝$x_1$轴上投影，则$$\begin{align*}\boldsymbol{A} \cdot cl(C) & = \left\{ (x_1, x_2) \ \vert \ x_1 > 0, x_2 = 0 \right\},   \\cl(\boldsymbol{A} \cdot C) & = \left\{ (x_1, x_2) \ \vert \ x_1 \geq 0, x_2 = 0 \right\},\end{align*}$$显然$\boldsymbol{A} \cdot cl(C) \neq cl(\boldsymbol{A} \cdot C))$.

**命题1.3.7**：集合$C_1$和$C_2$是非空凸集，那么

$ri(C_1 \times C_2) = ri(C_1) \times ri(C_2)$，$cl(C_1 \times C_2) = cl(C_1) \times cl(C_2)$.
$ri(C_1 + C_2) = ri(C_1) + ri(C_2)$，$cl(C_1) + cl(C_2) \subseteq cl(C_1 + C_2)$.
若$C_1$和$C_2$中至少有一个有界，则$cl(C_1) + cl(C_2) = cl(C_1 + C_2)$.
证明：

设$\boldsymbol{x} = [\boldsymbol{x}_1^\top, \boldsymbol{x}_2^\top]^\top \in ri(C_1 \times C_2)$，由命题1.3.3知对任意$\bar{\boldsymbol{x}} = [\bar{\boldsymbol{x}}_1^\top, \bar{\boldsymbol{x}}_2^\top]^\top \in C_1 \times C_2$，存在$\gamma > 0$使得$\boldsymbol{x} + \gamma (\boldsymbol{x} - \bar{\boldsymbol{x}}) \in C_1 \times C_2$，也即$$\begin{align*}\boldsymbol{x}_1 + \gamma (\boldsymbol{x}_1 - \bar{\boldsymbol{x}}_1) \in C_1 \ \ \ \boldsymbol{x}_2 + \gamma (\boldsymbol{x}_2 - \bar{\boldsymbol{x}}_2) \in C_2 \end{align*}$$于是再次由命题1.3.3知$\boldsymbol{x}_1 \in ri(C_1)$且$\boldsymbol{x}_2 \in ri(C_2)$，也即$\boldsymbol{x} \in ri(C_1) \times ri(C_2)$，这就证明了$ri(C_1 \times C_2) \subseteq ri(C_1) \times ri(C_2)$，反过来同理可证$ri(C_1 \times C_2) \supseteq ri(C_1) \times ri(C_2)$，故$ri(C_1 \times C_2) = ri(C_1) \times ri(C_2)$. 
设$\boldsymbol{x} = [\boldsymbol{x}_1^\top, \boldsymbol{x}_2^\top]^\top \in cl(C_1 \times C_2)$，于是存在收敛于$\boldsymbol{x}$的序列$\{\boldsymbol{x}_k = [\boldsymbol{x}_{k1}^\top, \boldsymbol{x}_{k2}^\top]^\top \} \subseteq C_1 \times C_2$，这意味着$\{\boldsymbol{x}_{k1}\} \rightarrow \boldsymbol{x}_1$且$\{\boldsymbol{x}_{k2}\} \rightarrow \boldsymbol{x}_2$，即$\boldsymbol{x}_1 \in cl(C_1)$且$\boldsymbol{x}_2 \in cl(C_2)$，也即$\boldsymbol{x} \in cl(C_1) \times cl(C_2)$，这就证明了$cl(C_1 \times C_2) \subseteq cl(C_1) \times cl(C_2)$，反过来同理可证$cl(C_1 \times C_2) \supseteq cl(C_1) \times cl(C_2)$，故$cl(C_1 \times C_2) = cl(C_1) \times cl(C_2)$.
考虑线性变换$\boldsymbol{A}: \mathbb{R}^{2n} \mapsto \mathbb{R}^n = (\boldsymbol{I}_n, \boldsymbol{I}_n)$，即$$\begin{align*} \boldsymbol{A} \begin{bmatrix} \boldsymbol{x}_1 \\ \boldsymbol{x}_2 \end{bmatrix} = \boldsymbol{x}_1 + \boldsymbol{x}_2, \ \ \ \boldsymbol{x}_1, \boldsymbol{x}_2 \in \mathbb{R}^n. \end{align*}$$由命题1.3.6(a)及$ri(C_1 \times C_2) = ri(C_1) \times ri(C_2)$知$$\begin{align*} ri(C_1 + C_2) = ri(\boldsymbol{A} \cdot (C_1 \times C_2)) = \boldsymbol{A} \cdot ri(C_1 \times C_2) = \boldsymbol{A} \cdot (ri(C_1) \times ri(C_2)) = ri(C_1) + ri(C_2). \end{align*}$$同样由命题1.3.6(b)及$cl(C_1 \times C_2) = cl(C_1) \times cl(C_2)$知$$\begin{align*} cl(C_1) + cl(C_2) = \boldsymbol{A} \cdot (cl(C_1) \times cl(C_2)) = \boldsymbol{A} \cdot (cl(C_1 \times C_2)) \subseteq cl(\boldsymbol{A} \cdot (C_1 \times C_2)) = cl(C_1 + C_2).\end{align*}$$
不妨设$C_1$有界，对于$\forall \boldsymbol{x} \in cl(C_1 + C_2)$，存在序列$\{\boldsymbol{x}_{1, k}\}  \subseteq  C_1$和$\{\boldsymbol{x}_{2, k}\} \subseteq C_2$使得$\boldsymbol{x}_{1, k} + \boldsymbol{x}_{2, k} \rightarrow \boldsymbol{x}$.又$C_1$有界，故$\{\boldsymbol{x}_{1, k}\}$有界，从而$\{\boldsymbol{x}_{2, k}\}$有界.因此，存在序列$\{[\boldsymbol{x}_{1, k}^\top, \boldsymbol{x}_{2, k}^\top]\}$的子序列收敛到$\{[\boldsymbol{x}_1^\top, \boldsymbol{x}_2^\top]\}$且$\boldsymbol{x}_1 + \boldsymbol{x}_2 = \boldsymbol{x}$，又$\boldsymbol{x}_1 \in cl(C_1)$，$\boldsymbol{x}_2 \in cl(C_2)$，故$\boldsymbol{x} \in cl(C_1) + cl(C_2)$，于是$cl(C_1 + C_2) \subseteq cl(C_1) + cl(C_2)$.
$C_1$和$C_2$中至少有一个有界是必须的，如上图所示，集合$$\begin{align*}C_1 = \left\{ (x_1, x_2) \ \vert \ x_1 > 0, x_2 > 0, x_1x_2 \geq 1 \right\}, \ C_2 = \left\{ (x_1, x_2) \ \vert \ x_1 = 0 \right\},\end{align*}$$则$$\begin{align*}cl(C_1 + C_2) & = \left\{ (x_1, x_2) \ \vert \ x_1 \geq 0 \right\}, \\cl(C_1) + cl(C_2) & = \left\{ (x_1, x_2) \ \vert \ x_1 > 0 \right\},\end{align*}$$显然$cl(C_1 + C_2) \neq cl(C_1) + cl(C_2)$.

**命题1.3.8**：集合$C_1$和$C_2$是非空凸集，那么

$ri(C_1) \cap ri(C_2) \subseteq ri(C_1 \cap C_2)$，$cl(C_1 \cap C_2) \subseteq cl(C_1) \cap cl(C_2)$.
若$ri(C_1)$和$ri(C_2)$有非空交集，则$ri(C_1) \cap ri(C_2) = ri(C_1 \cap C_2)$，$cl(C_1 \cap C_2) = cl(C_1) \cap cl(C_2)$.
证明：

对于$\forall \boldsymbol{x} \in ri(C_1) \cap ri(C_2)$和$\forall \boldsymbol{y} \in C_1 \cap C_2$，由命题1.3.3知连接$\boldsymbol{x}$和$\boldsymbol{y}$的线段沿$\boldsymbol{x}$端延长一小段依然分别属于$C_1$和$C_2$，故再次由命题1.3.3知$\boldsymbol{x} \in ri(C_1 \cap C_2)$，于是$ri(C_1) \cap ri(C_2) \subseteq ri(C_1 \cap C_2)$. 
显然有$C_1 \subseteq cl(C_1)$和$C_2 \subseteq cl(C_2)$，故$C_1 \cap C_2 \subseteq cl(C_1) \cap cl(C_2)$，又闭集的交集是闭集，闭集的闭包是其本身，于是$cl(C_1 \cap C_2) \subseteq cl(cl(C_1) \cap cl(C_2)) = cl(C_1) \cap cl(C_2)$.
若$ri(C_1)$和$ri(C_2)$有非空交集，则存在$\boldsymbol{x} \in ri(C_1) \cap ri(C_2)$，设$\boldsymbol{y} \in cl(C_1) \cap cl(C_2)$，由命题1.3.1知对于$\forall \alpha \in (0, 1]$有$\alpha \boldsymbol{x} + (1 - \alpha) \boldsymbol{y} \in ri(C_1) \cap ri(C_2)$，因此对于序列$\{\alpha_k \boldsymbol{x} + (1 - \alpha_k) \boldsymbol{y} \} \in ri(C_1) \cap ri(C_2)$，当$\alpha_k \rightarrow 0$时，其极限$\boldsymbol{y} \in cl(ri(C_1) \cap ri(C_2))$，于是有$$\begin{align} \label{equ: calculus of relative interiors and closures d} cl(C_1) \cap cl(C_2) \subseteq cl(ri(C_1) \cap ri(C_2)) \subseteq cl(C_1 \cap C_2) \end{align}$$由(1)知$cl(C_1 \cap C_2) \subseteq cl(C_1) \cap cl(C_2)$，故$cl(C_1 \cap C_2) = cl(C_1) \cap cl(C_2)$，此外式(\ref{equ: calculus of relative interiors and closures d})中全部该取等号，从而$C_1 \cap C_2$和$ri(C_1) \cap ri(C_2)$有相同的闭包，由命题1.3.5(c)知它们也应该有相同的相对内部，即$$\begin{align*}ri(C_1 \cap C_2) = ri(ri(C_1) \cap ri(C_2)) \subseteq ri(C_1) \cap ri(C_2),\end{align*}$$由(a) 知$ri(C_1) \cap ri(C_2) \subseteq ri(C_1 \cap C_2)$，故$ri(C_1) \cap ri(C_2) = ri(C_1 \cap C_2)$.
$ri(C_1)$和$ri(C_2)$有非空交集是必须的，设集合$$\begin{align*} C_1 = \left\{ x \ \vert \ x \geq 0 \right\}, \ C_2 = \left\{ x \ \vert \ x \leq 0 \right\}. \end{align*}$$则$$\begin{align*} ri(C_1 \cap C_2) = \{ 0 \} \neq \emptyset = ri(C_1) \cap ri(C_2), \end{align*}$$显然$ri(C_1 \cap C_2) \neq ri(C_1) \cap ri(C_2)$.

设集合$$\begin{align*} C_1 = \left\{ x \ \vert \ x > 0 \right\}, \ C_2 = \left\{ x \ \vert \ x < 0 \right\}. \end{align*}$$则$$\begin{align*} cl(C_1 \cap C_2) = \emptyset \neq \{ 0 \} = cl(C_1) \cap cl(C_2), \end{align*}$$显然$cl(C_1 \cap C_2) \neq cl(C_1) \cap cl(C_2)$.

**命题1.3.9**：集合$C$是$\mathbb{R}^{m}$的非空凸子集，矩阵$\boldsymbol{A} \in \mathbb{R}^{m \times n}$，如果$\boldsymbol{A}^{-1} \cdot ri(C)$非空，那么$$\begin{align*} ri(\boldsymbol{A}^{-1} \cdot C) = \boldsymbol{A}^{-1} \cdot ri(C), \ \ \ cl(\boldsymbol{A}^{-1} \cdot C) = \boldsymbol{A}^{-1} \cdot cl(C), \end{align*}$$这里$\boldsymbol{A}^{-1}$表示逆映射，不是逆矩阵的意思.

证明：先证第一个式子，定义集合$$\begin{align*} D = \mathbb{R}^n \times C, \ S = \{ (\boldsymbol{x}, \boldsymbol{A} \boldsymbol{x}) \ \vert \ \boldsymbol{x} \in \mathbb{R}^n \}. \end{align*}$$定义线性变换$T: \mathbb{R}^{n+m} \mapsto \mathbb{R}^n$如下：$$\begin{align*} T(\boldsymbol{x}, \boldsymbol{y}) = \boldsymbol{x}. \end{align*}$$易知$$\begin{align*} \boldsymbol{A}^{-1} \cdot C = \{ \boldsymbol{x} \ \vert \ \boldsymbol{A} \boldsymbol{x} \in C \} = T \cdot \{ (\boldsymbol{x}, \boldsymbol{A} \boldsymbol{x}) \ \vert \ \boldsymbol{A} \boldsymbol{x} \in C \} = T \cdot (D \cap S) \end{align*}$$于是$$\begin{align*}ri(\boldsymbol{A}^{-1} \cdot C) = ri(T \cdot (D \cap S)).\end{align*}$$由命题1.3.7(a)知$ri(D) = ri(\mathbb{R}^n) \times ri(C) = \mathbb{R}^n \times ri(C)$，于是$$\begin{align*}\boldsymbol{A}^{-1} \cdot ri(C) = \{ \boldsymbol{x} \ \vert \ \boldsymbol{A} \boldsymbol{x} \in ri(C) \} = T \cdot \{ (\boldsymbol{x}, \boldsymbol{A} \boldsymbol{x}) \ \vert \ \boldsymbol{A} \boldsymbol{x} \in ri(C) \} = T \cdot (ri(D) \cap S),\end{align*}$$由于$\boldsymbol{A}^{-1} \cdot ri(C)$非空，即存在$\boldsymbol{x} \in \mathbb{R}^n$使得$\boldsymbol{A}\boldsymbol{x} \in ri(C)$，那么$ri(D) \cap S$非空，又$S$是$\mathbb{R}^n$与$\mathbb{R}^m$某个字空间的Cartesian积，故$ri(S) = S$，于是根据命题1.3.6和命题1.3.8知$$\begin{align*}ri(T \cdot (D \cap S)) = T \cdot ri(D \cap S) = T \cdot (ri(D) \cap ri(S)) = T \cdot (ri(D) \cap S),\end{align*}$$于是$$\begin{align*}ri(\boldsymbol{A}^{-1} \cdot C) = \boldsymbol{A}^{-1} \cdot ri(C).\end{align*}$$

再证第二个式子，由命题1.3.7(a)知$cl(D) = cl(\mathbb{R}^n) \times cl(C) = \mathbb{R}^n \times cl(C)$，于是$$\begin{align*}\boldsymbol{A}^{-1} \cdot cl(C) = \{ \boldsymbol{x} \ \vert \ \boldsymbol{A} \boldsymbol{x} \in cl(C) \} = T \cdot \{ (\boldsymbol{x}, \boldsymbol{A} \boldsymbol{x}) \ \vert \ \boldsymbol{A} \boldsymbol{x} \in cl(C) \} = T \cdot (cl(D) \cap S),\end{align*}$$由于$ri(D) \cap S$非空且$ri(S) = S = cl(S)$，由命题1.3.8知$$\begin{align*}cl(D \cap S) = cl(D) \cap cl(S) = cl(D) \cap S,\end{align*}$$于是$$\begin{align*}\boldsymbol{A}^{-1} \cdot cl(C) = T \cdot (cl(D) \cap S) = T \cdot (cl(D \cap S)) \subseteq cl(T \cdot (D \cap S)) = cl(\boldsymbol{A}^{-1} \cdot C).\end{align*}$$反过来，设$\bar{\boldsymbol{x}} \in cl(\boldsymbol{A}^{-1} \cdot C)$，那么存在收敛于$\bar{\boldsymbol{x}}$的序列$\{\boldsymbol{x}_k\}$使得对于$\forall k$有$\boldsymbol{A}\boldsymbol{x}_k \in C$，于是序列$\{\boldsymbol{A}\boldsymbol{x}_k\}$收敛于$\boldsymbol{A}\bar{\boldsymbol{x}}$，故$\boldsymbol{A}\bar{\boldsymbol{x}} \in cl(C)$，即$\bar{\boldsymbol{x}} \in \boldsymbol{A}^{-1} cl(C)$.

综上有$cl(\boldsymbol{A}^{-1} \cdot C) = \boldsymbol{A}^{-1} \cdot cl(C)$成立.

**命题1.3.10**：凸集$C$是$\mathbb{R}^{n+m}$的子集，对于$\boldsymbol{x} \in \mathbb{R}^n$，设$C_{\boldsymbol{x}} = \{ \boldsymbol{y} \ \vert \ [\boldsymbol{x}^\top, \boldsymbol{y}^\top]^\top \in C \}$，$D = \{ \boldsymbol{x} \ \vert \ C_{\boldsymbol{x}} \neq \emptyset \}$，那么$ri(C) = \{ [\boldsymbol{x}^\top, \boldsymbol{y}^\top]^\top \ \vert \ \boldsymbol{x} \in ri(D), \boldsymbol{y} \in ri(C_{\boldsymbol{x}}) \}$.

证明：$D$是$C$在$\boldsymbol{x}$轴上的投影，由命题1.3.6(a)的知$$\begin{align*}ri(D) = \{ \boldsymbol{x} \ \vert \ [\boldsymbol{x}^\top, \boldsymbol{y}^\top]^\top \in ri(C) \}, 
\end{align*}$$故$$\begin{align*}ri(C) = \cup_{\boldsymbol{x} \in ri(D)} \left( M_{\boldsymbol{x}} \cap ri(C) \right),\end{align*}$$其中$M_{\boldsymbol{x}} = \{ [\boldsymbol{x}^\top, \boldsymbol{y}^\top]^\top \ \vert \ \boldsymbol{y} \in \mathbb{R}^m \}$，对于$\forall \boldsymbol{x} \in ri(D)$，由命题1.3.8(b)知$$\begin{align*}M_{\boldsymbol{x}} \cap ri(C)= ri(M_{\boldsymbol{x}} \cap C) = \{ [\boldsymbol{x}^\top, \boldsymbol{y}^\top]^\top \ \vert \ \boldsymbol{y} \in ri(C_{\boldsymbol{x}}) \},\end{align*}$$结合上面两式可得$$\begin{align*}ri(C) = \cup_{\boldsymbol{x} \in ri(D)} \{ [\boldsymbol{x}^\top, \boldsymbol{y}^\top]^\top \ \vert \ \boldsymbol{y} \in ri(C_{\boldsymbol{x}}) \} = \{ [\boldsymbol{x}^\top, \boldsymbol{y}^\top]^\top \ \vert \ \boldsymbol{x} \in ri(D), \boldsymbol{y} \in ri(C_{\boldsymbol{x}}) \}.\end{align*}$$

**命题1.3.11**：若函数$f: \mathbb{R}^n \mapsto (-\infty, \infty]$是正常凸函数，那么$f$在$ri(dom(f))$上必定连续.

证明：由于$f$是正常凸函数，故$ri(dom(f)) \neq \emptyset$，不妨设$\boldsymbol{0} \in ri(dom(f))$，否则可以将$f$平移使其有效定义域包含$\boldsymbol{0}$，这不影响结论.进一步设如下的单位超正方体$X = \{ \boldsymbol{x} \ \vert \ \|\boldsymbol{x}\|_{\infty} \leq 1\}$也属于$ri(dom(f))$，否则可以将$f$进行拉伸，这也不影响结论.下面只需证明$f$在$\boldsymbol{0}$处连续即可(非$\boldsymbol{0}$处的连续可通过将$f$平移得出)，也即对于任意收敛于$\boldsymbol{0}$的序列$\{\boldsymbol{x}_k\} \subseteq \mathbb{R}^n$有$f(\boldsymbol{x}_k) \rightarrow f(\boldsymbol{0} )$.

设$\boldsymbol{e}_i, i = 1,\dots, 2^n$是$X$的顶点，也即$\boldsymbol{e}_i$的每一维都是$1$或$-1$.显然$X$是凸集，故对于任意$\boldsymbol{x} \in X$有$$\begin{align*}\boldsymbol{x} = \sum_{i=1}^{2^n} \alpha_i \boldsymbol{e}_i, \ \sum_{i=1}^{2^n} \alpha_i = 1,\end{align*}$$设$A = \max_i f(\boldsymbol{e}_i)$，于是由Jensen's不等式可知$f(\boldsymbol{x}) \leq A$.

如右图所示，考虑如下的序列

![C1S3 Pic4][C1S3-pic4]

$$\begin{align*}\boldsymbol{y}_k = \frac{\boldsymbol{x}_k}{\|\boldsymbol{x}_k\|_{\infty}}, \ \boldsymbol{z}_k = -\frac{\boldsymbol{x}_k}{\|\boldsymbol{x}_k\|_{\infty}}, \end{align*}$$由于$\boldsymbol{x}_k$必然介于$\boldsymbol{y}_k$和$\boldsymbol{0}$之间，于是$$\begin{align*}f(\boldsymbol{x}_k) \leq (1 - \|\boldsymbol{x}_k\|_{\infty}) f(\boldsymbol{0} ) + \|\boldsymbol{x}_k\|_{\infty} f(\boldsymbol{y}_k),\end{align*}$$当$k \rightarrow \infty$时，$\boldsymbol{x}_k \rightarrow \boldsymbol{0}$，于是$\|\boldsymbol{x}_k\|_{\infty} \rightarrow 0$，又$f(\boldsymbol{y}_k) \leq A$，故$$\begin{align*}\limsup_{k \rightarrow \infty} f(\boldsymbol{x}_k) \leq f(\boldsymbol{0} ). 
\end{align*}$$同理，由于$\boldsymbol{0}$必然介于$\boldsymbol{x}_k$和$\boldsymbol{z}_k$之间，于是$$\begin{align*}f(\boldsymbol{0} ) \leq \frac{\|\boldsymbol{x}_k\|_{\infty}}{\|\boldsymbol{x}_k\|_{\infty} + 1} f(\boldsymbol{x}_k) + \frac{1}{\|\boldsymbol{x}_k\|_{\infty} + 1} f(\boldsymbol{x}_k),\end{align*}$$当$k \rightarrow \infty$时，$\boldsymbol{x}_k \rightarrow \boldsymbol{0}$，故$$\begin{align*}f(\boldsymbol{0} ) \leq \liminf_{k \rightarrow \infty} f(\boldsymbol{x}_k),\end{align*}$$又$\limsup_{k \rightarrow \infty} f(\boldsymbol{x}_k) \geq \liminf_{k \rightarrow \infty} f(\boldsymbol{x}_k)$，故有$\limsup_{k \rightarrow \infty} f(\boldsymbol{x}_k) = \liminf_{k \rightarrow \infty} f(\boldsymbol{x}_k) = f(\boldsymbol{0} )$，即$f$在$\boldsymbol{0}$处连续.

由命题1.3.11可知实值凸函数必然是闭函数.对于一维的实值凸函数，有如下更强的结论.

**命题1.3.12**：设$C$是实数轴上的闭区间，若函数$f: C \mapsto \mathbb{R}$是闭凸函数，则$f$在$C$上连续.

证明：由命题1.3.11知$f$在$ri(C)$上连续，故只需考虑边界点$\bar{x}$，设序列$\{ x_k \} \subseteq C$收敛到$\bar{x}$，并记$$\begin{align*}x_k = \alpha_k x_0 + (1 - \alpha_k) \bar{x}, \ \forall k,\end{align*}$$其中$\{ \alpha_k \}$是非负序列且$\alpha_k \rightarrow 0$，由$f$的凸性知$$\begin{align*}f(x_k) \leq \alpha_k f(x_0) + (1 - \alpha_k) f(\bar{x}),\end{align*}$$当$k \rightarrow \infty$时可得$$\begin{align*}\limsup_{k \rightarrow \infty} f(x_k) \leq f(\bar{x}).\end{align*}$$考虑扩展实值函数$\tilde{f}(x): \mathbb{R} \mapsto [-\infty, \infty]$：$$\begin{align*} \tilde{f}(x) = \begin{cases} f(x) & x \in C  \\ \infty & x \not \in C. \end{cases} \end{align*}$$由于$f$是闭函数，故其上境图是闭集，又$\tilde{f}$和$f$有相同的上境图，故$\tilde{f}$是闭函数，由命题1.1.6知$\tilde{f}$下半连续，于是$$\begin{align*}f(\bar{x}) \leq \liminf_{k \rightarrow \infty} f(x_k),\end{align*}$$这意味着$f(x_k) \rightarrow f(\bar{x})$，故$f$在$\bar{x}$处连续.

之前我们介绍了将非凸集进行凸化，同样对于非闭凸函数，我们考虑将其闭凸化.

函数$f: X \mapsto [-\infty, \infty]$的上境图的闭包可以看做另一个函数的上境图，该函数称作$f$的闭包，记作$$\begin{align*} cl(f)(\boldsymbol{x}) = \inf \{ w \ \vert \ (\boldsymbol{x}, w) \in cl(epi(f)) \}, \ \boldsymbol{x} \in \mathbb{R}^n. \end{align*}$$

函数$f: X \mapsto [-\infty, \infty]$的上境图的凸包可以看做另一个函数的上境图，该函数称作$f$的凸包，记作$$\begin{align*}conv(f)(\boldsymbol{x}) = \inf \{ w \ \vert \ (\boldsymbol{x}, w) \in conv(epi(f)) \}, \ \boldsymbol{x} \in \mathbb{R}^n.\end{align*}$$

函数$f: X \mapsto [-\infty, \infty]$的上境图的闭凸包可以看做另一个函数的上境图，该函数称作$f$的闭凸包，记作$$\begin{align*}cl(conv(f))(\boldsymbol{x}) = \inf \{ w \ \vert \ (\boldsymbol{x}, w) \in cl(conv(epi(f))) \}, \ \boldsymbol{x} \in \mathbb{R}^n.\end{align*}$$

显然$cl(conv(f))(\boldsymbol{x})$是$cl(f)(\boldsymbol{x})$的凸包，是$conv(f)(\boldsymbol{x})$的闭包.下面这个命题说明了闭凸包的一个重要性质：$cl(conv(f))$的下确界与$f$是一致的，且$f$能取到下确界的点也可使$cl(conv(f))(\boldsymbol{x})$取到下确界.因此当优化目标不是闭凸函数时，我们可以考虑去优化它的闭凸包.

**命题1.3.13**：设函数$f: X \mapsto [-\infty, \infty]$，那么

$$\begin{align} \label{equ: coincide of convex closure} \inf_{\boldsymbol{x} \in X} f(\boldsymbol{x}) = \inf_{\boldsymbol{x} \in X} cl(f)(\boldsymbol{x}) = \inf_{\boldsymbol{x} \in \mathbb{R}^n} cl(f)(\boldsymbol{x}) = \inf_{\boldsymbol{x} \in \mathbb{R}^n} conv(f)(\boldsymbol{x}) = \inf_{\boldsymbol{x} \in \mathbb{R}^n} cl(conv(f))(\boldsymbol{x}), \end{align}$$

此外，使得$f$取下确界的$\boldsymbol{x}$，同样可使$cl(f)$，$conv(f)$和$cl(conv(f))$取得下确界.

证明：若$epi(f)$是空集，即$f$恒取$\infty$，结论显然成立，不妨设$epi(f)$非空，记$f^* = \inf_{\boldsymbol{x} \in \mathbb{R}^n} cl(f)(\boldsymbol{x})$. 对于任意序列$\{ (\bar{\boldsymbol{x}}_k, \bar{w}_k) \} \subseteq cl(epi(f))$且$\bar{w}_k \rightarrow f^*$，构造序列$\{ (\boldsymbol{x}_k, w_k) \} \subseteq epi(f)$使得$\vertw_k - \bar{w}_k\vert \rightarrow 0$，即$w_k \rightarrow f^*$，又$f(\boldsymbol{x}_k) \leq w_k$，故对于$\forall \boldsymbol{x} \in X$有$$\begin{align*}\inf_{\boldsymbol{x} \in X} f(\boldsymbol{x}) = \limsup_{k \rightarrow \infty} \inf_{\boldsymbol{x} \in X} f(\boldsymbol{x}) \leq \limsup_{k \rightarrow \infty} f(\boldsymbol{x}_k) \leq \limsup_{k \rightarrow \infty} w_k = f^* \leq cl(f)(\boldsymbol{x}) \leq f(\boldsymbol{x}),\end{align*}$$于是对$\boldsymbol{x} \in X$取下确界可知有$$\begin{align*}\inf_{\boldsymbol{x} \in X} f(\boldsymbol{x}) = \inf_{\boldsymbol{x} \in X} cl(f)(\boldsymbol{x}) = \inf_{\boldsymbol{x} \in \mathbb{R}^n} cl(f)(\boldsymbol{x}).\end{align*}$$

选取序列$\{ (\boldsymbol{x}_k, w_k)\} \subseteq conv(epi(f))$且$w_k \rightarrow \inf_{\boldsymbol{x} \in \mathbb{R}^n} conv(f)(\boldsymbol{x})$.一方面，由于$\{ (\boldsymbol{x}_k, w_k) \}$是$epi(f)$中向量的凸组合，故$w_k \geq f(\boldsymbol{x}_k) \geq \inf_{\boldsymbol{x} \in X} f(\boldsymbol{x})$，于是对$k$取极限有$\inf_{\boldsymbol{x} \in \mathbb{R}^n} conv(f)(\boldsymbol{x}) \geq \inf_{\boldsymbol{x} \in X} f(\boldsymbol{x})$.另一方面，对于$\forall \boldsymbol{x} \in X$有$conv(f)(\boldsymbol{x}) \leq f(\boldsymbol{x})$，故$\inf_{\boldsymbol{x} \in \mathbb{R}^n} conv(f)(\boldsymbol{x}) \leq \inf_{\boldsymbol{x} \in X} conv(f)(\boldsymbol{x}) \leq \inf_{\boldsymbol{x} \in X} f(\boldsymbol{x})$，于是$\inf_{\boldsymbol{x} \in \mathbb{R}^n} conv(f)(\boldsymbol{x}) = \inf_{\boldsymbol{x} \in X} f(\boldsymbol{x})$.

又$cl(conv(f))$是$conv(f)$的闭包，由前面的证明知$\inf_{\boldsymbol{x} \in \mathbb{R}^n} conv(f)(\boldsymbol{x}) = \inf_{\boldsymbol{x} \in \mathbb{R}^n} cl(conv(f))(\boldsymbol{x})$.

综上式(\ref{equ: coincide of convex closure})得证.

设$f$在$\boldsymbol{x}^*$处取得下确界，又对于$\forall \boldsymbol{x} \in X$有$f(\boldsymbol{x}) \geq cl(f)(\boldsymbol{x})$，于是$$\begin{align*}\inf_{\boldsymbol{x} \in \mathbb{R}^n} cl(f)(\boldsymbol{x}) = \inf_{\boldsymbol{x} \in X} f(\boldsymbol{x}) = f(\boldsymbol{x}^*) \geq cl(f)(\boldsymbol{x}^*),\end{align*}$$即$cl(f)$也在$\boldsymbol{x}^*$处取得下确界.同理可证$conv(f)$和$cl(conv(f))$也在$\boldsymbol{x}^*$处取得下确界.

下面这个命题说明一个函数的闭凸包是对原函数“最紧”的放松.

**命题1.3.14**：设函数$f: \mathbb{R}^n \mapsto [-\infty, \infty]$，那么

$cl(f)$是$f$最紧的闭函数，即若$g: \mathbb{R}^n \mapsto [-\infty, \infty]$是闭函数且对于$\forall \boldsymbol{x} \in \mathbb{R}^n$有$g(\boldsymbol{x}) \leq f(\boldsymbol{x})$，那么对于$\forall \boldsymbol{x} \in \mathbb{R}^n$有$g(\boldsymbol{x}) \leq cl(f)(\boldsymbol{x})$.
$cl(conv(f))$是$f$最紧的闭凸函数，即若$g: \mathbb{R}^n \mapsto [-\infty, \infty]$是闭凸函数且对于$\forall \boldsymbol{x} \in \mathbb{R}^n$有$g(\boldsymbol{x}) \leq f(\boldsymbol{x})$，那么对于$\forall \boldsymbol{x} \in \mathbb{R}^n$有$g(\boldsymbol{x}) \leq cl(conv(f))(\boldsymbol{x})$.
证明：

易知$epi(f) \in epi(g)$且$epi(g)$是闭集，故$epi(cl(f)) = cl(epi(f)) \subseteq cl(epi(g)) = epi(g)$，这意味着对于$\forall \boldsymbol{x} \in \mathbb{R}^n$有$g(\boldsymbol{x}) \leq cl(f)(\boldsymbol{x})$.
易知$epi(f) \in epi(g)$且$epi(g)$是闭凸集，故$epi(cl(conv(f))) = cl(conv(epi(f))) \subseteq cl(conv(epi(g))) = epi(g)$，这意味着对于$\forall \boldsymbol{x} \in \mathbb{R}^n$有$g(\boldsymbol{x}) \leq cl(conv(f))(\boldsymbol{x})$. 
\end{proof}
下面这个命题刻画了凸函数与其闭包的关系，之前我们证明了凸函数在其有效定义域的相对内部是连续的，也即闭的，因此凸函数与其闭包在其有效定义域的相对内部应该是完全一样的，唯一可能不一样的就是有效定义域的边界.

**命题1.3.15**：设$f: \mathbb{R}^n \mapsto [-\infty, \infty]$是凸函数，那么

$cl(dom(f)) = cl(dom(cl(f)))$，$ri(dom(f)) = ri(dom(cl(f)))$，对于$\forall \boldsymbol{x} \in ri(dom(f))$有$cl(f)(\boldsymbol{x}) = f(\boldsymbol{x})$，$cl(f)$是正常凸函数当且仅当$f$是正常凸函数.
若$\boldsymbol{x} \in ri(dom(f))$，则对于$\boldsymbol{y} \in \mathbb{R}^n$有$$\begin{align*} cl(f)(\boldsymbol{y}) = \lim_{\alpha \rightarrow 0} f(\boldsymbol{y} + \alpha (\boldsymbol{x} - \boldsymbol{y})). \end{align*}$$
证明：

易知$$\begin{align*} ri(epi(f)) & = \{ (\boldsymbol{x}, w) \ \vert \ \boldsymbol{x} \in ri(dom(f)), f(\boldsymbol{x}) < w \}, \\ ri(epi(cl(f))) & = \{ (\boldsymbol{x}, w) \ \vert \ \boldsymbol{x} \in ri(dom(cl(f))), cl(f)(\boldsymbol{x}) < w \}. \end{align*}$$因为$epi(f)$和$epi(cl(f))$有相同的闭包，由命题1.3.5(c)知它们有相同的相对内部，故$$\begin{align*}\{ (\boldsymbol{x}, w) \ \vert \ \boldsymbol{x} \in ri(dom(f)), f(\boldsymbol{x}) < w \} = \{ (\boldsymbol{x}, w) \ \vert \ \boldsymbol{x} \in ri(dom(cl(f))), cl(f)(\boldsymbol{x}) < w \}，\end{align*}$$这意味着$ri(dom(f)) = ri(dom(cl(f)))$，即$dom(f)$和$dom(cl(f))$有相同的相对内部，再次由命题1.3.5(c)知它们有相同的闭包，故$cl(dom(f)) = cl(dom(cl(f)))$.于是有$$\begin{align*}\{ (\boldsymbol{x}, w) \ \vert \ \boldsymbol{x} \in ri(dom(f)), f(\boldsymbol{x}) < w \} = \{ (\boldsymbol{x}, w) \ \vert \ \boldsymbol{x} \in ri(dom(f)), cl(f)(\boldsymbol{x}) < w \},\end{align*}$$由此可得对于$\forall \boldsymbol{x} \in ri(dom(f))$有$cl(f)(\boldsymbol{x}) = f(\boldsymbol{x})$. 
若$cl(f)$是正常凸函数，则$f$显然是正常凸函数；若$f$是正常凸函数，反设$cl(f)$不是正常凸函数，则易知有$$\begin{align*}cl(f)(\boldsymbol{x}) = \begin{cases}  -\infty & \boldsymbol{x} \in dom(cl(f)), \\ \infty & \boldsymbol{x} \not \in dom(cl(f)).\end{cases}\end{align*}$$于是对于$\forall \boldsymbol{x} \in ri(dom(cl(f)))$有$f(\boldsymbol{x}) = cl(f)(\boldsymbol{x}) = -\infty$，这意味着$f$不是正常凸函数，矛盾.
若$\boldsymbol{y} \not \in dom(cl(f))$，则$cl(f)(\boldsymbol{y}) = \infty$，由$cl(f)$的下半连续性知对于任意收敛于$\boldsymbol{y}$的序列$\{\boldsymbol{y}_k\}$有$$\begin{align*}\infty = cl(f)(\boldsymbol{y}) \leq \liminf_{k \rightarrow \infty} cl(f)(\boldsymbol{y}_k),\end{align*}$$这意味着$cl(f)(\boldsymbol{y}_k) \rightarrow \infty$，又$cl(f)(\boldsymbol{y}_k) \leq f(\boldsymbol{y}_k)$，故$f(\boldsymbol{y}_k) \rightarrow \infty$，于是$cl(f)(\boldsymbol{y}) = \lim_{\alpha \rightarrow 0} f(\boldsymbol{y} + \alpha (\boldsymbol{x} - \boldsymbol{y})) = \infty$. 
若$\boldsymbol{y} \in dom(cl(f))$，考虑函数$g: [0, 1] \mapsto \mathbb{R}$：$$\begin{align*}g(\alpha) = cl(f)(\boldsymbol{y} + \alpha(\boldsymbol{x} - \boldsymbol{y})).\end{align*}$$由于$\boldsymbol{x} \in ri(dom(f)) = ri(dom(cl(f)))$，$\boldsymbol{y} \in dom(cl(f))$，由命题1.3.1知对于$\alpha \in (0, 1]$有$$\begin{align*}\boldsymbol{y} + \alpha(\boldsymbol{x} - \boldsymbol{y}) \in ri(dom(cl(f))),\end{align*}$$由(1)知$\boldsymbol{y} + \alpha(\boldsymbol{x} - \boldsymbol{y}) \in ri(dom(f))$，于是$$\begin{align} \label{equ: closure of convex function}g(\alpha) = cl(f)(\boldsymbol{y} + \alpha(\boldsymbol{x} - \boldsymbol{y})) = f(\boldsymbol{y} + \alpha(\boldsymbol{x} - \boldsymbol{y})).\end{align}$$
若$cl(f)(\boldsymbol{y}) = -\infty$，那么$cl(f)$不是正常凸函数，于是对于$\forall \boldsymbol{z} \in dom(cl(f))$有$cl(f)(\boldsymbol{z}) = -\infty$，因此$$\begin{align*}f(\boldsymbol{y} + \alpha(\boldsymbol{x} - \boldsymbol{y})) = -\infty, \ \forall \alpha \in (0, 1],\end{align*}$$结论成立. 
若$cl(f)(\boldsymbol{y}) > -\infty$，那么$cl(f)$是正常闭凸函数，于是$g$是$[0, 1]$上的实值闭凸函数，由命题1.3.12知，$g$在$[0, 1]$上连续，对式(\ref{equ: closure of convex function})取极限知$$\begin{align*}cl(f)(\boldsymbol{y}) = g(0) = \lim_{\alpha \rightarrow 0} g(\alpha) = \lim_{\alpha \rightarrow 0} f(\boldsymbol{y} + \alpha(\boldsymbol{x} - \boldsymbol{y})).\end{align*}$$
以前证明过非正常闭凸函数$f: \mathbb{R}^n \mapsto [-\infty, \infty]$必呈如下形式：$$\begin{align*} f(\boldsymbol{x}) = \begin{cases} -\infty & \boldsymbol{x} \in dom(f), \\ \infty & \boldsymbol{x} \not \in dom(f). \end{cases} \end{align*}$$现在考虑任意非正常凸函数$f$，由命题1.3.15(a)知$cl(f)$也是非正常凸函数，故$cl(f)$是非正常闭凸函数，那么$cl(f)$在$dom(cl(f))$上恒取$-\infty$，又由命题1.3.15(a)知在$ri(dom(f))$上有$cl(f)(\boldsymbol{x}) = f(\boldsymbol{x})$，故$f$在$ri(dom(f))$上恒取$-\infty$.

下面这个命题给出了凸函数线性复合后的闭包等于其闭包的线性复合的条件.

**命题1.3.16**：设$f: \mathbb{R}^m \mapsto [-\infty, \infty]$是凸函数，矩阵$\boldsymbol{A} \in \mathbb{R}^{m \times n}$且存在$\mathit{Col}(\boldsymbol{A}) \cap ri(dom(f))$非空，则函数$$\begin{align*}F(\boldsymbol{x}) = f(\boldsymbol{A}\boldsymbol{x}),\end{align*}$$是凸函数且对于$\forall \boldsymbol{x} \in \mathbb{R}^n$有$cl(F)(\boldsymbol{x}) = cl(f)(\boldsymbol{A}\boldsymbol{x})$.

证明：由命题1.1.8知$F$是凸函数，设$\boldsymbol{z} \in \mathit{Col}(\boldsymbol{A}) \cap ri(dom(f))$，于是存在$\boldsymbol{y}$满足$\boldsymbol{A}\boldsymbol{y} = \boldsymbol{z} \in ri(dom(f))$，即$\boldsymbol{y} \in \boldsymbol{A}^{-1} \cdot ri(dom(f))$(注意这里$\boldsymbol{A}^{-1}$是线性变换$\boldsymbol{A}$的逆变换，不是逆矩阵的意思).显然$dom(F) = \boldsymbol{A}^{-1} \cdot dom(f)$，由命题1.3.9知$ri(dom(F)) = \boldsymbol{A}^{-1} \cdot ri(dom(f))$，故$\boldsymbol{y} \in ri(dom(F))$，由命题1.3.15(b)知对于$\forall \boldsymbol{x} \in \mathbb{R}^n$有$$\begin{align*}cl(F)(\boldsymbol{x}) = \lim_{\alpha \rightarrow 0} F(\boldsymbol{x} + \alpha (\boldsymbol{y} - \boldsymbol{x})) = \lim_{\alpha \rightarrow 0} f(\boldsymbol{A}\boldsymbol{x} + \alpha (\boldsymbol{A}\boldsymbol{y} - \boldsymbol{A}\boldsymbol{x})) = cl(f)(\boldsymbol{A} \boldsymbol{x}).\end{align*}$$

下面这个命题可以看成命题1.3.16的一个特例.

**命题1.3.17**：设$f_i: \mathbb{R}^n \mapsto [-\infty, \infty], i = 1, \dots, m$是凸函数且$\cap_{i=1}^m ri(dom(f_i)) \neq \emptyset$，则函数$$\begin{align*}F(\boldsymbol{x}) = f_1(\boldsymbol{x}) + \dots + f_m(\boldsymbol{x})\end{align*}$$是凸函数且对于$\forall \boldsymbol{x} \in \mathbb{R}^n$有$cl(f)(\boldsymbol{x}) = cl(f_1)(\boldsymbol{x}) + \dots + cl(f_m)(\boldsymbol{x})$.

证明：将$F$写成$F(\boldsymbol{x}) = f(\boldsymbol{A}\boldsymbol{x})$，其中矩阵$\boldsymbol{A} = [\boldsymbol{I}_n, \dots, \boldsymbol{I}_n]^\top \in \mathbb{R}^{mn \times n}$，定义函数$f: \mathbb{R}^{mn} \mapsto (-\infty, \infty]$如下：$$\begin{align*}f([\boldsymbol{x}_1^\top, \dots, \boldsymbol{x}_m^\top]^\top) = f_1(\boldsymbol{x}_1) + \dots + f_m (\boldsymbol{x}_m)\end{align*}$$易知$dom(F) = \cap_{i=1}^m dom(f_i)$，于是由命题1.3.8和命题1.3.9知$$\begin{align*}\emptyset \neq \cap_{i=1}^m ri(dom(f_i)) = ri(\cap_{i=1}^m dom(f_i)) = ri(dom(F)) = ri(\boldsymbol{A}^{-1} \cdot dom(f)) = \boldsymbol{A}^{-1} \cdot ri(dom(f))\end{align*}$$这意味着$\mathit{Col}(\boldsymbol{A}) \cap ri(dom(f))$非空，由命题命题1.3.16知$$\begin{align*}cl(F)(\boldsymbol{x}) = cl(f)(\boldsymbol{A}\boldsymbol{x}).\end{align*}$$设$\boldsymbol{y} \in \cap_{i=1}^m ri(dom(f_i))$，于是$[\boldsymbol{y}^\top, \dots, \boldsymbol{y}^\top]^\top \in ri(dom(f))$，由命题1.3.15(b)知$$\begin{align*}cl(f)(\boldsymbol{x}) & = cl(f)([\boldsymbol{x}^\top, \dots, \boldsymbol{x}^\top]^\top)  \\ & = \lim_{\alpha \rightarrow 0} f_1(\boldsymbol{x} + \alpha (\boldsymbol{y} - \boldsymbol{x})) + \dots + \lim_{\alpha \rightarrow 0} f_m(\boldsymbol{x} + \alpha (\boldsymbol{y} - \boldsymbol{x}))   \\ & = cl(f_1)(\boldsymbol{x}) + \dots + cl(f_m)(\boldsymbol{x}) \end{align*}$$


[C1S3-pic1]: {{"/assets/images/C1S3-pic1.png" | site.baseurl }}
[C1S3-pic2]: {{"/assets/images/C1S3-pic2.png" | site.baseurl }}
[C1S3-pic3]: {{"/assets/images/C1S3-pic3.png" | site.baseurl }}
[C1S3-pic4]: {{"/assets/images/C1S3-pic4.png" | site.baseurl }}

