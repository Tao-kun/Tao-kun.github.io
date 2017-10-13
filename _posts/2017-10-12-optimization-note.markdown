---
layout: post
title:  "《凸优化理论》笔记"
date:   2017-10-12 18:04:00 +0800
tags: [Mathematics]
---

# C1S1 - 凸集和凸函数
在优化问题中，凸集(convex set)和凸函数(convex function)是很常见的，它们有一些特殊的结构，通过利用这些结构，可以为设计算法带来很多便利.例如每一个闭凸集都可以看成一系列半空间的交集，以后会提到的割平面法(cutting plane method)就是基于这个想法提出的.但尽管如此，对它们做理论分析却并不容易，因为总有很多例外的情况，使问题变得复杂，例如闭凸集在线性变换下不一定能保持闭凸性(仿射集(affine set)和紧集(compact set)就没有这个问题)，这时最优解是否存在，我们就不能想当然了.因此，我们有必要建立严格的理论来对其进行研究，这自然免不了要定义很多新的概念，本节主要引入凸集和凸函数的概念，以及一些相关的分析.

![C1S1 Pic1][C1S1-pic1]

**定义1.1.1**：集合$C$是$\mathbb{R}^n$的子集，如果对于$\forall \boldsymbol{x}, \boldsymbol{y} \in C$和$\forall \alpha \in [0, 1]$，有 

$$
\begin{align*}
\alpha \boldsymbol{x} + (1 - \alpha) \boldsymbol{y} \in C
\end{align*}
$$

成立，则称集合$C$是凸的.

我们约定空集也是凸集.直观上来说，一个集合若是凸集，它会给人“鼓鼓”的感觉，中间永远不会低于两边，如右图所示.

**命题1.1.2**：以下操作可以保持集合得凸性：

1. 两个凸集$C_1$和$C_2$的交集$C_1 \cap C_2$是凸集.

2. 两个凸集$C_1$和$C_2$中的元素的向量和$C_1 + C_2$组成的集合是凸集.

3. 对于任意凸集$C$和标量$\lambda$，$\lambda C$是凸集.

4. 凸集$C$的闭包$cl(C)$和内部$int(C)$都是凸集.

5. 凸集$C$在仿射变换(affine transformation)下的象(img(C))和原象(invimg(C))都是凸集.

**证明**：

1. 对于$\forall \boldsymbol{x}, \boldsymbol{y} \in C_1 \cap C_2$，易知有$\boldsymbol{x}, \boldsymbol{y} \in C_1$和$\boldsymbol{x}, \boldsymbol{y} \in C_2$.由$C_1$和$C_2$的凸性知对于$\forall \alpha \in [0, 1]$有

$$
\begin{align*}
\alpha \boldsymbol{x} + (1 - \alpha) \boldsymbol{y} & \in C_1, \\
\alpha \boldsymbol{x} + (1 - \alpha) \boldsymbol{y} & \in C_2
\end{align*}
$$

故

$$
\begin{align*}
\alpha \boldsymbol{x} + (1 - \alpha) \boldsymbol{y} \in C_1 \cap C_2
\end{align*}
$$


2. 对于$\forall \boldsymbol{x}, \boldsymbol{y} \in C_1 + C_2$，易知存在$\boldsymbol{x}_1, \boldsymbol{y}_1 \in C_1$和$\boldsymbol{x}_2, \boldsymbol{y}_2 \in C_2$满足$\boldsymbol{x} = \boldsymbol{x}_1 + \boldsymbol{x}_2$和$\boldsymbol{y} = \boldsymbol{y}_1 + \boldsymbol{y}_2$，于是对于$\forall \alpha \in [0, 1]$有

$$
\begin{align*}
\alpha \boldsymbol{x} + (1 - \alpha) \boldsymbol{y} 
= \alpha (\boldsymbol{x}_1 + \boldsymbol{x}_2) + (1 - \alpha) (\boldsymbol{y}_1 + \boldsymbol{y}_2) 
= \left( \alpha \boldsymbol{x}_1 + (1 - \alpha) \boldsymbol{y}_1 \right) + \left( \alpha \boldsymbol{x}_2 + (1 - \alpha) \boldsymbol{y}_2 \right),
\end{align*}
$$

由$C_1$和$C_2$的凸性知$\alpha \boldsymbol{x}_1 + (1 - \alpha) \boldsymbol{y}_1 \in C_1$和$\alpha \boldsymbol{x}_2 + (1 - \alpha) \boldsymbol{y}_2 \in C_2$，故$\alpha \boldsymbol{x} + (1 - \alpha) \boldsymbol{y} \in C_1 + C_2$.
对于$\forall \boldsymbol{x}, \boldsymbol{y} \in \lambda C$，易知存在$\boldsymbol{x}_1, \boldsymbol{y}_1 \in C$满足$\boldsymbol{x} = \lambda \boldsymbol{x}_1$和$\boldsymbol{y} = \lambda \boldsymbol{y}_1$，于是对于$\forall \alpha \in [0, 1]$有$$\begin{align*}\alpha \boldsymbol{x} + (1 - \alpha) \boldsymbol{y} = \lambda \alpha \left( \boldsymbol{x}_1 + (1 - \alpha) \boldsymbol{y}_1 \right),\end{align*}$$由$C$的凸性知$\alpha \boldsymbol{x}_1 + (1 - \alpha) \boldsymbol{y}_1 \in C$，故$\alpha \boldsymbol{x} + (1 - \alpha) \boldsymbol{y} \in \lambda C$.

3. 对于$\forall \boldsymbol{x}, \boldsymbol{y} \in cl(C)$，易知存在序列$\{ \boldsymbol{x}_k \}, \{ \boldsymbol{y}_k \} \in C$满足$\boldsymbol{x}_k \rightarrow \boldsymbol{x}$和$\boldsymbol{y}_k \rightarrow \boldsymbol{y}$.对于$\forall \alpha \in [0, 1]$，由$C$的凸性知序列$\{ \alpha \boldsymbol{x}_k + (1 - \alpha) \boldsymbol{y}_k \} \in C$，于是该序列的极限$\alpha \boldsymbol{x} + (1 - \alpha) \boldsymbol{y} \in cl(C)$. 

4. 对于$\forall \boldsymbol{x}, \boldsymbol{y} \in int(C)$，易知存在以$\boldsymbol{x}, \boldsymbol{y}$为球心半径为$r$的开球$B(\boldsymbol{x}, r) \subseteq C$和$B(\boldsymbol{y}, r) \subseteq C$. 考虑开球$B(\alpha \boldsymbol{x} + (1 - \alpha) \boldsymbol{y}, r)$中的任意一点$\alpha \boldsymbol{x} + (1 - \alpha) \boldsymbol{y} + \boldsymbol{z}$，其中
$\|z\| < r$
，易知有

$$
\begin{align*}
\alpha \boldsymbol{x} + (1 - \alpha) \boldsymbol{y} + \boldsymbol{z}
= \alpha (\boldsymbol{x} + \boldsymbol{z}) + (1 - \alpha) (\boldsymbol{y} + \boldsymbol{z})
\end{align*}
$$

因为$(\boldsymbol{x} + \boldsymbol{z}) \in B(\boldsymbol{x}, r) \subseteq C$，$(\boldsymbol{y} + \boldsymbol{z}) \in B(\boldsymbol{y}, r) \subseteq C$，故$\alpha \boldsymbol{x} + (1 - \alpha) \in C$.
设仿射变换对应的矩阵为$\boldsymbol{A}$.对于$\forall \boldsymbol{x}, \boldsymbol{y} \in img(C)$，易知存在$\boldsymbol{x}_1, \boldsymbol{y}_1 \in C$满足$\boldsymbol{A} \boldsymbol{x}_1 = \boldsymbol{x}$和$\boldsymbol{A} \boldsymbol{y}_1 = \boldsymbol{y}$，于是对于$\forall \alpha \in [0, 1]$有

$$
\begin{align*}
\alpha \boldsymbol{x} + (1 - \alpha) \boldsymbol{y} 
= \alpha \boldsymbol{A} \boldsymbol{x}_1 + (1 - \alpha) \boldsymbol{A} \boldsymbol{y}_1
= \boldsymbol{A} (\alpha \boldsymbol{x}_1 + (1 - \alpha) \boldsymbol{y}_1)
\end{align*}
$$

由$C$的凸性知$\alpha \boldsymbol{x}_1 + (1 - \alpha) \boldsymbol{y}_1 \in C$，故$\alpha \boldsymbol{x} + (1 - \alpha) \boldsymbol{y} \in img(C)$. 

对于$\forall \boldsymbol{x}, \boldsymbol{y} \in invimg(C)$，易知存在$\boldsymbol{x}_1, \boldsymbol{y}_1 \in C$满足$\boldsymbol{A} \boldsymbol{x} = \boldsymbol{x}_1$和$\boldsymbol{A} \boldsymbol{y} = \boldsymbol{y}_1$，即$\boldsymbol{A}^{-1} \boldsymbol{x}_1 = \boldsymbol{x}$和$\boldsymbol{A}^{-1} \boldsymbol{y}_1 = \boldsymbol{y}$，于是对于$\forall \alpha \in [0, 1]$有

$$
\begin{align*}
\alpha \boldsymbol{x} + (1 - \alpha) \boldsymbol{y}
= \alpha \boldsymbol{A}^{-1} \boldsymbol{x}_1 + (1 - \alpha) \boldsymbol{A}^{-1} \boldsymbol{y}_1
= \boldsymbol{A}^{-1} (\alpha \boldsymbol{x}_1 + (1 - \alpha) \boldsymbol{y}_1)
\end{align*}
$$

由$C$的凸性知$\alpha \boldsymbol{x}_1 + (1 - \alpha) \boldsymbol{y}_1 \in C$，故$\alpha \boldsymbol{x} + (1 - \alpha) \boldsymbol{y} \in invimg(C)$.
下面介绍一些特殊的凸集.一个**超平面** (**hyperplane**)对应如下形式的线性方程，

$$
\begin{align*}
\{ \boldsymbol{x} \vert \boldsymbol{a}^\top \boldsymbol{x} = b \}
\end{align*}
$$

其中$\boldsymbol{a}$是一个$\mathbb{R}^n$中的非零向量，$b$是一个标量，显然超平面是凸的.

5. 对于$\forall \boldsymbol{x}, \boldsymbol{y} \in invimg(C)$，易知存在$\boldsymbol{x}_1, \boldsymbol{y}_1 \in C$满足$\boldsymbol{A} \boldsymbol{x} = \boldsymbol{x}_1$和$\boldsymbol{A} \boldsymbol{y} = \boldsymbol{y}_1$，即$\boldsymbol{A}^{-1} \boldsymbol{x}_1 = \boldsymbol{x}$和$\boldsymbol{A}^{-1} \boldsymbol{y}_1 = \boldsymbol{y}$，于是对于$\forall \alpha \in [0, 1]$有

$$
\begin{align*}
\alpha \boldsymbol{x} + (1 - \alpha) \boldsymbol{y}
= \alpha \boldsymbol{A}^{-1} \boldsymbol{x}_1 + (1 - \alpha) \boldsymbol{A}^{-1} \boldsymbol{y}_1
= \boldsymbol{A}^{-1} (\alpha \boldsymbol{x}_1 + (1 - \alpha) \boldsymbol{y}_1)
\end{align*}
$$

由$C$的凸性知$\alpha \boldsymbol{x}_1 + (1 - \alpha) \boldsymbol{y}_1 \in C$，故$\alpha \boldsymbol{x} + (1 - \alpha) \boldsymbol{y} \in invimg(C)$.

下面介绍一些特殊的凸集.

1.一个 **超平面** (**hyperplane**)对应如下形式的线性方程，

$$
\begin{align*}
\{ \boldsymbol{x} \vert \boldsymbol{a}^\top \boldsymbol{x} = b \}
\end{align*}
$$

其中$\boldsymbol{a}$是一个$\mathbb{R}^n$中的非零向量，$b$是一个标量，显然超平面是凸的.

2.一个**半空间** (**halfspace**)对应如下形式的线性不等式，

$$
\begin{align*}
\{ \boldsymbol{x} \vert \boldsymbol{a}^\top \boldsymbol{x} \leq b \}
\end{align*}
$$

其中$\boldsymbol{x}$是一个$\mathbb{R}^n$中的非零向量，$b$是一个标量，显然半平面是凸的.

3.有限个半空间的交集是**多面体** (**polyhedral**)，对应如下形式的线性不等式组，

$$
\begin{align*}
\{ \boldsymbol{x} \vert \boldsymbol{a}_j^\top \boldsymbol{x} \leq b_j, j = 1, \dots, r \}
\end{align*}
$$

其中$\boldsymbol{a}_1, \dots, \boldsymbol{a}_r$是$\mathbb{R}^n$中的非零向量，$b_1, \dots, b_r$是$\mathbb{R}$中的标量.由命题1.1.2(a)知多面体是凸的.

对于$\forall \boldsymbol{x} \in C$和$\forall \alpha > 0$，都有$\lambda \boldsymbol{x} \in C$，则称集合$C$是锥(cone).锥不一定是凸的，也不一定包含原点，但是非空锥的闭包(closure)必然包含原点.多面体锥(polyhedral cone)对应如下形式的线性不等式组，

$$
\begin{align*}
\{ \boldsymbol{x} \vert \boldsymbol{a}_j^\top \boldsymbol{x} \leq 0, j = 1, \dots, r \}
\end{align*}
$$

其中$\boldsymbol{a}_1, \dots, \boldsymbol{a}_r$是$\mathbb{R}^n$中的非零向量

$\mathbb{R}^n$的子空间是特殊的多面体锥，从而也是特殊的多面体.

下面给出凸函数的定义，参考右图.

![C1S1 Pic2][C1S1-pic2]

**定义1.1.3**：凸集$C$是$\mathbb{R}^n$的子集，如果对于$\forall \boldsymbol{x}, \boldsymbol{y} \in C$和$\forall \alpha \in [0, 1]$有

$$
\begin{align*}
f(\alpha \boldsymbol{x} + (1 - \alpha) \boldsymbol{y}) \leq \alpha f(\boldsymbol{x}) + (1 - \alpha) f(\boldsymbol{y})
\end{align*}
$$

成立，则称$f: C \mapsto \mathbb{R}$是实值凸函数(real-valued convex function).

当我们说一个函数是凸函数时，暗指了它的定义域(domain)也是凸的.显然仿射函数是凸函数，另一个例子是范数
$\|\cdot\|$
，因为三角不等式保证了它的凸性.

对于任意函数$f: C \mapsto \mathbb{R}$和标量$\gamma$，集合$\{ \boldsymbol{x} \in C \vert f(\boldsymbol{x}) \leq \gamma \}$和$\{ \boldsymbol{x} \in C \vert f(\boldsymbol{x}) < \gamma \}$称为$f$的 水平集 (level sets)，也即作一个水平面与$f$相交，落在水平面下方的那部分对应的$\boldsymbol{x}$就组成了**水平集**.凸函数$f: C \mapsto \mathbb{R}$的所有水平集都是凸的.考虑水平集$S = \{ \boldsymbol{x} \in C \vert f(\boldsymbol{x}) \leq \gamma \}$，对于$\forall \boldsymbol{x}, \boldsymbol{y} \in S$和$\forall \alpha \in [0, 1]$，由$S$的定义和$f$的凸性知

$$
\begin{align*}
f(\alpha \boldsymbol{x} + (1 - \alpha) \boldsymbol{y}) \leq \alpha f(\boldsymbol{x}) + (1 - \alpha) f(\boldsymbol{y}) \leq \alpha \gamma + (1 - \alpha) \gamma 
= \gamma
\end{align*}
$$

类似可证$\{ \boldsymbol{x} \in C \vert f(\boldsymbol{x}) < \gamma \}$
也是凸的.但是倒过来是**不成立**的，例如函数$f(\boldsymbol{x}) = \sqrt{\vert\boldsymbol{x}\vert}$的水平集是凸的，但是该函数不是凸的.

![C1S1 Pic3][C1S1-pic3]

之前我们定义函数都特指实值凸函数，即从$C$到$\mathbb{R}$的映射，但为了方便，我们更希望函数是在定义在整个空间$\mathbb{R}^n$上的，此外我们还希望函数可以取值$+\infty$，这在后面的共轭函数和对偶问题里很常见.因此对于这样的$f: C \mapsto \mathbb{R}$，我们将考虑其对应的扩展实值函数(extended real-valued function)，即将定义域从$C$扩展到整个$\mathbb{R}^n$，不在$C$中时函数取值为$+\infty$. 做了这样的扩展后，产生了一个问题，无法再通过之前的定义1.1.3来判断一个扩展实值函数是否是凸函数，因为这涉及比较两个无穷大的数的大小问题.解决这个问题的办法是引入一个和凸函数息息相关概念，即它的上境图(epigraph)，如右图所示.

函数$f: X \mapsto \mathbb{R}$的上境图是$\mathbb{R}^{n+1}$的子集：

$$
\begin{align*}
epi(f) = \{ (\boldsymbol{x}, w) \vert \boldsymbol{x} \in X, w \in \mathbb{R}, f(\boldsymbol{x}) \leq w \}
\end{align*}
$$

函数$f$的有效定义域(effective domain)为

$$
\begin{align*}
dom(f) = \{ \boldsymbol{x} \in \mathbb{R}^n \vert f(\boldsymbol{x}) < + \infty \}
\end{align*}
$$

易知$dom(f)$是$epi(f)$在$\mathbb{R}^n$上的投影.

**命题1.1.4**：实值函数$f: C \mapsto \mathbb{R}$是凸函数当且仅当其上境图$epi(f)$是凸集.

**证明**：一方面，对于$\forall (\boldsymbol{x}, u), (\boldsymbol{y}, v) \in epi(f)$，即$f(\boldsymbol{x}) \leq u$和$f(\boldsymbol{y}) \leq v$成立.由$f$的凸性知对于$\forall \alpha \in [0, 1]$有

$$
\begin{align*}
f(\alpha \boldsymbol{x} + (1 - \alpha) \boldsymbol{y}) 
\leq \alpha f(\boldsymbol{x}) + (1 - \alpha) f(\boldsymbol{y}) 
\leq \alpha u + (1 - \alpha) v,
\end{align*}
$$

这意味着$(\alpha \boldsymbol{x} + (1 - \alpha) \boldsymbol{y}, \alpha u + (1 - \alpha) v) \in epi(f)$，又$(\alpha \boldsymbol{x} + (1 - \alpha) \boldsymbol{y}, \alpha u + (1 - \alpha) v) = \alpha (\boldsymbol{x}, u) + (1 - \alpha) (\boldsymbol{y}, v)$，故$epi(f)$是凸集.

另一方面，对于$\forall (\boldsymbol{x}, u), (\boldsymbol{y}, v) \in epi(f)$，即$f(\boldsymbol{x}) \leq u$和$f(\boldsymbol{y}) \leq v$成立，由$epi(f)$的凸性知对于$\forall \alpha \in [0, 1]$有

$$
\begin{align*}
(\alpha \boldsymbol{x} + (1 - \alpha) \boldsymbol{y}, \alpha u + (1 - \alpha) v) \in epi(f)
\end{align*}
$$

即$f(\alpha \boldsymbol{x} + (1 - \alpha) \boldsymbol{y}) \leq \alpha u + (1 - \alpha) v$，由于$(\boldsymbol{x}, f(\boldsymbol{x})), (\boldsymbol{y}, f(\boldsymbol{y})) \in epi(f)$，因此取$u = f(\boldsymbol{x})$及$v = f(\boldsymbol{y})$可得

$$
\begin{align*}
f(\alpha \boldsymbol{x} + (1 - \alpha) \boldsymbol{y}) 
\leq \alpha f(\boldsymbol{x}) + (1 - \alpha) f(\boldsymbol{y})
\end{align*}
$$

故$f$是凸函数.

不难发现，一个函数扩展后，其上境图并不会发生变化，因此我们可以通过上境图来定义扩展实值凸函数.

**定义1.1.5**：设$f: \mathbb{R}^n \mapsto [-\infty, \infty]$是扩展实值函数，如果$f$的上境图是$\mathbb{R}^{n+1}$的凸子集，则称$f$是扩展实值凸函数.

最后有两个退化的情况需要剔除掉：$f$恒取值$+\infty$，这对应于$epi(f)$是空集；$f$在某些点取值$-\infty$，这对应于$epi(f)$包含一条直线.如果函数$f$不恒取值$\infty$且恒不取值$-\infty$，则称$f$是正常(proper)的.

如果函数$f: X \mapsto [-\infty, \infty]$的上境图是闭集(closed set)，则称$f$是闭函数(closed function).对于$X$中的任意收敛于$\boldsymbol{x}$的序列$\{\boldsymbol{x}_k\}$，如果

$$
\begin{align*}
f(\boldsymbol{x}) \leq \liminf_{k \rightarrow \infty} f(\boldsymbol{x}_k)
\end{align*}
$$

则称$f$下半连续(lower semicontinuous).

闭函数的概念和下半连续是紧密相关的，直观上来说，如果闭函数不连续，在某点有个“跳跃”，那么在该点的取值应该取小的那个值.

**命题1.1.6**：对于函数$f: \mathbb{R}^n \mapsto [-\infty, \infty]$，如下3个条件是等价的：

1. 对于任意标量$\gamma$，水平集$S_\gamma = \{ \boldsymbol{x} \vert f(\boldsymbol{x}) \leq \gamma \}$是闭的.

2.$f$下半连续.

3.$epi(f)$是闭的.

**证明**：如果$f$恒取值$\infty$，那么结论显然成立.不失一般性，设至少存在一个$\boldsymbol{x} \in \mathbb{R}^n$使得$f(\boldsymbol{x}) < \infty$，即$epi(f)$非空，至少存在一个水平集非空.

1$\Rightarrow$2：反证法，假设存在收敛于
$\boldsymbol{x}bar$
的序列
$\{\boldsymbol{x}_k\}$
满足

$$
\begin{align*}
f(\boldsymbol{x}bar) > \liminf_{k \rightarrow \infty} f(\boldsymbol{x}_k)
\end{align*}
$$

那么选取$\gamma$使得

$$
\begin{align*}
f(\boldsymbol{x}bar) > \gamma > \liminf_{k \rightarrow \infty} f(\boldsymbol{x}_k)
\end{align*}
$$

于是存在序列
$\{\boldsymbol{x}_k\}$
的一个子序列
$\{\boldsymbol{x}_k\}_\mathcal{K}$
对于
$\forall k \in \mathcal{K}$
有
$f(\boldsymbol{x}_k) \leq \gamma$
，即
$\{\boldsymbol{x}_k\}_\mathcal{K} \subseteq S_\gamma$
，因为水平集
$S_\gamma$
是闭的，故
$\boldsymbol{x}bar \in S_\gamma$
，即
$f(\boldsymbol{x}bar) \leq \gamma$
，矛盾.

2$\Rightarrow$3：设
$epi(f)$
中的序列
$\{(\boldsymbol{x}_k, w_k)\}$
收敛于
$(\boldsymbol{x}bar, \bar{\boldsymbol{w}})$
，由上境图的定义知
$f(\boldsymbol{x}_k) \leq w_k$
，取极限令
$k \rightarrow \infty$
并结合下半连续的定义知

$$
\begin{align*}
f(\boldsymbol{x}bar)
\leq \liminf_{k \rightarrow \infty} f(\boldsymbol{x}_k)
= \lim_{k \rightarrow \infty} f(\boldsymbol{x}_k)
\leq \bar{\boldsymbol{w}}
\end{align*}
$$

因此，
$(\boldsymbol{x}bar, \bar{\boldsymbol{w}}) \in epi(f)$
，故
$epi(f)$
是闭的.

3$\Rightarrow$1：设水平集
$S_\gamma$
中的序列
$\{\boldsymbol{x}_k\}$
收敛于
$\boldsymbol{x}bar$
，于是对于
$\forall k$
有
$(\boldsymbol{x}_k, \gamma) \in epi(f)$
，因为
$epi(f)$
是闭的，故序列
$\{(\boldsymbol{x}_k, \gamma)\}$
的极限
$(\boldsymbol{x}bar, \gamma) \in epi(f)$
，即
$\boldsymbol{x}bar \in S_\gamma$
，故
$S_\gamma$
是闭的.

一般来说，闭性比下半连续更方便使用，因为下半连续是一个定义域有关的性质，例如函数$f: \mathbb{R}^n \mapsto (-\infty, \infty]$：

$$
\begin{align*}
f(x) =
\begin{cases}
0 & x \in (0, 1)  \\
\infty & x \not \in (0, 1)
\end{cases}
\end{align*}
$$

既不是闭的，也不是下半连续的，但是当限制定义域在$(0, 1)$上时，$f$就是下半连续的了.

**命题1.1.7**：对于函数$f: X \mapsto [-\infty, \infty]$，如果$dom(f)$是闭的且$f$对于$\forall \boldsymbol{x} \in dom(f)$均下半连续，则$f$是闭的.

**证明**：将定义域扩展为$\mathbb{R}^n$后，$f$即在整个$\mathbb{R}^n$上下半连续，于是由命题1.1.6知扩展后的$epi(f)$是闭的，又扩展并不会使上境图和有效定义域都不会发生变化，故扩展前的$epi(f)$也是闭的，即$f$是闭的.

根据上述命题可知，集合$X$的示性函数：

$$\begin{align*}
I_X(x) =
\begin{cases} 
0 & \boldsymbol{x} \in X \\
\infty & \boldsymbol{x} \not \in X
\end{cases}
\end{align*}
$$

是闭的当且仅当$X$是闭的.

更一般的，对于任意连续函数$f: \mathbb{R}^n \mapsto \mathbb{R}$，函数

$$
\begin{align*}
f_X(\boldsymbol{x}) =
\begin{cases}
f(\boldsymbol{x}) & \boldsymbol{x} \in X \\
\infty & \boldsymbol{x} \not \in X 
\end{cases}
\end{align*}
$$

是闭的当且仅当$X$是闭的.

非正常闭凸函数$f: \mathbb{R}^n \mapsto [-\infty, \infty]$必呈如下形式：

$$
\begin{align*}
f(\boldsymbol{x}) =
\begin{cases}
-\infty & \boldsymbol{x} \in dom(f) \\
\infty & \boldsymbol{x} \not \in dom(f)
\end{cases}
\end{align*}
$$

反证法，假设存在一点$\boldsymbol{x}$使得$f(\boldsymbol{x})$取有限值，由于$f$是非正常闭凸函数，故存在一点$\boldsymbol{x}bar$使得$f(\boldsymbol{x}bar) = - \infty$，由$f$的凸性知对于如下形式的所有点

$$
\begin{align*}
\boldsymbol{x}_k
= \frac{k-1}{k} \boldsymbol{x} + \frac{1}{k} \boldsymbol{x}bar, k = 1, 2, \dots
\end{align*}
$$

均有

$$
\begin{align*}
f(\boldsymbol{x}_k)
\leq \frac{k-1}{k} f(\boldsymbol{x}) + \frac{1}{k} f(\boldsymbol{x}bar)
= - \infty, k = 1, 2, \dots
\end{align*}
$$

因为$\boldsymbol{x}_k \rightarrow \boldsymbol{x}$，且$f$是闭的，这意味着$f(\boldsymbol{x}) = - \infty$，矛盾.

下面主要讨论保持函数凸性的操作，这样可以从几个已知凸性的简单函数出发，构造出复杂的凸函数，主要讨论一下3种操作：

1. 线性变换的复合.

2. 相加及非负标量乘.

3. 逐点取上确界.

**命题1.1.8**：给定函数$f: \mathbb{R}^m \mapsto (-\infty, \infty]$，矩阵$\boldsymbol{A} \in \mathbb{R}^{m \times n}$，函数$F: \mathbb{R}^n \mapsto (-\infty, \infty]$定义如下：

$$
\begin{align*}
F(\boldsymbol{x})
= f(\boldsymbol{A} \boldsymbol{x}), \boldsymbol{x} \in \mathbb{R}^n
\end{align*}
$$

如果$f$是凸的，则$F$是凸的；如果$f$是闭的，则$F$是闭的.

**证明**：由$f$的凸性，易知对于$\forall \boldsymbol{x}, \boldsymbol{y} \in \mathbb{R}^n$和$\forall \alpha \in [0, 1]$有 

$$
\begin{align*}
F(\alpha \boldsymbol{x} + (1 - \alpha) \boldsymbol{y})
= f(\alpha \boldsymbol{A} \boldsymbol{x} + (1 - \alpha) \boldsymbol{A} \boldsymbol{y}) 
\leq \alpha f(\boldsymbol{A} \boldsymbol{x}) + (1 - \alpha) f( \boldsymbol{A} \boldsymbol{y})
= \alpha F(\boldsymbol{x}) + (1 - \alpha) F(\boldsymbol{y})
\end{align*}
$$

故$F$是凸的.

因为$f$是闭的，故$f$对于$\forall \boldsymbol{x} \in \mathbb{R}^m$均下半连续，由下半连续的定义知对任意收敛于$\boldsymbol{x}$的序列$\{\boldsymbol{x}_k\}$，有

$$
\begin{align*}
f(\boldsymbol{A} \boldsymbol{x})
\leq \liminf_{k \rightarrow \infty} f(\boldsymbol{A} \boldsymbol{x}_k)
\end{align*}
$$

即

$$
\begin{align*}
F(\boldsymbol{x})
\leq \liminf_{k \rightarrow \infty} F(\boldsymbol{x}_k)
\end{align*}
$$

故$F$下半连续，由命题1.1.6知$F$是闭的.

**命题1.1.9**：给定函数$f_i: \mathbb{R}^n \mapsto (-\infty, \infty], i = 1, \dots, m$，以及正标量$\gamma_1, \dots, \gamma_m$，函数$F: \mathbb{R}^n \mapsto (-\infty, \infty]$定义如下：

$$
\begin{align*}
F(\boldsymbol{x})
= \gamma_1 f_1(\boldsymbol{x}) + \dots + \gamma_m f_m(\boldsymbol{x}), \boldsymbol{x} \in \mathbb{R}^n
\end{align*}
$$

如果$f_i, i = 1, \dots, m$是凸的，则$F$是凸的；如果$f_i, , i = 1, \dots, m$是闭的，则$F$是闭的.

**证明**：由$f_i, i = 1, \dots, m$的凸性，易知对于$\forall \boldsymbol{x}, \boldsymbol{y} \in \mathbb{R}^n$和$\forall \alpha \in [0, 1]$有

$$
\begin{align*}
F(\alpha \boldsymbol{x} + (1 - \alpha) \boldsymbol{y}) 
& = \gamma_1 f_1(\alpha \boldsymbol{x} + (1 - \alpha) \boldsymbol{y}) + \dots + \gamma_m f_m(\alpha \boldsymbol{x} + (1 - \alpha) \boldsymbol{y})  \\
& \leq \gamma_1 \alpha f_1(\boldsymbol{x}) + (1 - \alpha) f_1(\boldsymbol{y}) + \dots + \gamma_m \alpha f_m(\boldsymbol{x}) + (1 - \alpha) f_m(\boldsymbol{y})  \\
& = \alpha F(\boldsymbol{x}) + (1 - \alpha) F(\boldsymbol{y}) 
\end{align*}
$$

故$F$是凸的.

因为$f_i, i = 1, \dots, m$是闭的，故$f_i$对于$\forall \boldsymbol{x} \in \mathbb{R}^n$均下半连续，由下半连续的定义知对任意收敛于$\boldsymbol{x}$的序列$\{\boldsymbol{x}_k\}$，有

$$
\begin{align*}
f_i(\boldsymbol{x})
\leq \liminf_{k \rightarrow \infty} f_i(\boldsymbol{x}_k), i = 1, \dots, m
\end{align*}
$$

于是

$$
\begin{align*}
F(\boldsymbol{x})
& = \gamma_1 f_1(\boldsymbol{x}) + \dots + \gamma_m f_m(\boldsymbol{x})   \\
& \leq \gamma_1 \liminf_{k \rightarrow \infty} f_1(\boldsymbol{x}_k) + \dots + \gamma_m \liminf_{k \rightarrow \infty} f_m(\boldsymbol{x}_k) \\
& = \liminf_{k \rightarrow \infty} (\gamma_1 f_1(\boldsymbol{x}_k) + \dots + \gamma_m f_m(\boldsymbol{x}_k))  \\
& = \liminf_{k \rightarrow \infty} F(\boldsymbol{x}_k)
\end{align*}
$$

故$F$下半连续，由命题1.1.6知$F$是闭的.

**命题1.1.10**：给定函数$f_i: \mathbb{R}^n \mapsto (-\infty, \infty], i \in I$，其中$I$是任意下标集合，函数$F: \mathbb{R}^n \mapsto (-\infty, \infty]$定义如下：

$$
\begin{align*}
F(\boldsymbol{x}) = \sup_{i \in I} f(\boldsymbol{x}_i)
\end{align*}
$$

如果$f_i, i \in I$是凸的，则$F$是凸的；如果$f_i, i \in I$是闭的，则$F$是闭的.

证明：点$(\boldsymbol{x}, w) \in epi(F)$当且仅当$F(\boldsymbol{x}) \leq w$，即当且仅当$f_i(\boldsymbol{x}) \leq w, i \in I$，即$(\boldsymbol{x}, w) \in \cap_{i \in I} epi(f_i)$，即

$$
\begin{align*}
epi(F) = \cap_{i \in I} epi(f_i)
\end{align*}
$$

若$f_i, i \in I$是凸的，由命题1.1.4知$epi(f_i)$是凸的，再由命题1.1.2(a)知$epi(F)$是凸的.若$f_i, i \in I$是闭的，由命题1.1.6知$epi(f_i)$是闭的，故$epi(F)$是闭的.

对于一阶和二阶可微凸函数，有一些额外的解析性质，还可以以此判别凸性.

命题1.1.11 [一阶性质]：凸集$C$是$\mathbb{R}^n$的非空子集，函数$f: C \rightarrow \mathbb{R}$一阶可微，那么$f$是凸函数当且仅当对于$\forall \boldsymbol{x}, \boldsymbol{z} \in C$有

$$
\begin{align}
\label{equ: first order} f(\boldsymbol{z})
\geq f(\boldsymbol{x}) + \nabla f(\boldsymbol{x})^\top (\boldsymbol{z} - \boldsymbol{x})
\end{align}
$$

**证明**：一方面，若式(\ref{equ: first order})成立，则对于$\forall \boldsymbol{x}, \boldsymbol{z} \in C$和$\forall \alpha \in [0, 1]$，设$\boldsymbol{z} = \alpha \boldsymbol{x} + (1 - \alpha) \boldsymbol{y}$，使用式(\ref{equ: first order})两次可得如下两式：

$$
\begin{align*}
f(\boldsymbol{x}) & \geq f(\boldsymbol{z}) + \nabla f(\boldsymbol{z})^\top (\boldsymbol{x} - \boldsymbol{z}),   \\
f(\boldsymbol{y}) & \geq f(\boldsymbol{z}) + \nabla f(\boldsymbol{y})^\top (\boldsymbol{y} - \boldsymbol{z})
\end{align*}
$$

将前式乘以$\alpha$，后式乘以$1 - \alpha$，相加可得

$$
\begin{align*}
\alpha f(\boldsymbol{x}) + (1 - \alpha) f(\boldsymbol{y})
\geq f(\boldsymbol{z}) + \nabla f(\boldsymbol{y})^\top (\alpha \boldsymbol{x} + (1 - \alpha) \boldsymbol{y} - \boldsymbol{z})
= f(\boldsymbol{z})= f(\alpha \boldsymbol{x} + (1 - \alpha) \boldsymbol{y})
\end{align*}
$$

故$f(\boldsymbol{x})$是凸函数.

另一方面，若$f$是凸函数，则对于$\forall \boldsymbol{x}, \boldsymbol{z} \in C$且$\boldsymbol{x} \neq \boldsymbol{z}$，考虑函数$g: (0, 1] \mapsto \mathbb{R}$：

$$
\begin{align*}
g(\alpha)
= \frac{f(\boldsymbol{x} + \alpha (\boldsymbol{z} - \boldsymbol{x})) - f(\boldsymbol{x})}{\alpha}, \alpha \in (0, 1]
\end{align*}
$$

对于任意满足$0 < \alpha_1 < \alpha_2 < 1$的$\alpha_1$和$\alpha_2$，设$\bar{\alpha} = \frac{\alpha_1}{\alpha_2}$，$\boldsymbol{z}bar = \boldsymbol{x}bar + \alpha_2 (\boldsymbol{z} - \boldsymbol{x})$，由$f$的凸性易知有

$$
\begin{align*}
f(\boldsymbol{x} + \bar{\alpha}(\boldsymbol{z} - \boldsymbol{x}))
\leq \bar{\alpha} f(\boldsymbol{z}bar) + (1 - \boldsymbol{z}bar) f(\boldsymbol{x})
\end{align*}
$$

即

$$
\begin{align*}
\frac{f(\boldsymbol{x} + \bar{\alpha}(\boldsymbol{z} - \boldsymbol{x})) - f(\boldsymbol{x})}{\alpha}
\leq f(\boldsymbol{z}bar) - f(\boldsymbol{x})
\end{align*}
$$

进一步化简得

$$
\begin{align*}
\frac{f(\boldsymbol{x} + \alpha_1 (\boldsymbol{z} - \boldsymbol{x})) - f(\boldsymbol{x})}{\alpha_1}
\leq \frac{f(\boldsymbol{x} + \alpha_2 (\boldsymbol{z} - \boldsymbol{x})) - f(\boldsymbol{x})}{\alpha_2}
\end{align*}
$$

即$g(\alpha_1) \leq g(\alpha_2)$，这意味着$g$是单调增函数，于是可得

$$
\begin{align*}
\nabla f(\boldsymbol{x})^\top (\boldsymbol{z} - \boldsymbol{x})
= \lim_{\alpha \rightarrow 0} g(\alpha)
\leq g(1) = f(\boldsymbol{z}) - f(\boldsymbol{x})
\end{align*}
$$

该命题的一个直接推论是若$f$是凸函数且对于$\forall \boldsymbol{z} \in C$有$\nabla f(\boldsymbol{x}^*)^\top (\boldsymbol{z} - \boldsymbol{x}^*) \geq 0$成立，则$\boldsymbol{x}^*$是$f$的最小值点.进一步，若$\boldsymbol{x}^* \in int(C)$，则$\boldsymbol{x}^*$是$f$的最小值点的充要条件是$\nabla f(\boldsymbol{x}^*) = \boldsymbol{0}$.

命题1.1.12 [二阶性质]：凸集$C$是$\mathbb{R}^n$的非空子集，函数$f: C \rightarrow \mathbb{R}$二阶可微，那么

1.若对于$\forall \boldsymbol{x} \in C$有$\nabla^2 f(\boldsymbol{x})$半正定，则$f$是凸函数.

2.若$f$是凸函数，$C$是开集，则对于$\forall \boldsymbol{x} \in C$有$\nabla^2 f(\boldsymbol{x})$半正定.

**证明**：

1.由Taylor展式知，对于$\forall \boldsymbol{x}, \boldsymbol{z} \in C$，存在$\alpha \in [0, 1]$满足

$$\begin{align*}
f(\boldsymbol{y})
= f(\boldsymbol{x}) + \nabla f(\boldsymbol{x})^\top (\boldsymbol{y} - \boldsymbol{x}) + \frac{1}{2} (\boldsymbol{y} - \boldsymbol{x})^\top \nabla^2 f(\boldsymbol{x} + \alpha(\boldsymbol{y} - \boldsymbol{x})) (\boldsymbol{y} - \boldsymbol{x})
\end{align*}
$$

若$\nabla^2 f(\boldsymbol{x})$半正定，则有$f(\boldsymbol{y}) \geq f(\boldsymbol{x}) + \nabla f(\boldsymbol{x})^\top (\boldsymbol{y} - \boldsymbol{x})$，由命题1.1.11知$f$是凸函数.

2.反证法，假设存在$\boldsymbol{x} \in C$和$\boldsymbol{z} \in \mathbb{R}^n$满足$\boldsymbol{z}^\top \nabla^2 f(\boldsymbol{x}) \boldsymbol{z} < 0$.因为$C$是开集，$\nabla^2 f$连续，于是可令$\boldsymbol{z}$取很小的模使得对于$\forall \alpha \in [0, 1]$有$\boldsymbol{z}^\top \nabla^2 f(\boldsymbol{x} + \alpha \boldsymbol{z}) \boldsymbol{z} < 0$. 于是再一次用Taylor展式可知$f(\boldsymbol{x} + \boldsymbol{z}) < f(\boldsymbol{x}) + \nabla f(\boldsymbol{x})^\top \boldsymbol{z}$，由命题1.1.11知这和$f$是凸函数是矛盾的.

# C1S2 - 凸包和仿射包
这一节主要介绍如何对非凸集进行凸化.

设集合$X$是$\mathbb{R}^n$的非空子集，所有包含$X$的凸集的交集称作$X$的凸包(convex hull)，记为$conv(X)$. 进一步，若$\boldsymbol{x}_1, \dots, \boldsymbol{x}_m \in X$，$m$是一正整数，如下形式的向量：

$$
\begin{align*}
\sum_{i=1}^m \alpha_i \boldsymbol{x}_i
, \alpha_i \geq 0
, \sum_{i=1}^m \alpha_i = 1
\end{align*}
$$

称作$X$中元素的凸组合(convex combination).

由命题1.1.2(a)知凸包也是凸集，若$X$是凸集，它的凸包就是它本身，$X$中元素的凸组合必然属于它的凸包.

进一步，若集合$X$是$\mathbb{R}^n$的非空子集，$X$中所有元素的凸组合构成的集合等价于$conv(X)$.一方面，由于$X$中的所有元素都属于$conv(X)$，根据$conv(X)$的凸性知所有元素的凸组合也都属于$conv(X)$.另一方面，考虑$X$中任意两个元素的凸组合

$$\begin{align*}
\boldsymbol{x}
& = \lambda_1 \boldsymbol{x}_1 + \dots + \lambda_m \boldsymbol{x}_m, \\
\boldsymbol{y}
& = \mu_1 \boldsymbol{y}_1 + \dots + \mu_r \boldsymbol{y}_r
\end{align*}
$$

其中$\sum_{i=1}^m \lambda_i = 1$，$\sum_{i=1}^r \mu_i = 1$，那么向量

$$
\begin{align*}
\alpha \boldsymbol{x} + (1 - \alpha) \boldsymbol{y}
= \alpha (\lambda_1 \boldsymbol{x}_1 + \dots + \lambda_m \boldsymbol{x}_m) + (1 - \alpha) (\lambda_1 \boldsymbol{y}_1 + \dots + \lambda_r \boldsymbol{y}_r)
\end{align*}
$$

也是$X$中元素的凸组合，因为$\alpha (\sum_{i=1}^m \lambda_i) + (1 - \alpha) (\sum_{i=1}^r \mu_i) = 1$，这意味着$X$中所有元素的凸组合构成的集合也是凸集，又$X$中所有元素的凸组合构成的集合包含$X$，而$conv(X)$是包含$X$的最小凸集，故$conv(X)$属于$X$中所有元素的凸组合构成的集合.综上，两者等价.由此可知，若集合$X$只有有限的$m$个元素：$\boldsymbol{x}_1, \dots, \boldsymbol{x}_m$，那么它的凸包是 

$$
\begin{align*}
conv(\{ \boldsymbol{x}_1, \dots, \boldsymbol{x}_m \})
= \left\{ \sum_{i=1}^m \alpha_i \boldsymbol{x}_i  \vert  \alpha_i \geq 0, i = 1, \dots, m, \sum_{i=1}^m \alpha_i = 1 \right\}
\end{align*}
$$

![C1S2 Pic1][C1S2-pic1]

设集合$X$是$\mathbb{R}^n$的非空子集，若$X$包含所有通过其内任意两点的直线，则称$X$为仿射集(affine set)，也称为仿射流形(affine manifold)或者仿射子空间(affine subspace)，$X$的维度是平行于该仿射空间的子空间的维度.所有包含$X$的仿射集的交集称作$X$的仿射包(affine hull)，记为$aff(X)$.

集合$X$是$\mathbb{R}^n$的非空子集，$X$中所有元素的非负组合构成的集合称作$X$生成的锥，记为$cone(X)$.显然$cone(X)$是包含原点的凸锥，但它不一定是闭的(在某些特殊的情况下，例如$X$只含有有限个元素时$cone(X)$是闭的).一个反例，$X = \{(x_1, x_2) \ \vert \ x_1^2 + (x_2^2 - 1)^2 \leq 1 \}$是紧集，但是$cone(X) = \{(x_1, x_2) \ \vert \ x_2 > 0 \} \cup \{ (0, 0) \}$不是闭的.

**命题1.2.1**：$X$是非空集合，那么

1.$X$，$conv(X)$和$cl(X)$有相同的仿射包.
2.$cone(X) = cone(conv(X))$.
3.$aff(conv(X)) \subseteq aff(cone(X))$.
4. 如果$\boldsymbol{0} \in conv(X)$，那么$aff(conv(X)) = aff(cone(X))$.

**证明**：
1.先证$X$和$cl(X)$有相同的仿射包.一方面，由$X \subseteq cl(X)$易知有$aff(X) \subseteq aff(cl(X))$.另一方面，$X \subseteq aff(X)$，而$aff(X)$是闭集，由闭包的定义知$cl(X) \subseteq aff(X)$，故$aff(cl(X)) \subseteq aff(X)$. 再证$X$和$conv(X)$有相同的仿射包，不妨设$\boldsymbol{0} \in X$，否则可以将$X$平移使其包含$\boldsymbol{0}$，这不影响结论.于是$aff(X)$和$aff(conv(X))$都是子空间.一方面，由$X \subseteq conv(X)$易知有$aff(X) \subseteq aff(conv(X))$.另一方面，设$aff(conv(X))$的维度为$m$，易知存在$\boldsymbol{x}_1, \dots, \boldsymbol{x}_m \in conv(X)$张成了$aff(conv(X))$，于是$\forall \boldsymbol{x} \in aff(conv(X))$都可以写成$\boldsymbol{x}_1, \dots, \boldsymbol{x}_m$的线性组合，由凸包的定义知$\boldsymbol{x}_i, 1 \leq i \leq m$都是$X$中元素的凸组合，故$\boldsymbol{x}$也是$X$中元素的线性组合，所以$\boldsymbol{x} \in aff(X)$，于是$aff(conv(X)) \subseteq aff(X)$.

2.因为$X \subseteq conv(X)$，故$cone(X) \subseteq cone(conv(X))$；对于$\forall \boldsymbol{x} \in cone(conv(X))$，由锥的定义知$\boldsymbol{x}$是$conv(X)$中元素的非负组合，又$conv(X)$中元素是$X$中元素的凸组合，故$\boldsymbol{x}$是$X$中元素的非负组合，所以，$\boldsymbol{x} \in cone(X)$，于是$cone(conv(X)) \subseteq cone(X)$.
.
3.因为$conv(X)$是$X$中所有元素的凸组合，$cone(X)$是$X$中所有元素的非负组合，故$conv(X) \subseteq cone(X)$，于是$aff(conv(X)) \subseteq aff(cone(X))$. 
事实上，设$X = \{(1, 1)\} \in \mathbb{R}^2$，那么$conv(X) = X$，$cone(X) = \{(\alpha, \alpha) \ \vert \ \alpha \geq 0 \}$，于是

$$
\begin{align*}
aff(conv(X)) & = \{(1, 1)\}, \\
aff(cone(X)) & = \{(x_1, x_2) \vert x_1 = x_2 \}
\end{align*}
$$

即$aff(conv(X))$是$aff(cone(X))$的真子集.

4.由(1)和(3)的结论知，只需证$aff(cone(X)) \subseteq aff(X)$.由于$\boldsymbol{0} \in cone(X)$，故$aff(cone(X))$是一个子空间，设$aff(cone(X))$的维度为$m$，易知存在$\boldsymbol{x}_1, \dots, \boldsymbol{x}_m \in cone(X)$张成了$aff(cone(X))$，于是$\forall \boldsymbol{x} \in aff(cone(X))$都可以写成$\boldsymbol{x}_1, \dots, \boldsymbol{x}_m$的线性组合，由锥的定义知$\boldsymbol{x}_i, 1 \leq i \leq m$都是$X$中元素的非负组合，故$\boldsymbol{x}$也是$X$中元素的线性组合.又$\boldsymbol{0} \in conv(X)$，故$aff(conv(X))$是一个子空间，由(1)知，$aff(X)$是子空间，因此有$\boldsymbol{x} \in aff(X)$，于是$aff(cone(X)) \subseteq aff(X)$.

**命题1.2.2** [**Caratheodory's定理**]：集合$X$是$\mathbb{R}^n$的非空子集，则

1.$cone(X)$中的任意非零向量可表示为$X$中的线性无关的向量的正组合.
2.$conv(X)$中的任意向量可表示为$X$中不超过$n + 1$个向量的凸组合，$n$是$X$的仿射包的维度.
证明：

1. 设向量$\boldsymbol{x} \neq \boldsymbol{0} \in cone(X)$，设$m$是最小的使得$\boldsymbol{x}$满足如下形式

$$
\begin{align*}
\sum_{i=1}^m \alpha_i \boldsymbol{x}_i,
\alpha_i > 0,
\boldsymbol{x}_i \in X,
i = 1, \dots, m
\end{align*}
$$

的正整数，那么向量$\boldsymbol{x}_i, i = 1, \dots, m$必然是线性无关的.反证法，假设向量$\boldsymbol{x}_i$线性相关，那么存在实数$\lambda_1, \dots, \lambda_m$满足$\sum_{i=1}^m \lambda_i \boldsymbol{x}_i = \boldsymbol{0}$且至少有一个$\lambda_i$是正数，考虑线性组合$\sum_{i=1}^m (\alpha_i - \bar{\gamma} \lambda_i) \boldsymbol{x}_i$，其中$\bar{\gamma}$是使得$\alpha_i - \gamma \lambda_i \geq 0$对所有$i$成立的最大的$\gamma$，这个线性组合给出了$\boldsymbol{x}$的一个少于$m$个向量的正组合，矛盾，故向量$\boldsymbol{x}_i, i = 1, \dots, m$必然是线性无关的.

![C1S2 Pic2][C1S2-pic2]

2. 如右图所示，考虑$\mathbb{R}^{n+1}$中的子集：$Y = \{ (y, 1) \ \vert \ y \in X \}$. 如果$\boldsymbol{x} \in conv(X)$，那么$\boldsymbol{x}$可表示为
 
$$
\begin{align*}
\boldsymbol{x}
= \sum_{i=1}^I \gamma_i \boldsymbol{x}_i, I > 0
, \gamma_i \geq 0, \sum_{i=1}^I \gamma_i = 1
\end{align*}
$$

于是$(\boldsymbol{x}, 1) = (\sum_{i=1}^I \gamma_i \boldsymbol{x}_i, \sum_{i=1}^I \gamma_i) = \sum_{i=1}^I \gamma_i (\boldsymbol{x}_i, 1) \in cone(Y)$，由(a)易知

$$
\begin{align*}
(\boldsymbol{x}, 1)
= \sum_{i=1}^m \alpha_i (\boldsymbol{x}_i, 1)
, \alpha_i > 0, m \leq n + 1
\end{align*}
$$

这里$m \leq n + 1$是因为$Y$的维度是$n+1$，最多存在$n+1$个线性无关的向量，故

$$
\begin{align*}
\boldsymbol{x}
= \sum_{i=1}^m \alpha_i \boldsymbol{x}_i
, 1 = \sum_{i=1}^m \alpha_i
, \alpha_i > 0
, m \leq n + 1
\end{align*}
$$

Caratheodory's定理是一个很重要的定理，可以此推出一些其它的结果.

**命题1.2.3**：紧集$X$是$\mathbb{R}^n$的子集，其凸包还是紧集.

**证明**：只需证明$conv(X)$中的序列$\{\boldsymbol{x}_k\}$收敛时，其极限$\bar{\boldsymbol{x}} \in conv(X)$即可.由Caratheodory's定理易知序列中的任意$\boldsymbol{x}_k$可表示为$n + 1$个向量$\boldsymbol{x}_{k,1}, \dots, \boldsymbol{x}_{k,n+1}$的凸组合，即 

$$
\begin{align*}
\boldsymbol{x}_k = \alpha_{k,1} \boldsymbol{x}_{k,1} + \dots + \alpha_{k,n+1} \boldsymbol{x}_{k,n+1},
\sum_{i=1}^{n+1} \alpha_{k,i} = 1,
\alpha_{k,i} \geq 0, i = 1, \dots, n+1
\end{align*}
$$

令

$$
\begin{align*}
\tilde{{\boldsymbol{\alpha}}}_k = \begin{bmatrix} \alpha_{k,1} \\
\vdots \\
\alpha_{k,n+1} \end{bmatrix} \in \mathbb{R}^{n+1}, \tilde{\boldsymbol{x}}_k = \begin{bmatrix} \boldsymbol{x}_{k,1} \\
\vdots \\
\boldsymbol{x}_{k,n+1} \end{bmatrix} \in \mathbb{R}^{(n+1)n}
\end{align*}
$$

由于序列$\{ \tilde{{\boldsymbol{\alpha}}}_k^\top, \tilde{\boldsymbol{x}}_k^\top \}$有界，故必存在极限，设为$( \tilde{{\boldsymbol{\alpha}}}_\infty^\top, \tilde{\boldsymbol{x}}_\infty^\top )$，其中 

$$
\begin{align*}
\tilde{{\boldsymbol{\alpha}}}_\infty = \begin{bmatrix} \alpha_{\infty,1} \\
\vdots \\
\alpha_{\infty,n+1} \end{bmatrix} \in \mathbb{R}^{n+1}, \tilde{\boldsymbol{x}}_\infty = \begin{bmatrix} \boldsymbol{x}_{\infty,1} \\
\vdots \\
\boldsymbol{x}_{\infty,n+1} \end{bmatrix} \in \mathbb{R}^{(n+1)n}
\end{align*}
$$

显然有$\sum_{i=1}^{n+1} \alpha_{\infty,i} = 1, \alpha_{\infty,i} \geq 0, i = 1, \dots, n + 1$，由于$X$是闭集，故$\boldsymbol{x}_{\infty, i} \in X, i = 1, \dots, n + 1$，再由序列极限$\bar{\boldsymbol{x}}$可表示为$\bar{\boldsymbol{x}} = \alpha_{\infty,1} \boldsymbol{x}_{\infty,1} + \dots + \alpha_{\infty,n+1} \boldsymbol{x}_{\infty,n+1}$可知$\bar{\boldsymbol{x}} \in conv(X)$.

$X$有界的假设是不可或缺的，否则序列$\{ \tilde{{\boldsymbol{\alpha}}}_k^\top, \tilde{\boldsymbol{x}}_k^\top \}$的极限不一定存在.一个反例，设 

$$
\begin{align*}
X = \{ (0, 0) \}
\cup \{ (x_1, x_2)  \vert  x_1 x_2 \geq 1, x_1 \geq 0, x_2 \geq 0 \}
\end{align*}
$$

它的凸包

$$
\begin{align*}
conv(X)
= \{ (0, 0) \}
\cup \{ (x_1, x_2)  \vert \  x_1 > 0, x_2 > 0 \}
\end{align*}
$$

就不是闭的.

# C1S3 - 相对内部和闭包
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

# C1S4 - 回收锥
![C1S4 Pic1][C1S4-pic1]

这一节考虑凸集和凸函数的渐近性质，这跟后面优化问题的最优解的存在性有很多关系.

**定义1.4.1**：集合$C$为非空凸集，若向量$\boldsymbol{d}$满足对于$\forall \boldsymbol{x} \in C$及$\forall \alpha \geq 0$有$\boldsymbol{x} + \alpha \boldsymbol{d} \in C$成立，则称$\boldsymbol{d}$是$C$的 回收方向 (recession direction)，所有回收方向构成的集合称为 回收锥 (recession cone)，记为$R_C$.

如右图所示，回收锥是包含原点的锥，事实上它是个闭凸锥.下面这个回收锥定理说明了，一个方向，只要对于凸集内某一点是回收方向，那它就是整个凸集的回收方向.

命题1.4.2[回收锥定理]：集合$C$为非空闭凸集，那么

回收锥$R_C$是闭凸集合.
$\boldsymbol{d} \in R_C$当且仅当存在$\boldsymbol{x} \in C$使得对于$\forall \alpha \geq 0$满足$\boldsymbol{x} + \alpha \boldsymbol{d} \in C$.
**证明**：

若$\boldsymbol{d}_1, \boldsymbol{d}_2 \in R_C$，$\beta \in [0, 1]$，那么对于$\forall \boldsymbol{x} \in C$及$\forall \alpha \geq 0$有$$\begin{align*}\boldsymbol{x} + \alpha(\beta \boldsymbol{d}_1 + (1 - \beta) y_2) = \beta (\boldsymbol{x} + \alpha \boldsymbol{d}_1) + (1 - \beta) (\boldsymbol{x} + \alpha \boldsymbol{d}_2) \in C,\end{align*}$$故$R_C$是凸集. 
设$\boldsymbol{d} \in cl(R_C)$且序列$\{\boldsymbol{d}_k\}$收敛于$\boldsymbol{d}$，那么对于$\forall \boldsymbol{x} \in C$及$\forall \alpha \geq 0$有$\boldsymbol{x} + \alpha \boldsymbol{d}_k \in C$，由于$C$是闭集，故$\boldsymbol{x} + \alpha \boldsymbol{d} \in C$，即$\boldsymbol{d} \in R_C$，于是$R_C$是闭集.

![C1S4 Pic2][C1S4-pic2]

若$\boldsymbol{d} \in R_C$，由定义显然存在$\boldsymbol{x} \in C$使得对于$\forall \alpha \geq 0$有$\boldsymbol{x} + \alpha \boldsymbol{d} \in C$.反过来，设对于向量$\boldsymbol{d}$，存在$\boldsymbol{x} \in C$使得对于$\forall \alpha \geq 0$有$\boldsymbol{x} + \alpha \boldsymbol{d} \in C$，不失一般性，不妨设$\boldsymbol{d} \neq \boldsymbol{0}$，任取$\bar{\boldsymbol{x}} \in C$，只需证$\bar{\boldsymbol{x}} + \boldsymbol{d} \in C$(这里假设$\alpha = 1$是没有问题的，对于$\alpha \neq 1$的情况，将$\boldsymbol{d}$进行伸缩即可). 
如右图所示，设$\boldsymbol{z} _k = \boldsymbol{x} + k \boldsymbol{d}, k = 1, 2, \dots$，显然对于$\forall k$有$\boldsymbol{z} _k \in C$. 如果存在某个$k$使得$\bar{\boldsymbol{x}} = \boldsymbol{z} _k$，那么$\bar{\boldsymbol{x}} + \boldsymbol{d} = \boldsymbol{z} _k + \boldsymbol{d} = \boldsymbol{x} + (k + 1)\boldsymbol{d} \in C$，因此不妨设对于$\forall k$有$\bar{\boldsymbol{x}} \neq \boldsymbol{z} _k$，并定义$$\begin{align*}\boldsymbol{d}_k = \frac{\boldsymbol{z} _k - \bar{\boldsymbol{x}}}{\|\boldsymbol{z} _k - \bar{\boldsymbol{x}}\|}\|\boldsymbol{d}\|, \ k = 1, 2, \dots\end{align*}$$即$\bar{\boldsymbol{x}} + \boldsymbol{d}_k$是以$\bar{\boldsymbol{x}}$为球心$\|\boldsymbol{d}\|$为半径的球与以$\bar{\boldsymbol{x}}$为端点穿过$\boldsymbol{z} _k$的射线的交点，于是有$$\begin{align*}\frac{\boldsymbol{d}_k}{\|\boldsymbol{d}\|} = \frac{\|\boldsymbol{z} _k - \boldsymbol{x}\|}{\|\boldsymbol{z} _k - \bar{\boldsymbol{x}}\|} \cdot \frac{\boldsymbol{z} _k - \boldsymbol{x}}{\|\boldsymbol{z} _k - \boldsymbol{x}\|} + \frac{\boldsymbol{x} - \bar{\boldsymbol{x}}}{\|\boldsymbol{z} _k - \bar{\boldsymbol{x}}\|} = \frac{\|\boldsymbol{z} _k - \boldsymbol{x}\|}{\|\boldsymbol{z} _k - \bar{\boldsymbol{x}}\|} \cdot \frac{\boldsymbol{d}}{\|\boldsymbol{d}\|} + \frac{\boldsymbol{x} - \bar{\boldsymbol{x}}}{\|\boldsymbol{z} _k - \bar{\boldsymbol{x}}\|},\end{align*}$$由于$\{ \boldsymbol{z} _k \}$是无界序列，故$$\begin{align*}\frac{\|\boldsymbol{z} _k - \boldsymbol{x}\|}{\|\boldsymbol{z} _k - \bar{\boldsymbol{x}}\|} \rightarrow 1, \ \frac{\boldsymbol{x} - \bar{\boldsymbol{x}}}{\|\boldsymbol{z} _k - \bar{\boldsymbol{x}}\|} \rightarrow 0,\end{align*}$$故$\boldsymbol{d}_k \rightarrow \boldsymbol{d}$.对于充分大的$k$，必然有$\|\boldsymbol{z} _k - \bar{\boldsymbol{x}}\| \geq \|\boldsymbol{d}\|$，即$\bar{\boldsymbol{x}} + \boldsymbol{d}_k$落在以$\bar{\boldsymbol{x}}$和$\boldsymbol{z} _k$为端点的线段上，由$C$的凸性知对于充分大的$k$有$\bar{\boldsymbol{x}} + \boldsymbol{d}_k \in C$，又$C$是闭集且$\bar{\boldsymbol{x}} + \boldsymbol{d}_k \rightarrow \bar{\boldsymbol{x}} + \boldsymbol{d}$，故$\bar{\boldsymbol{x}} + \boldsymbol{d} \in C$.
虽然定义1.4.1中并不要求$C$是闭集，但是命题1.4.2中，$C$是闭集是必需的，否则考虑非空凸集$$\begin{align*}C =  \{ (x_1, x_2) \vert x_1 > 0, x_2 > 0 \} \cup \{ (0, 0) \}, \end{align*}$$它的回收锥就是它本身，故(a) 不成立，回收锥不是闭集；(b)也不成立，$\boldsymbol{d} = (1,0)$是除$(0, 0)$外的所有点的回收方向，但不是$(0, 0)$点的回收方向.

**命题1.4.3**：集合$C$是$\mathbb{R}^n$的非空闭凸子集，那么

回收锥$R_C$包含非零方向当且仅当$C$无界.
$R_C = R_{ri(C)}$.
对于一系列闭凸集$C_i, i \in I$，其中$I$是任意满足$\cap_{i \in I} C_i \neq \emptyset$的下标集，则$R_{\cap_{i \in I} C_i} = \cap_{i \in I} R_{C_i}$.
设$W$是$\mathbb{R}^m$的紧凸子集，矩阵$\boldsymbol{A} \in \mathbb{R}^{m \times n}$，那么集合$V = \{ \boldsymbol{x} \in C \ \vert \ \boldsymbol{A} \boldsymbol{x} \in W \}$的回收锥是$R_C \cap \mathit{Nul}(\boldsymbol{A})$.
**证明**：

一方面，若回收锥$R_C$包含非零方向，则$C$必然无界；另一方面，若$C$无界，对于$\forall \boldsymbol{x} \in C$和$\forall \{ \boldsymbol{z} _k \} \in C$，考虑序列$\{ \boldsymbol{d}_k \}$，其中$$\begin{align*}\boldsymbol{d}_k = \frac{\boldsymbol{z} _k - \boldsymbol{x}}{\|\boldsymbol{z} _k - \boldsymbol{x}\|},\end{align*}$$设$\boldsymbol{d}$是$\{ \boldsymbol{d}_k \}$的极限，不妨设$\|\boldsymbol{z} _k - \boldsymbol{x}\|$关于$k$单调增，对于任意固定的$\alpha \geq 0$，存在充分大的$k$使得$\|\boldsymbol{z} _k - \boldsymbol{x}\| \geq \alpha$，于是$\boldsymbol{x} + \alpha \boldsymbol{d}_k$落在以$\boldsymbol{x}$和$\boldsymbol{z} _k$为端点的线段上，由$C$的凸性知$\boldsymbol{x} + \alpha \boldsymbol{d}_k \in C$，又$C$是闭集且$\boldsymbol{x} + \alpha \boldsymbol{d}_k \rightarrow \boldsymbol{x} + \alpha \boldsymbol{d}$，故$\boldsymbol{x} + \alpha\boldsymbol{d} \in C$.由命题1.4.2(b)知$\boldsymbol{d}$是回收方向.
一方面，若$\boldsymbol{d} \in R_{ri(C)}$，那么对于固定的$\boldsymbol{x} \in ri(C)$和$\forall \alpha \geq 0$有$\boldsymbol{x} + \alpha \boldsymbol{d} \in ri(C) \subseteq C$，由命题1.4.2(b)知$\boldsymbol{d} \in R_C$. 另一方面，若$\boldsymbol{d} \in R_C$，那么对于$\forall \boldsymbol{x} \in ri(C)$和$\forall \alpha \geq 0$有$\boldsymbol{x} + \alpha \boldsymbol{d} \in C$，由命题1.3.1知对于$\forall \alpha \geq 0$有$\boldsymbol{x} + \alpha \boldsymbol{d} \in ri(C)$，故$\boldsymbol{d} \in R_{ri(C)}$.
一方面，若$\boldsymbol{d} \in R_{\cap_{i \in I} C_i}$，则对于$\forall \boldsymbol{x} \in \cap_{i \in I} C_i$和$\forall \alpha \geq 0$有$\boldsymbol{x} + \alpha \boldsymbol{d} \in \cap_{i \in I} C_i$，由命题1.4.2(b)知对于$\forall i \in I$有$\boldsymbol{d} \in R_{C_i}$，于是$R_{\cap_{i \in I} C_i} \subseteq \cap_{i \in I} R_{C_i}$.另一方面，若$\boldsymbol{d} \in \cap_{i \in I} R_{C_i}$，则对于$\forall \boldsymbol{x} \in \cap_{i \in I} C_i$和$\forall \alpha \geq 0$有$\boldsymbol{x} + \alpha \boldsymbol{d} \in \cap_{i \in I} C_i$，于是$\boldsymbol{d} \in R_{\cap_{i \in I} C_i}$，于是$\cap_{i \in I} R_{C_i} \subseteq R_{\cap_{i \in I} C_i}$.
考虑闭凸集$\bar{V} = \{ \boldsymbol{x} \ \vert \ \boldsymbol{A}\boldsymbol{x} \in W \}$及$\boldsymbol{x} \in \bar{V}$，由命题1.4.2(b)知$\boldsymbol{d} \in R_{\bar{V}}$当且仅当对于$\forall \alpha \geq 0$有$\boldsymbol{x} + \alpha \boldsymbol{d} \in \bar{V}$，而这又等价于对于$\forall \alpha \geq 0$有$\boldsymbol{A} (\boldsymbol{x} + \alpha \boldsymbol{d}) \in W$，由于$\boldsymbol{A} \boldsymbol{x} \in W$，故$\boldsymbol{A} \boldsymbol{d} \in R_W$，故$\boldsymbol{d} \in R_{\bar{V}}$当且仅当$\boldsymbol{A} \boldsymbol{d} \in R_W$. 因为$W$有界，故$R_W = \{ \boldsymbol{0} \}$，于是$R_{\bar{V}}$等价于$\{ \boldsymbol{d} \ \vert \ \boldsymbol{A} \boldsymbol{d} = \boldsymbol{0} \}$，即$\mathit{Nul}(\boldsymbol{A})$，又$V = C \cap \bar{V}$，由(c)知$R_V = R_C \cap \mathit{Nul}(\boldsymbol{A})$.
$C$是闭集的条件是必需的，否则考虑无界凸集$$\begin{align*}C = \{ (x_1, x_2) \ \vert \ 0 \leq x_1 < 1, x_2 \geq 0 \} \cup \{ (1, 0) \},\end{align*}$$由于$C$没有非零的回收方向，故(a)不成立；又$(0, 1)$是$ri(C)$的回收方向，故(b)不成立；设集合$$\begin{align*}D = \{ (x_1, x_2) \ \vert \ -1 \leq x_1 \leq 0, x_2 \geq 0 \},\end{align*}$$易知$(0, 1)$是$C \cap D$的回收方向，于是$R_{C \cap D} = \{ (0, 1) \} \neq \emptyset = R_C \cap R_D$，故(c)不成立.

此外若集合$C \subseteq D$，由(c)知$R_C = R_{C \cap D} = R_C \cap R_D$，于是$R_C \subseteq R_D$，但是这个结论在$C$和$D$非闭集时不成立，设集合$$\begin{align*}C = \{ (x_1, x_2) \ \vert \ 0 \leq x_1 < 1, x_2 \geq 0 \}, \ D = C \cup \{ (1, 0) \},\end{align*}$$易知$(0, 1)$是$C$的回收方向，却不是$D$的回收方向.

回收锥的一个子集在很多时候很有用，就是它的 线性空间 (lineality space).

**定义1.4.4**：非空凸集$C$的回收锥的线性空间记为$L_C$，定义如下：$$\begin{align*}L_C = R_C \cap (-R_C),\end{align*}$$即$\boldsymbol{d} \in L_C$当且仅当对于$\forall \boldsymbol{x} \in C$有$\{\boldsymbol{x} + \alpha \boldsymbol{d} \ \vert \ \alpha \in \mathbb{R} \} \subseteq C$.

**命题1.4.5**：集合$C$是$\mathbb{R}^n$的非空闭凸子集，那么

$L_C$是$\mathbb{R}^n$的子空间.
$L_C = L_{ri(C)}$.
对于一些列闭凸集$C_i, i \in I$，其中$I$是任意满足$\cap_{i \in I} C_i \neq \emptyset$的下标集，则$L_{\cap_{i \in I} C_i} = \cap_{i \in I} L_{C_i}$.
设$W$是$\mathbb{R}^m$的紧凸子集，矩阵$\boldsymbol{A} \in \mathbb{R}^{m \times n}$，那么集合$V = \{ \boldsymbol{x} \in C \ \vert \ \boldsymbol{A} \boldsymbol{x} \in W \}$的回收线性空间是$L_C \cap \mathit{Nul}(\boldsymbol{A})$.
**证明**：

设$\boldsymbol{d}_1, \boldsymbol{d}_2 \in L_C$，$\alpha_1$和$\alpha_2$是非零标量，那么$$\begin{align*}\alpha_1 \boldsymbol{d}_1 + \alpha_2 \boldsymbol{d}_2 & = \vert\alpha_1\vert (sgn(\alpha_1) \boldsymbol{d}_1) + \vert\alpha_2\vert (sgn(\alpha_2) \boldsymbol{d}_2) \\ & = (\vert\alpha_1\vert + \vert\alpha_2\vert) \left( \frac{\vert\alpha_1\vert}{\vert\alpha_1\vert + \vert\alpha_2\vert} sgn(\alpha_1) \boldsymbol{d}_1 + \frac{\vert\alpha_2\vert}{\vert\alpha_1\vert + \vert\alpha_2\vert} sgn(\alpha_2) \boldsymbol{d}_2 \right) \\ & = (\vert\alpha_1\vert + \vert\alpha_2\vert) (\alpha \bar{\boldsymbol{d}}_1 + (1 - \alpha) \bar{\boldsymbol{d}}_2),\end{align*}$$其中$$\begin{align*}\alpha = \frac{\vert\alpha_1\vert}{\vert\alpha_1\vert + \vert\alpha_2\vert}, \ \bar{\boldsymbol{d}}_1 = sgn(\alpha_1) \boldsymbol{d}_1, \ \bar{\boldsymbol{d}}_2 = sgn(\alpha_2) \boldsymbol{d}_2,\end{align*}$$由于$L_C$是凸锥的交集，故$L_C$是凸锥，故$\bar{\boldsymbol{d}}_1 = sgn(\alpha_1) \in L_C$，$\bar{\boldsymbol{d}}_2 = sgn(\alpha_2) \boldsymbol{d}_2 \in L_C$，由$L_C$的凸性知$\alpha \bar{\boldsymbol{d}}_1 + (1 - \alpha) \bar{\boldsymbol{d}}_2 \in L_C$，于是$\alpha_1 \boldsymbol{d}_1 + \alpha_2 \boldsymbol{d}_2 \in L_C$，故$L_C$是$\mathbb{R}^n$的子空间.
易知$$\begin{align*}L_C = R_C \cap (-R_C) = R_{ri(C)} \cap (-R_{ri(C)}) = L_{ri(C)},\end{align*}$$其中第二个等号根据的是命题1.4.3(b).
易知$$\begin{align*}L_{\cap_{i \in I} C_i} = (R_{\cap_{i \in I} C_i}) \cap (-R_{\cap_{i \in I} C_i}) = (\cap_{i \in I} R_{C_i}) \cap (-\cap_{i \in I} R_{C_i}) = \cap_{i \in I} (R_{C_i} \cap -R_{C_i}) = \cap_{i \in I} L_{C_i},\end{align*}$$其中第二个等号根据的是命题1.4.3(c).
易知$$\begin{align*}L_V = R_V \cap (-R_V) = (R_C \cap \mathit{Nul}(\boldsymbol{A})) \cap ((-R_C) \cap \mathit{Nul}(\boldsymbol{A})) = (R_C \cap (-R_C))\cap \mathit{Nul}(\boldsymbol{A}) = L_C \cap \mathit{Nul}(\boldsymbol{A}),\end{align*}$$其中第二个等号根据的是命题1.4.3(d).
下面这个例子研究由线性不等式和凸二次不等式定义的集合的回收锥及其回收线性空间.

**例1.4.6**：考虑如下形式的非空集合$$\begin{align*}C = \{ \boldsymbol{x} \ \vert \ \boldsymbol{x}^\top \boldsymbol{Q} \boldsymbol{x} + \boldsymbol{c}^\top \boldsymbol{x} + b \leq 0 \},\end{align*}$$其中$\boldsymbol{Q} \in \mathbb{R}^{n \times n}$是对称半正定矩阵，$\boldsymbol{c} \in \mathbb{R}^n$，$b$是标量.则$\boldsymbol{d} \in R_C$当且仅当$$\begin{align*}(\boldsymbol{x} + \alpha \boldsymbol{d})^\top \boldsymbol{Q} (\boldsymbol{x} + \alpha \boldsymbol{d}) + \boldsymbol{c}^\top (\boldsymbol{x} + \alpha \boldsymbol{d}) + b \leq 0, \ \forall \alpha > 0,\boldsymbol{x} \in C,\end{align*}$$即$$\begin{align} \label{equ: recession cone and lineality space of sets specified by linear and convex quadratic inequalities}\boldsymbol{x}^\top \boldsymbol{Q} \boldsymbol{x} + \boldsymbol{c}^\top \boldsymbol{x} + b + \alpha (\boldsymbol{c} + 2 \boldsymbol{Q} \boldsymbol{x})^\top \boldsymbol{d} + \alpha^2 \boldsymbol{d}^\top \boldsymbol{Q} \boldsymbol{d} \leq 0, \ \forall \alpha > 0, \boldsymbol{x} \in C,\end{align}$$由于$\boldsymbol{Q} \in \mathbb{R}^{n \times n}$是对称半正定矩阵，故$\boldsymbol{d}^\top \boldsymbol{Q} \boldsymbol{d} \geq 0$，然而由$\alpha$的任意性，欲使式(\ref{equ: recession cone and lineality space of sets specified by linear and convex quadratic inequalities}) 成立，必然有$\boldsymbol{d}^\top \boldsymbol{Q} \boldsymbol{d} \leq 0$，于是$\boldsymbol{d}^\top \boldsymbol{Q} \boldsymbol{d} = 0$.设$\boldsymbol{Q} = \boldsymbol{M}^\top \boldsymbol{M}$，则$(\boldsymbol{M} \boldsymbol{d})^\top \boldsymbol{M} \boldsymbol{d} = 0$，即$\boldsymbol{M} \boldsymbol{d} = \boldsymbol{0}$，故$\boldsymbol{Q} \boldsymbol{d} = \boldsymbol{0}$，于是式(\ref{equ: recession cone and lineality space of sets specified by linear and convex quadratic inequalities})等价于$$\begin{align*}\boldsymbol{x}^\top \boldsymbol{Q} \boldsymbol{x} + \boldsymbol{c}^\top \boldsymbol{x} + b + \alpha \boldsymbol{c}^\top \boldsymbol{d} \leq 0, \ \forall \alpha > 0, \boldsymbol{x} \in C,\end{align*}$$由$\alpha$的任意性知必然有$\boldsymbol{c}^\top \boldsymbol{d} \leq 0$.

综上可得$R_C = \{ \boldsymbol{d} \ \vert \ \boldsymbol{Q} \boldsymbol{d} = \boldsymbol{0} , \boldsymbol{c}^\top \boldsymbol{d} \leq 0 \}$，$L_C = \{ \boldsymbol{d} \ \vert \ \boldsymbol{Q} \boldsymbol{d} = \boldsymbol{0} , \boldsymbol{c}^\top \boldsymbol{d} = 0 \}$.

若集合$C$是由一系列这样的凸二次不等式的交集构成的，即$$\begin{align*}C = \{ \boldsymbol{x} \ \vert \ \boldsymbol{x}^\top \boldsymbol{Q}_j \boldsymbol{x} + \boldsymbol{c}_j^\top \boldsymbol{x} + b_j \leq 0, j \in J \} = \cap_{j \in J} \{ \boldsymbol{x} \ \vert \ \boldsymbol{x}^\top \boldsymbol{Q}_j \boldsymbol{x} + \boldsymbol{c}_j^\top \boldsymbol{x} + b_j \leq 0 \},\end{align*}$$其中$J$是下标集，由命题1.4.3(c)，命题1.4.5(c)和前面的推导知$$\begin{align*}R_C & = R_{\cap_{j \in J} \{ \boldsymbol{x} \ \vert \ \boldsymbol{x}^\top \boldsymbol{Q}_j \boldsymbol{x} + \boldsymbol{c}_j^\top \boldsymbol{x} + b_j \leq 0 \}} = \cap_{j \in J} R_{\{ \boldsymbol{x} \ \vert \ \boldsymbol{x}^\top \boldsymbol{Q}_j \boldsymbol{x} + \boldsymbol{c}_j^\top \boldsymbol{x} + b_j \leq 0 \}} = \cap_{j \in J} \{ \boldsymbol{d} \ \vert \ \boldsymbol{Q}_j \boldsymbol{d} = \boldsymbol{0} , \boldsymbol{c}_j^\top \boldsymbol{d} \leq 0 \}, \\ L_C & = L_{\cap_{j \in J} \{ \boldsymbol{x} \ \vert \ \boldsymbol{x}^\top \boldsymbol{Q}_j \boldsymbol{x} + \boldsymbol{c}_j^\top \boldsymbol{x} + b_j \leq 0 \}} = \cap_{j \in J} L_{\{ \boldsymbol{x} \ \vert \ \boldsymbol{x}^\top \boldsymbol{Q}_j \boldsymbol{x} + \boldsymbol{c}_j^\top \boldsymbol{x} + b_j \leq 0 \}} = \cap_{j \in J} \{ \boldsymbol{d} \ \vert \ \boldsymbol{Q}_j \boldsymbol{d} = \boldsymbol{0} , \boldsymbol{c}_j^\top \boldsymbol{d} = 0 \}.\end{align*}$$特别地，若$C$是多面体，即$$\begin{align*}C = \{ \boldsymbol{x} \ \vert \ \boldsymbol{c}_j^\top \boldsymbol{x} + b_j \leq 0, j \in J \} = \cap_{j \in J} \{ \boldsymbol{x} \ \vert \ \boldsymbol{c}_j^\top \boldsymbol{x} + b_j \leq 0 \},\end{align*}$$那么$$\begin{align*}R_C = \cap_{j \in J} \{ \boldsymbol{d} \ \vert \ \boldsymbol{c}_j^\top \boldsymbol{d} \leq 0 \}, \ L_C = \cap_{j \in J} \{ \boldsymbol{d} \ \vert \ \boldsymbol{c}_j^\top \boldsymbol{d} = 0 \}.\end{align*}$$

命题1.4.7[凸集分解定理]：集合$C$是$\mathbb{R}^n$的非空闭凸子集，那么对于$L_C$的任意子空间$S$有$$\begin{align*}C = S + (C \cap S^\perp).\end{align*}$$

![C1S4 Pic3][C1S4-pic3]

**证明**：如右图所示将$\mathbb{R}^n$分解成$S$和$S^\perp$.一方面，若$\boldsymbol{x} \in C$，可设$\boldsymbol{x} = \boldsymbol{d} + \boldsymbol{z}$，其中$\boldsymbol{d} \in S$，$\boldsymbol{z}  \in S^\perp$. 由于$\boldsymbol{d} \in S \subseteq L_C$，故$-\boldsymbol{d} \in L_C$，即$-\boldsymbol{d}$也是$C$的回收方向，于是$\boldsymbol{z}  = \boldsymbol{x} - \boldsymbol{d} \in C$，即$\boldsymbol{z}  \in C \cap S^\perp$，于是$\boldsymbol{x} \in S + (C \cap S^\perp)$，故$C \subseteq S + (C \cap S^\perp)$.另一方面，若$\boldsymbol{x} \in S + (C \cap S^\perp)$，可设$\boldsymbol{x} = \boldsymbol{d} + \boldsymbol{z}$，其中$\boldsymbol{d} \in S$，$\boldsymbol{z}  \in C \cap S^\perp$. 由于$\boldsymbol{d} \in S \subseteq L_C$，故$\boldsymbol{d}$是$C$的回收方向，又$\boldsymbol{z}  \in C$，故$\boldsymbol{x} = \boldsymbol{d} + \boldsymbol{z}  \in C$，故$S + (C \cap S^\perp) \subseteq C$.

综上，$C = S + (C \cap S^\perp)$.

注意若取$S = L_C$可得$C = L_C + (C \cap L_C^\perp)$故$C$可分解为如下两个集合的向量和：

$L_C$，即$C$中包含的所有通过原点的直线.
$C \cap L_C^\perp$，这个集合不包含直线.否则设直线$\{\boldsymbol{x} + \alpha \boldsymbol{d} \ \vert \ \alpha \in \mathbb{R}\} \subseteq C \cap L_C^\perp$，于是$\boldsymbol{d} \in L_C$，故有$\boldsymbol{d} \perp (\boldsymbol{x} + \alpha \boldsymbol{d})$，由$\alpha$的任意性知$\boldsymbol{d} = \boldsymbol{0}$.
于是若$C$是闭集且$R_C = L_C$，那么$C \cap L_C^\perp$不包含任何回收方向，由命题1.4.3(a)知是紧集，故此时$C$可分解成其回收线性空间与某个紧集.

  下面引入一个新的概念， 凸函数的回收方向 ，这跟后面优化问题的最优解的存在性有很多关系.注意凸函数的上境图是凸集，而这个凸集的回收锥是可以用来刻画函数的变化特性的.事实上，沿着这个回收锥的水平方向，函数值将单调减小，参见下面这几个命题.

**命题1.4.8**：函数$f: \mathbb{R}^n \mapsto (-\infty, \infty]$是正常闭凸函数，水平集$V_\gamma = \{ \boldsymbol{x} \ \vert \ f(\boldsymbol{x}) \leq \gamma \}, \gamma \in \mathbb{R}$，那么

所有的非空水平集$V_\gamma$有相同的回收锥，记为$R_f$，且$$\begin{align*}R_f = \{ \boldsymbol{d} \ \vert \ (\boldsymbol{d}, 0) \in R_{epi(f)} \},\end{align*}$$其中$R_{epi(f)}$是$f$上境图的回收锥.
如果有一个非空水平集是紧集，那么所有的水平集都是紧集.

![C1S4 Pic4][C1S4-pic4]

**证明**：

对于任意使得$V_\gamma$非空的$\gamma$，定义集合$$\begin{align*}S = \{ (\boldsymbol{x}, \gamma) \ \vert \ f(\boldsymbol{x}) \leq \gamma \},\end{align*}$$易知$$\begin{align*}S = epi(f) \cap \{ (\boldsymbol{x}, \gamma) \ \vert \ \boldsymbol{x} \in \mathbb{R}^n \}\end{align*}$$由命题1.4.3(c)中的的结论知$$\begin{align*}R_S = R_{epi(f)} \cap R_{\{ (\boldsymbol{x}, \gamma) \ \vert \ \boldsymbol{x} \in \mathbb{R}^n \}} = R_{epi(f)} \cap \{ (\boldsymbol{d}, 0) \ \vert \ \boldsymbol{d} \in \mathbb{R}^n \} = \{ (\boldsymbol{d}, 0) \ \vert \ (\boldsymbol{d}, 0) \in R_{epi(f)} \},\end{align*}$$由于$V_\gamma$是$S$在$\mathbb{R}^n$上的投影，于是$$\begin{align*}R_{V_\gamma} = \{ \boldsymbol{d} \ \vert \ (\boldsymbol{d}, 0) \in R_{epi(f)} \}.\end{align*}$$
某个非空水平集$V_\gamma$是紧集当且仅当它的回收锥不含有非零方向，由(a)知所有非空水平集$V_\gamma$有相同的回收锥，故所有非空水平集都是紧集.
命题中$f$是闭函数是必需的，设非闭凸函数$f: \mathbb{R}^2 \mapsto (-\infty, \infty]$定义如下：$$\begin{align*}f(x_1, x_2) = \begin{cases} - x_1 & x_1 > 0, x_2 \geq 0, \\ x_2 & x_1 = 0, x_2 \geq 0, \\ \infty & others, \end{cases} \end{align*}$$对于$\gamma < 0$，显然$V_\gamma = \{ (\boldsymbol{x}_1, \boldsymbol{x}_2) \ \vert \ \boldsymbol{x}_1 \geq - \gamma, x_2 \geq 0 \}$，$(0, 1) \in R_{V_\gamma}$；而$V_0 = \{ (\boldsymbol{x}_1, \boldsymbol{x}_2) \ \vert \ \boldsymbol{x}_1 > 0, x_2 \geq 0 \} \cup \{(0, 0)\}$，$(0, 1) \not \in R_{V_0}$.

正常闭凸函数$f: \mathbb{R}^n \mapsto (-\infty, \infty]$的回收锥定义为它的非空水平集的回收锥，如下图所示，回收锥中的任意一个向量都称为$f$的回收方向，回收锥的线性空间记为$L_f$.

![C1S4 Pic5][C1S4-pic5]

直观上来说，可以从函数值变化的角度来看正常闭凸函数的回收锥，从某个点$\boldsymbol{x} \in dom(f)$开始，沿着回收方向走，则函数值将连续非增(continuous non-ascent)，每当穿过一个水平集的边界，我们将永远在它“里面”.若$\boldsymbol{d} \in L_f$，则沿着$\boldsymbol{d}$方向和$-\boldsymbol{d}$方向走函数值都连续非增，这意味着在这个方向上函数值为常数，即对于$\forall \alpha \in \mathbb{R}$有$f(\boldsymbol{x} + \alpha \boldsymbol{d}) = f(\boldsymbol{x})$，故$L_f$又被称为$f$的常数空间(constancy space).例如设函数$f$为二次函数，即$f = \boldsymbol{x}^\top \boldsymbol{Q} \boldsymbol{x} + \boldsymbol{c}^\top \boldsymbol{x} + b$，其中$\boldsymbol{Q} \in \mathbb{R}^{n \times n}$是对称半正定矩阵，$\boldsymbol{c} \in \mathbb{R}^n$，$b$是标量，由例1.4.6中的推导知$$\begin{align*}R_f = \{ \boldsymbol{d} \ \vert \ \boldsymbol{Q} \boldsymbol{d} = \boldsymbol{0} , \boldsymbol{c}^\top \boldsymbol{d} \leq 0 \}, \ L_f = \{ \boldsymbol{d} \ \vert \ \boldsymbol{Q} \boldsymbol{d} = \boldsymbol{0} , \boldsymbol{c}^\top \boldsymbol{d} = 0 \}.\end{align*}$$

由于正常闭凸函数$f: \mathbb{R}^n \mapsto (-\infty, \infty]$的上境图是非空闭凸集，故由命题1.4.2(a)知其回收锥是闭凸的，故将其看作另一个正常闭凸函数的上境图，该函数称为$f$的回收函数(recession function)，记为$r_f$，即$epi(r_f) = R_{epi(f)}$.回收函数可以用来刻画原函数的回收锥和常数空间，下面这个命题说明了，如果$\boldsymbol{d}$是$f$的回收方向，那么从任意点$\boldsymbol{x} \in dom(f)$开始，沿着$\boldsymbol{d}$走，函数值都将连续非增.

**命题1.4.9**：设$f: \mathbb{R}^n \mapsto (-\infty, \infty]$是正常闭凸函数，那么$f$的回收锥及其常数空间分别可以表示如下：$$\begin{align*} R_f = \{ \boldsymbol{d} \ \vert \ r_f(\boldsymbol{d}) \leq 0\}, \ L_f = \{ \boldsymbol{d} \ \vert \ r_f(\boldsymbol{d}) = r_f(-\boldsymbol{d}) = 0 \}.\end{align*}$$

**证明**：由命题1.4.8(a)及$r_f$的定义知$$\begin{align*}R_f = \{ \boldsymbol{d} \ \vert \ (\boldsymbol{d}, 0) \in R_{epi(f)} \} = \{ \boldsymbol{d} \ \vert \ (\boldsymbol{d}, 0) \in epi(r_f) \} = \{ \boldsymbol{d} \ \vert \ r_f(\boldsymbol{d}) \leq 0 \}.\end{align*}$$由定义知$L_f = R_f \cap (-R_f)$，因此$\boldsymbol{d} \in L_f$当且仅当$r_f(\boldsymbol{d}) \leq 0$且$r_f(-\boldsymbol{d}) \leq 0$，由$r_f$的凸性知$$\begin{align*}0 \geq r_f(\boldsymbol{d}) + r_f(-\boldsymbol{d}) \geq 2r_f( \boldsymbol{0} ) = 0\end{align*}$$这意味着$r_f(\boldsymbol{d}) = r_f(-\boldsymbol{d}) = 0$.

下面这个命题给出了回收函数的显式表达.

**命题1.4.10**：设$f: \mathbb{R}^n \mapsto (-\infty, \infty]$是正常闭凸函数，那么对于$\forall \boldsymbol{x} \in dom(f)$和$\boldsymbol{d} \in \mathbb{R}^n$有$$\begin{align} \label{equ: recession function}r_f(\boldsymbol{d}) = \sup_{\alpha > 0} \frac{f(\boldsymbol{x} + \alpha \boldsymbol{d}) - f(\boldsymbol{x})}{\alpha} = \lim_{\alpha \rightarrow \infty} \frac{f(\boldsymbol{x} + \alpha \boldsymbol{d}) - f(\boldsymbol{x})}{\alpha}.\end{align}$$

**证明**：由定义$r_f(\boldsymbol{d}) \leq v \Leftrightarrow (\boldsymbol{d}, v) \in epi(r_f) \Leftrightarrow (\boldsymbol{d}, v) \in R_{epi(f)}$，由于$f$是闭凸函数，由回收锥定理知$$\begin{align*}(\boldsymbol{d}, v) \in R_{epi(f)} & \Leftrightarrow f(\boldsymbol{x} + \alpha \boldsymbol{d}) \leq f(\boldsymbol{x}) + \alpha v, \ \forall \alpha \geq 0 \\ & \Leftrightarrow f(\boldsymbol{x} + \alpha \boldsymbol{d}) \leq f(\boldsymbol{x}) + \alpha v, \ \forall \alpha > 0 \\ & \Leftrightarrow \frac{f(\boldsymbol{x} + \alpha \boldsymbol{d}) - f(\boldsymbol{x})}{\alpha} \leq v, \ \forall \alpha > 0 \\ & \Leftrightarrow \sup_{\alpha > 0} \frac{f(\boldsymbol{x} + \alpha \boldsymbol{d}) - f(\boldsymbol{x})}{\alpha} \leq v. \end{align*}$$故$r_f(\boldsymbol{d}) \leq v \Leftrightarrow \sup_{\alpha > 0} \frac{f(\boldsymbol{x} + \alpha \boldsymbol{d}) - f(\boldsymbol{x})}{\alpha} \leq v$，这意味着$$\begin{align*}r_f(\boldsymbol{d}) = \sup_{\alpha > 0} \frac{f(\boldsymbol{x} + \alpha \boldsymbol{d}) - f(\boldsymbol{x})}{\alpha}.\end{align*}$$由命题1.1.11的证明过程知$\frac{f(\boldsymbol{x} + \alpha \boldsymbol{d}) - f(\boldsymbol{x})}{\alpha}$是关于$\alpha$的单调增函数，故$$\begin{align*}r_f(\boldsymbol{d}) = \sup_{\alpha > 0} \frac{f(\boldsymbol{x} + \alpha \boldsymbol{d}) - f(\boldsymbol{x})}{\alpha} = \lim_{\alpha \rightarrow \infty} \frac{f(\boldsymbol{x} + \alpha \boldsymbol{d}) - f(\boldsymbol{x})}{\alpha}.\end{align*}$$

若$f$是正常闭凸函数，那么$f$的回收锥为$R_f = \{ \boldsymbol{d} \ \vert \ r_f(\boldsymbol{d}) \leq 0\}$，结合式(\ref{equ: recession function})可知，从任意点开始，沿着回收方向，函数值都将连续非增.若$f$可微，可以得到更具体的表达式，由命题1.1.11(a)知$$\begin{align*}\nabla f(\boldsymbol{x})^\top \boldsymbol{d} \leq \frac{f(\boldsymbol{x} + \alpha \boldsymbol{d}) - f(\boldsymbol{x})}{\alpha} \leq \nabla f(\boldsymbol{x} + \alpha \boldsymbol{d})^\top \boldsymbol{d},\end{align*}$$令$\alpha \rightarrow \infty$可得$$\begin{align*}\nabla f(\boldsymbol{x})^\top \boldsymbol{d} \leq r_f(\boldsymbol{d}) \leq \lim_{\alpha \rightarrow \infty} \nabla f(\boldsymbol{x} + \alpha \boldsymbol{d})^\top \boldsymbol{d},\end{align*}$$左边的不等式对于$\forall \boldsymbol{x}$都成立，故用$\boldsymbol{x} + \alpha \boldsymbol{d}$替代$\boldsymbol{x}$可得$$\begin{align*}f(\boldsymbol{x} + \alpha \boldsymbol{d})^\top \boldsymbol{d} \leq r_f(\boldsymbol{d}), \ \forall \alpha > 0.\end{align*}$$令$\alpha \rightarrow \infty$可得$$\begin{align*}\lim_{\alpha \rightarrow \infty} f(\boldsymbol{x} + \alpha \boldsymbol{d})^\top \boldsymbol{d} \leq r_f(\boldsymbol{d}).\end{align*}$$综上可得$$\begin{align*}r_f(\boldsymbol{d}) = \lim_{\alpha \rightarrow \infty} \nabla f(\boldsymbol{x} + \alpha \boldsymbol{d})^\top \boldsymbol{d}.\end{align*}$$

下面这个命题说明函数和的回收函数等于函数回收函数的和.

**命题1.4.11**：设$f_i: \mathbb{R}^n \mapsto (-\infty, \infty], i = 1, \dots, m$是正常闭凸函数且$$\begin{align*}f = f_1 + \dots + f_m\end{align*}$$是正常闭凸函数，那么$$\begin{align*}r_f(\boldsymbol{d}) = r_{f_1}(\boldsymbol{d}) + \dots + r_{f_m}(\boldsymbol{d}), \ \forall \boldsymbol{d} \in \mathbb{R}^n.\end{align*}$$

**证明**：由命题1.1.9知$f_1 + \dots + f_m$是闭凸函数，由命题1.4.10知对于$\forall \boldsymbol{x} \in dom(f)$和$\boldsymbol{d} \in \mathbb{R}^n$有$$\begin{align*}r_f(\boldsymbol{d}) & = \lim_{\alpha \rightarrow \infty} \frac{f(\boldsymbol{x} + \alpha \boldsymbol{d}) - f(\boldsymbol{x})}{\alpha} \\ & = \lim_{\alpha \rightarrow \infty} \left( \frac{f_1(\boldsymbol{x} + \alpha \boldsymbol{d}) - f_1(\boldsymbol{x})}{\alpha} + \dots + \frac{f_m(\boldsymbol{x} + \alpha \boldsymbol{d}) - f_m(\boldsymbol{x})}{\alpha} \right) \\ & = \lim_{\alpha \rightarrow \infty} \frac{f_1(\boldsymbol{x} + \alpha \boldsymbol{d}) - f_1(\boldsymbol{x})}{\alpha} + \dots + \lim_{\alpha \rightarrow \infty} \frac{f_m(\boldsymbol{x} + \alpha \boldsymbol{d}) - f_m(\boldsymbol{x})}{\alpha} \\ & = r_{f_1}(\boldsymbol{d}) + \dots + r_{f_m}(\boldsymbol{d}).\end{align*}$$

注意命题中的$f$是正常函数的要求是必须的，否则它的回收函数没有意义.同理可证明如下命题.

**命题1.4.12**：设$f_i: \mathbb{R}^n \mapsto (-\infty, \infty], i = 1, \dots, m$是正常闭凸函数且$$\begin{align*}f(\boldsymbol{x}) = \sup_{i \in I} f_i(\boldsymbol{x})\end{align*}$$是正常闭凸函数，其中$I$是下标集，那么$$\begin{align*}r_f(\boldsymbol{d}) = \sup_{i \in I} r_{f_i}(\boldsymbol{d}).\end{align*}$$

**证明**：由命题1.1.10的证明过程知$f(\boldsymbol{x}) = \sup_{i \in I} f_i(\boldsymbol{x}) \Leftrightarrow epi(f) = \cap_{i \in I} epi(f_i)$. 于是根据回收函数的定义和命题1.4.3(c)知$$\begin{align*}epi(r_f) = R_{epi(f)} = R_{\cap_{i \in I} epi(f_i)} = \cap_{i \in I} R_{epi(f_i)} = \cap_{i \in I}epi(r_{f_i}),\end{align*}$$故$$\begin{align*}r_f(\boldsymbol{d}) = \sup_{i \in I} r_{f_i}(\boldsymbol{d}).\end{align*}$$

![C1S4 Pic6][C1S4-pic6]

集合交集的非空性可以用来回答下面这个问题：函数$f: \mathbb{R}^n \mapsto \mathbb{R}$是否能在集合$X$上取得最小值？如右图所示，这等价于$$\begin{align*}\cap_{k=0}^\infty \{ \boldsymbol{x} \in X \vert f(\boldsymbol{x}) \leq \gamma_k \}\end{align*}$$是否非空集，其中$\{ \gamma_k \}$是标量序列且$\gamma_k \rightarrow \inf_{\boldsymbol{x} \in X} f(\boldsymbol{x})$.对于紧集，回答是肯定的，但是对于一般的闭凸集来说，就不一定了，需要一些额外的条件才能保证类似的性质，这就要涉及到前面介绍的回收方向等概念了.

下面我们讨论非空嵌套闭凸集合序列交集非空的条件，设序列$\{\boldsymbol{x}_k\}$满足$\boldsymbol{x}_k \in C_k, k = 1, 2, \dots$，由于$\cap_{k=0}^\infty C_k$非空当且仅当全部这样的序列$\{\boldsymbol{x}_k\}$均是无界的，因此只需研究何时并非全部这样的序列均是无界的.

**定义1.4.13**：设$\{C_k\}$是非空嵌套闭凸集序列，若序列$\{\boldsymbol{x}_k\}$对于$\forall k$有$\boldsymbol{0} \neq \boldsymbol{x}_k \in C_k$，且$$\begin{align*}\|\boldsymbol{x}_k \| \rightarrow \infty, \ \frac{\boldsymbol{x}_k}{\|\boldsymbol{x}_k\|} \rightarrow\frac{\boldsymbol{d}}{\|\boldsymbol{d}\|},\end{align*}$$其中$\boldsymbol{d}$是$\{C_k\}$的某个非零公共回收方向，即$\boldsymbol{0} \neq \boldsymbol{d} \in \cap_{k=0}^\infty R_{C_k}$，则称$\{\boldsymbol{x}_k\}$是$\{C_k\}$的 渐进序列 (asymptotic sequence).特别地，若所有的$C_k$都是相同的，即$C_k \equiv C$，则称$\{\boldsymbol{x}_k\}$是集合$C$的渐进序列.

对于任一满足$\boldsymbol{x}_k \in C_k, k = 1, 2, \dots$的无界序列$\{\boldsymbol{x}_k\}$，都存在子序列$\{\boldsymbol{x}_k\}_{k \in \mathcal{K}}$是集合子序列$\{C_k\}_{k \in \mathcal{K}}$的渐进序列.事实上，由命题1.4.2(b)的证明过程知序列$\{ \boldsymbol{x}_k / \|\boldsymbol{x}_k\| \}$的任一聚点都是$\{C_k\}$的公共回收方向.因此，我们只需将注意力放在渐进序列上.

**定义1.4.14**：设$\{C_k\}$是非空嵌套闭凸集序列，渐进序列$\{\boldsymbol{x}_k\}$和公共回收方向$\boldsymbol{d}$同定义1.4.13，若存在下标$\bar{k}$使得$$\begin{align*}\boldsymbol{x}_k - \boldsymbol{d} \in C_k, \ \forall k \geq \bar{k},\end{align*}$$则称渐进序列$\{\boldsymbol{x}_k\}$是 回缩 (retractive)的.若$\{C_k\}$的所有渐进序列都是回缩的，则称$\{C_k\}$是回缩的.特别地，若所有的$C_k$都是相同的，即$C_k \equiv C$，则称$C$是回缩的.

回缩集合序列的任一渐进序列，沿其对应的公共回收方向$\boldsymbol{d}$反向平移后，都存在充分大的$\bar{k}$，使得$\boldsymbol{x}_k \in C_k, k \geq \bar{k}$.例如设$C_k = \{ (x_1, x_2) \ \vert \ \vertx_1\vert \leq 1/k \}$，则其渐进序列是回缩的：若$\boldsymbol{x}_{k,1} \rightarrow 0$，$\boldsymbol{x}_{k,2} \rightarrow \infty$，则对应$\boldsymbol{d} = (0, 1)$；若$\boldsymbol{x}_{k,1} \rightarrow 0$，$\boldsymbol{x}_{k,2} \rightarrow -\infty$，则对应$\boldsymbol{d} = (0, -1)$.

**命题1.4.15**：设$\{C_{1,k}\}, \dots, \{C_{r,k}\}$是$r$个回缩集合序列，令$N_k = C_{1,k} \cap \dots \cap C_{r,k}$，$T_k = C_{1,k} \times \dots \times C_{r,k}$，则$\{N_k\}$和$\{T_k\}$是回缩集合序列.

**证明**：考虑$\{ N_k \}$的任一渐进序列$\boldsymbol{x}_k \in N_k, k = 1, 2, \dots$，则由定义1.4.13知$$\begin{align*}\|\boldsymbol{x}_k \| \rightarrow \infty, \ \frac{\boldsymbol{x}_k}{\|\boldsymbol{x}_k\|} \rightarrow \frac{\boldsymbol{d}}{\|\boldsymbol{d}\|},\end{align*}$$其中$\boldsymbol{0} \neq \boldsymbol{d} \in \cap_{k=0}^\infty R_{N_k}$.由命题1.4.3(c)知$$\begin{align*}\boldsymbol{0} \neq \boldsymbol{d} \in \cap_{k=0}^\infty R_{N_k} = \cap_{k=0}^\infty (\cap_{i=1}^r R_{C_{i,k}}) = \cap_{i=1}^r (\cap_{k=0}^\infty R_{C_{i,k}}),\end{align*}$$故$\boldsymbol{d}$属于$r$个回缩集合序列的非零公共回收方向的交集，于是对于这$r$个集合序列，$\{\boldsymbol{x}_k\}$均是其渐进序列，又这$r$个集合序列是回缩的，故由定义1.4.14知，对于第$i$个回缩集合序列$\{C_{r,k}\}$，存在下标$k_i$使得$$\begin{align*}\boldsymbol{x}_k - \boldsymbol{d} \in C_{i,k}, \ \forall k \geq k_i,\end{align*}$$取$\bar{k} = \max\{k_1, \dots, k_r \}$，于是$$\begin{align*}\boldsymbol{x}_k - \boldsymbol{d} \in C_{i,k}, \ \forall k \geq \bar{k}, 1 \leq i \leq r,\end{align*}$$即$$\begin{align*}\boldsymbol{x}_k - \boldsymbol{d} \in \cap_{i=1}^r C_{i,k} = N_k, \ \forall k \geq \bar{k},\end{align*}$$故$\{N_k\}$是回缩集合序列.

考虑$\{ T_k \}$的任一渐进序列$\boldsymbol{x}_k = [\boldsymbol{x}_{1,k}^\top, \dots, \boldsymbol{x}_{r,k}^\top]^\top \in T_k, k = 1, 2, \dots$，则由定义1.4.13知$$\begin{align*}\|\boldsymbol{x}_k \| \rightarrow \infty, \ \frac{\boldsymbol{x}_k}{\|\boldsymbol{x}_k\|} \rightarrow \frac{\boldsymbol{d}}{\|\boldsymbol{d}\|},\end{align*}$$其中$\boldsymbol{0} \neq \boldsymbol{d} \in \cap_{k=0}^\infty R_{T_k}$.由定义不难证明$R_{C_1 \times \dots \times C_k} = R_{C_1} \times \dots \times R_{C_k}$成立，故有$$\begin{align*}\boldsymbol{0} \neq \boldsymbol{d} \in \cap_{k=0}^\infty R_{T_k} = \cap_{k=0}^\infty (R_{C_{1,k}} \times \dots \times R_{C_{r,k}}) = (\cap_{k=0}^\infty R_{C_{1,k}}) \times \dots\times (\cap_{k=0}^\infty R_{C_{r,k}}),\end{align*}$$故$\boldsymbol{d} = [\boldsymbol{d}_1^\top, \dots, \boldsymbol{d}_r^\top]^\top$是$r$个回缩集合序列的非零公共回收方向的Cartesian积，又这$r$个集合序列是回缩的，故由定义1.4.14知，对于第$i$个回缩集合序列$\{C_{r,k}\}$，存在下标$k_i$使得$$\begin{align*}\boldsymbol{x}_{i,k} - \boldsymbol{d}_i \in C_{i,k}, \ \forall k \geq k_i,\end{align*}$$取$\bar{k} = \max\{k_1, \dots, k_r \}$，于是$$\begin{align*}\boldsymbol{x}_{i,k} - \boldsymbol{d}_i \in C_{i,k}, \ \forall k \geq \bar{k}, 1 \leq i \leq r,\end{align*}$$即$$\begin{align*}\boldsymbol{x}_k - \boldsymbol{d} \in C_{1,k} \times \dots \times C_{r,k} = T_k, \ \forall k \geq \bar{k},\end{align*}$$故$\{T_k\}$是回缩集合序列.

**命题1.4.16**：多面体是回缩的.

**证明**：多面体是有限个半空间的非空交集，半空间显然是回缩的，由命题1.4.15知多面体也是回缩的.

**命题1.4.17**：若非空嵌套闭凸集序列$\{C_k\}$是回缩的，则其交集$\cap_{k=0}^\infty C_k$非空.

**证明**：反证法，设$\boldsymbol{x}_k$是原点在集合$C_k$上的投影，即$\boldsymbol{x}_k$是集合$C_k$中范数最小的向量，若$\cap_{k=0}^\infty C_k$是空集，则$\{\boldsymbol{x}_k\}$是无界序列，故存在子序列$\{\boldsymbol{x}_k\}_{k \in \mathcal{K}}$是集合子序列$\{C_k\}_{k \in \mathcal{K}}$的渐进序列，即$$\begin{align*}\|\boldsymbol{x}_k \| \rightarrow \infty, \ \frac{\boldsymbol{x}_k}{\|\boldsymbol{x}_k\|} \rightarrow \frac{\boldsymbol{d}}{\|\boldsymbol{d}\|}, \ k \in \mathcal{K}.\end{align*}$$其中$\boldsymbol{d}$是$\{C_k\}$的某个非零公共回收方向.对于任意$k = 0, 1, \dots$，定义$\boldsymbol{z} _k = \boldsymbol{x}_m$，其中$m$是满足$k \leq m \in \mathcal{K}$的最小下标，故$$\begin{align*}\|\boldsymbol{z} _k \| \rightarrow \infty, \ \frac{\boldsymbol{z} _k}{\|\boldsymbol{z} _k\|} \rightarrow \frac{\boldsymbol{d}}{\|\boldsymbol{d}\|}.\end{align*}$$由于$\{C_k\}$是回缩的，故渐进序列$\{\boldsymbol{z} _k\}$也是回缩的，于是存在$\bar{k}$满足$$\begin{align*}\boldsymbol{z} _k - \boldsymbol{d} \in C_k, \ \forall k \geq \bar{k}.\end{align*}$$又$$\begin{align*}\boldsymbol{d}^\top \frac{\boldsymbol{z} _k}{\\vert\boldsymbol{z} _k\\vert} \rightarrow \\vert\boldsymbol{d}\\vert^2 = 1,\end{align*}$$故$\boldsymbol{d}^\top \boldsymbol{z} _k \rightarrow \infty$，于是对于所有满足$k \geq \bar{k}$和$2\boldsymbol{d}^\top \boldsymbol{z} _k > 1$的$k$有$$\begin{align*}\\vert \boldsymbol{z} _k - \boldsymbol{d} \\vert^2 = \\vert \boldsymbol{z} _k \\vert^2 - (2\boldsymbol{d}^\top \boldsymbol{z} _k - 1) < \\vert \boldsymbol{z} _k \\vert^2,\end{align*}$$这与$\boldsymbol{z} _k$是集合$C_k$中范数最小的向量矛盾.

![C1S4 Pic7][C1S4-pic7]

非空嵌套闭凸集序列$\{C_k\}$回缩仅仅是交集$\cap_{k=0}^\infty C_k$非空的充分条件，反过来则不成立.如右图(b)所示，非空嵌套闭凸集序列$\{C_k\}$的交集是$\{ (0, x_2) \ \vert \ x_2 \geq 0 \}$，但是$\{C_k\}$不是回缩的.

**命题1.4.18**：设$\{C_k\}$是非空嵌套闭凸集序列，记$R = \cap_{k=0}^\infty R_{C_k}$，$L = \cap_{k=0}^\infty L_{C_k}$.

若$R = L$，则$\{C_k\}$是回缩的，且交集$\cap_{k=0}^\infty C_k$非空，进一步，$$\begin{align*}\cap_{k=0}^\infty C_k = L + \tilde{C},\end{align*}$$其中$\tilde{C}$是非空紧集.
设$X$是回缩闭凸集，若$\bar{C}_k = X \cap C_k$非空且$R_X \cap R \subseteq L$，那么$\{\bar{C}_k\}$是回缩的且交集$\cap_{k=0}^\infty \bar{C}_k$非空.
**证明**：

令(b)中的$X = \mathbb{R}^n$，即可得(a)中前一半的结论.下面证明后一半结论，由凸集分解定理知$\cap_{k=0}^\infty C_k = L + \tilde{C}$，其中$$\begin{align*}\tilde{C} = (\cap_{k=0}^\infty C_k) \cap L^\perp,\end{align*}$$又子空间的回收锥就是它本身即$R_{L^\perp} = L^\perp$，由命题1.4.3(b)知$$\begin{align*}R_{(\cap_{k=0}^\infty C_k) \cap L^\perp} = R_{\cap_{k=0}^\infty C_k} \cap R_{L^\perp} = \cap_{k=0}^\infty R_{C_k} \cap L^\perp = R \cap L^\perp = L \cap L^\perp = \{ \boldsymbol{0} \},\end{align*}$$由命题1.4.3(a)$\tilde{C}$有界，故$\tilde{C}$是紧集.
由命题1.4.3(b)知$$\begin{align*}\cap_{k=0}^\infty R_{\bar{C}_k} = \cap_{k=0}^\infty R_{X \cap C_k} = \cap_{k=0}^\infty (R_X \cap R_{C_k}) = R_X \cap (\cap_{k=0}^\infty R_{C_k}) = R_X \cap R \subseteq L,\end{align*}$$那么对于$\{\bar{C}_k\}$的任意渐进序列$\{ \boldsymbol{x}_k \}$，其对应的$\boldsymbol{d} \in R_X \cap R \subseteq L$，于是对于$\forall k$有$\boldsymbol{x}_k - \boldsymbol{d} \in C_k$. 又$X$是回缩的且$\boldsymbol{d} \in R_X$，故对于充分大的$k$有$\boldsymbol{x}_k - \boldsymbol{d} \in X$，从而$\boldsymbol{x} - \boldsymbol{d} \in X \cap C_k = \bar{C}_k$，于是$\{ \boldsymbol{x}_k \}$是回缩的，由$\{ \boldsymbol{x}_k \}$的任意性知$\{\bar{C}_k\}$是回缩的，由命题1.4.17的结论知$\cap_{k=0}^\infty \bar{C}_k$非空.

![C1S4 Pic8][C1S4-pic8]

(b)中条件$X$是回缩的是必需的，如上图所示，$\cap_{k=0}^\infty C_k$是最左面的竖直线，左图中$X$是多面体，即是回缩的，交集$X \cap (\cap_{k=0}^\infty C_k)$非空；右图中$X$是非多面体，即是非回缩的，交集$X \cap (\cap_{k=0}^\infty C_k)$是空的.

**命题1.4.19**：设矩阵$\boldsymbol{Q} \in \mathbb{R}^{n \times n}$正定对称，设$\boldsymbol{c}, \boldsymbol{a}_1, \dots, \boldsymbol{a}_r \in \mathbb{R}^n$，$b_1, \dots, b_r$是标量，设优化问题$$\begin{align*}\min_{\boldsymbol{x}} & \ \boldsymbol{x}^\top \boldsymbol{Q} \boldsymbol{x} + \boldsymbol{c}^\top \boldsymbol{x} \\ \mbox{s.t.}    & \ \boldsymbol{a}_j^\top \boldsymbol{x} \leq b_j, \ j = 1, \dots, r,\end{align*}$$
的最优目标函数是有限值，那么其至少有一个最优解.

**证明**：记$$\begin{align*}f(\boldsymbol{x}) = \boldsymbol{x}^\top \boldsymbol{Q} \boldsymbol{x} + \boldsymbol{c}^\top \boldsymbol{x}, \ X = \{ \boldsymbol{x} \ \vert \ \boldsymbol{a}_j^\top \boldsymbol{x} \leq b_j, j = 1, \dots, r \}.\end{align*}$$记$f^*$为最优目标函数值，设标量序列$\{\gamma_k\}$满足$\gamma_k \rightarrow f^*$，并记$$\begin{align*}\bar{C}_k = X \cap \{ \boldsymbol{x} \ \vert \ \boldsymbol{x}^\top \boldsymbol{Q} \boldsymbol{x} + \boldsymbol{c}^\top \leq \gamma_k \}.\end{align*}$$故只需证$\cap_{k=0}^\infty \bar{C}_k$非空.设$R_X$是$X$的回收锥，$R$和$L$分别是集合$\{ \boldsymbol{x} \in \mathbb{R}^n \ \vert \ \boldsymbol{x}^\top \boldsymbol{Q} \boldsymbol{x} + \boldsymbol{c}^\top \leq \gamma_k \}$的回收锥及其线性空间，由例1.4.6知$$\begin{align*}R = \{ \boldsymbol{d} \ \vert \ \boldsymbol{Q} \boldsymbol{d} = \boldsymbol{0} , \boldsymbol{c}^\top \boldsymbol{d} \leq 0 \}, \ L = \{ \boldsymbol{d} \ \vert \ \boldsymbol{Q} \boldsymbol{d} = \boldsymbol{0} , \boldsymbol{c}^\top \boldsymbol{d} = 0 \}, \ R_X = \{ \boldsymbol{d} \ \vert \ \boldsymbol{a}_j^\top \boldsymbol{d} \leq 0, j = 1, \dots, r \}.\end{align*}$$若$\boldsymbol{d} \in R_X \cap R$且$\boldsymbol{d} \not \in L$，那么$$\begin{align*}\boldsymbol{Q} \boldsymbol{d} = \boldsymbol{0} , \ \boldsymbol{c}^\top \boldsymbol{d} < 0, \ \boldsymbol{a}_j^\top \boldsymbol{d} \leq 0, \ j = 1, \dots, r,\end{align*}$$这意味着对于$\forall \boldsymbol{x} \in X$和$\forall \alpha \geq 0$有$\boldsymbol{x} + \alpha \boldsymbol{d} \in X$，同时当$\alpha \rightarrow \infty$时有$f(\boldsymbol{x} + \alpha \boldsymbol{d}) \rightarrow -\infty$，这与$f^*$有限矛盾，故$R_X \cap R \subseteq L$，由命题1.4.18(b)知$\cap_{k=0}^\infty \bar{C}_k$非空.

![C1S4 Pic9][C1S4-pic9]

若$C$是闭集，$\boldsymbol{A}$是矩阵，$\boldsymbol{A} \cdot C$是否是闭集？设序列$\{\boldsymbol{y}_k\} \in \boldsymbol{A} \cdot C$收敛于$\bar{\boldsymbol{y}} \in \mathbb{R}^n$，那么问题等价于$\bar{\boldsymbol{y}} \in \boldsymbol{A} \cdot C$是否成立.如右图所示，引入集合$C_k = C \cap N_k$，其中$$\begin{align*}N_k = \{ \boldsymbol{x} \ \vert \ \|\boldsymbol{A} \boldsymbol{x} - \bar{\boldsymbol{y}}\| \leq \|\boldsymbol{y}_k - \bar{\boldsymbol{y}}\| \},\end{align*}$$于是问题等价于$\cap_{k=0}^\infty C_k$是否非空.因此之前关于闭凸集交集非空的条件可以转换为闭凸集在线性变换下保持闭性的条件.

**命题1.4.20**：设$X$和$C$是$\mathbb{R}^n$中的非空闭凸集，矩阵$\boldsymbol{A} \in \mathbb{R}^{m \times n}$，若$X$是回缩闭凸集且$$\begin{align*}R_X \cap R_C \cap \mathit{Nul}(\boldsymbol{A}) \subseteq L_C,\end{align*}$$那么$\boldsymbol{A} \cdot (X \cap C)$是闭凸集.

**证明**：设序列$\{y_k\}$属于集合$\boldsymbol{A} \cdot (X \cap C)$且收敛于$\bar{\boldsymbol{y}}$，下面只需证$\bar{\boldsymbol{y}} \in \boldsymbol{A} \cdot (X \cap C)$. 如右图所示，设$C_k = C \cap N_k$，其中$$\begin{align*}N_k = \{ \boldsymbol{x} \ \vert \ \|\boldsymbol{A} \boldsymbol{x} - \bar{\boldsymbol{y}}\| \leq \|\boldsymbol{y}_k - \bar{\boldsymbol{y}}\| \},\end{align*}$$显然以$\bar{\boldsymbol{y}}$为球心$\|\boldsymbol{y}_k - \bar{\boldsymbol{y}}\|$为半径的闭球是紧集，由命题1.4.3(d)和命题1.4.5(d)知$$\begin{align*}R_{C_k} = R_C \cap \mathit{Nul}(\boldsymbol{A}), \ L_{C_k} = L_C \cap \mathit{Nul}(\boldsymbol{A}),\end{align*}$$易知有$$\begin{align*}R_{\cap_{k=0}^\infty C_k} = \cap_{k=0}^\infty R_{C_k} = R_C \cap \mathit{Nul}(\boldsymbol{A}), \ L_{\cap_{k=0}^\infty C_k} = \cap_{k=0}^\infty L_{C_k} = L_C \cap \mathit{Nul}(\boldsymbol{A}),\end{align*}$$于是$$\begin{align*}R_X \cap R_{\cap_{k=0}^\infty C_k} = R_X \cap R_C \cap \mathit{Nul}(\boldsymbol{A}),\end{align*}$$显然$R_X \cap R_C \cap \mathit{Nul}(\boldsymbol{A}) \subseteq \mathit{Nul}(\boldsymbol{A})$，结合$R_X \cap R_C \cap \mathit{Nul}(\boldsymbol{A}) \subseteq L_C$知$$\begin{align*}R_X \cap R_C \cap \mathit{Nul}(\boldsymbol{A}) \subseteq L_C \cap \mathit{Nul}(\boldsymbol{A}),\end{align*}$$这意味着$$\begin{align*}R_X \cap R_{\cap_{k=0}^\infty C_k} \subseteq L_{\cap_{k=0}^\infty C_k}.\end{align*}$$由命题1.4.18(b)知$\cap_{k=0}^\infty (X \cap C_k) = \cap_{k=0}^\infty (X \cap C \cap N_k) = X \cap C \cap (\cap_{k=0}^\infty N_k)$非空，对于$\forall \boldsymbol{x} \in X \cap C \cap (\cap_{k=0}^\infty N_k)$，显然有$\boldsymbol{x} \in X \cap C$且$\boldsymbol{A}\boldsymbol{x} = \bar{\boldsymbol{y}}$，故$\bar{\boldsymbol{y}} \in \boldsymbol{A} \cdot (X \cap C)$.

![C1S4 Pic10][C1S4-pic10]

$X$回缩是必要的，如上图所示.下面考虑一些特例：

设$C = \mathbb{R}^n$，$X$是多面体，易知$L_C = \mathbb{R}^n$，故命题1.4.20中的条件都成立，于是$\boldsymbol{A} \cdot X$是闭集，即多面体在线性变换下的象是闭集.设$\boldsymbol{A} = [\boldsymbol{a}_1, \dots, \boldsymbol{a}_r]$，$C = \{ (\alpha_1, \dots, \alpha_r) \ \vert \ \alpha_i \geq 0, 1 \leq i \leq r \}$，显然$C$是多面体，于是$\boldsymbol{A} \cdot C$是向量$\boldsymbol{a}_1, \dots, \boldsymbol{a}_r$生成的锥，是闭集.
设$X = \mathbb{R}^n$，则命题1.4.20等价于若$R_C \cap \mathit{Nul}(\boldsymbol{A}) \subseteq L_C$，则$\boldsymbol{A} \cdot C$是闭集，特别的，若$R_C \cap \mathit{Nul}(\boldsymbol{A}) = \{ \boldsymbol{0} \}$，则$\boldsymbol{A} \cdot C$是闭集，参考如下命题.

**命题1.4.21**：设$C_1, \dots, C_m$是$\mathbb{R}^n$的非空闭凸子集且满足若$\boldsymbol{d}_1 + \dots + \boldsymbol{d}_m = \boldsymbol{0} , \boldsymbol{d}_i \in R_{C_i}$则$\boldsymbol{d}_i \in L_{C_i}, i= 1, \dots, m$，于是$C_1 + \dots + C_m$是闭集.

**证明**：设$C = C_1 \times \dots \times C_m$，则$C$是闭凸集，由定义不难证明$$\begin{align*}R_C = R_{C_1} \times \dots \times R_{C_k}, \ L_C = L_{C_1} \times \dots \times L_{C_k}.\end{align*}$$对于任意$\boldsymbol{d} = [\boldsymbol{d}_1^\top, \dots, \boldsymbol{d}_m^\top]^\top \in R_C$，由命题1.4.2(b)知存在$\boldsymbol{x} = [\boldsymbol{x}_1^\top, \dots, \boldsymbol{x}_m^\top]^\top \in C$使得对于$\forall \alpha \geq 0$满足$\boldsymbol{x} + \alpha \boldsymbol{d} \in C$，即存在$\boldsymbol{x}_i \in C_i$和$\boldsymbol{d}_i \in R_{C_i}$使得对于$\forall \alpha \geq 0$满足$\boldsymbol{x}_i + \alpha \boldsymbol{d}_i \in C$.

考虑线性变换$\boldsymbol{A}: \mathbb{R}^{mn} \mapsto \mathbb{R}^n = (\boldsymbol{I}_n, \dots, \boldsymbol{I}_n)$，即$$\begin{align*}\boldsymbol{A}\begin{bmatrix}\boldsymbol{x}_1 \\ \vdots \\ \boldsymbol{x}_m \end{bmatrix} = \boldsymbol{x}_1 + \dots + \boldsymbol{x}_m, \ \boldsymbol{x}_1, \dots, \boldsymbol{x}_m \in \mathbb{R}^n.\end{align*}$$则$$\begin{align*}\mathit{Nul}(\boldsymbol{A}) = \{ (\boldsymbol{d}_1^\top, \dots, \boldsymbol{d}_m^\top)^\top \ \vert \ \boldsymbol{d}_1 + \dots + \boldsymbol{d}_m = \boldsymbol{0} \},\end{align*}$$于是由题设条件$$\begin{align*}R_C \cap \mathit{Nul}(\boldsymbol{A}) & = \{ (\boldsymbol{d}_1^\top, \dots, \boldsymbol{d}_m^\top)^\top \ \vert \ \boldsymbol{d}_1 + \dots + \boldsymbol{d}_m = \boldsymbol{0} , \boldsymbol{d}_i \in R_{C_i}, 1 \leq i \leq m \} \\ & \subseteq \{ (\boldsymbol{d}_1^\top, \dots, \boldsymbol{d}_m^\top)^\top \ \vert \ \boldsymbol{d}_i \in L_{C_i}, 1 \leq i \leq m \} \\ & = L_C,\end{align*}$$由命题1.4.20的结论知$\boldsymbol{A} \cdot C = C_1 + \dots + C_m$是闭集.

若只有两个集合$C_1$和$C_2$，那么由命题1.4.21知$C_1 - C_2$为闭集当且仅当$C_1$和$C_2$没有公共的非零回收方向，即$$\begin{align*}R_{C_1} \cap R_{C_2} = \emptyset,\end{align*}$$因此若$C_1$和$C_2$任意一个是紧集，都有$C_1 - C_2$是闭集.

此外，有限个多面体的向量和构成的集合也是闭集，因为这可以看成它们Cartesian积的线性变换，而多面体的Cartesian积还是多面体且多面体在线性变换下的象是闭集.

# C1S5 - 超平面
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

# C1S6 - 共轭函数
![C1S6 Pic1][C1S6-pic1]

这一节将介绍凸优化里一个很重要的概念——共轭变换，它给我们提供了另一个研究凸函数的视角.其背后想法是，对于凸函数$f$，通过它的共轭函数(conjugate function)，即一系列和$f$相关的仿射函数来描述它.此外，当$f$是正常闭凸函数时，这种变换还是对称的，也即$f$的共轭函数的共轭函数就是它本身，这个有趣的性质会给后面的计算和分析带来便利.

扩展实值函数$f: \mathbb{R}^n \mapsto [-\infty, \infty]$的共轭函数$f^*: \mathbb{R}^n \mapsto [-\infty, \infty]$是$$\begin{align*} f^*(\boldsymbol{y}) = \sup_{\boldsymbol{x} \in \mathbb{R}^n} \{ \boldsymbol{x}^\top \boldsymbol{y} - f(\boldsymbol{x}) \}, \ \boldsymbol{y} \in \mathbb{R}^n. \end{align*}$$如右图所示，$f$的上境图的法向量为$( -\boldsymbol{y}, 1)$的支撑超平面与竖轴的交点是$-f^*(\boldsymbol{y})$.由于$f^*$是对仿射函数逐点取上确界，故由命题1.1.10知不管$f$是何形式，$f^*$都是闭凸函数.注意即使$f$是正常函数，$f^*$也不一定是正常函数，但若$f$是凸函数，那么$f^*$是正常闭凸函数当且仅当$f$是正常函数.

扩展实值函数$f: \mathbb{R}^n \mapsto [-\infty, \infty]$的二次共轭函数$f^{**}: \mathbb{R}^n \mapsto [-\infty, \infty]$是其共轭函数$f^*$的共轭函数，$$\begin{align*} f^{**}(\boldsymbol{x}) = \sup_{\boldsymbol{y} \in \mathbb{R}^n} \{ \boldsymbol{y}^\top \boldsymbol{x} - f^*(\boldsymbol{y}) \}, \ \boldsymbol{x} \in \mathbb{R}^n. \end{align*}$$

![C1S6 Pic2][C1S6-pic2]

如上图所示，对于$\forall \boldsymbol{x} \in \mathbb{R}^n$，考虑过$(\boldsymbol{x}, 0)$的垂直直线，对于$\forall \boldsymbol{y} \in dom(f^*)$，考虑$f$上境图的法向量为$( -\boldsymbol{y}, 1)$的支撑超平面，这两条直线的交点即是$(\boldsymbol{x}, \boldsymbol{y}^\top \boldsymbol{x} - f^*(\boldsymbol{y}))$，故$f^{**}$就是这个交点能达到的上确界，从图上能看到，$f^{**}$是$f$的闭凸包.

![C1S6 Pic3][C1S6-pic3]

**例1.6.1**：下面来看几个简单例子，如右图所示

$f(x) = \alpha x - \beta$，则$$\begin{align*} f^*(y) = \sup_{x \in \mathbb{R}} \{ yx - \alpha x + \beta \} = \sup_{x \in \mathbb{R}} \{ (y - \alpha) x \} + \beta = \begin{cases} \beta, & y = \alpha; \\ \infty, & y \neq \alpha.\end{cases} \end{align*}$$且$$\begin{align*} f^{**}(x) = \sup_{y \in \mathbb{R}} \{ xy - f^*(y) \} = x \alpha - f^*(\alpha) = \alpha x - \beta = f(x). \end{align*}$$
$f(x) = \vertx\vert$，则$$\begin{align*} f^*(y)  = \sup_{x \in \mathbb{R}} \{ yx - \vertx\vert \} = \begin{cases} \sup_{x \geq 0} (y - 1)x \\ \sup_{x \leq 0} (y + 1)x \end{cases} = \begin{cases} 0, & \verty\vert \leq 1; \\ \infty, & \verty\vert > 1. \end{cases} \end{align*}$$且$$\begin{align*} f^{**}(x) = \sup_{y \in \mathbb{R}} \{ xy - f^*(y) \} = \sup_{\verty\vert \leq 1} \{ xy - 0 \} = \vertx\vert = f(x). \end{align*}$$
$f(x) = \frac{c}{2}x^2$，则$$\begin{align*} f^*(y) = \sup_{x \in \mathbb{R}} \{ yx - \frac{c}{2}x^2 \} = y \frac{y}{c} - \frac{c}{2} \frac{y}{c} \frac{y}{c} = \frac{y^2}{c} - \frac{y^2}{2c} = \frac{y^2}{2c}. \end{align*}$$且$$\begin{align*} f^{**}(x) = \sup_{y \in \mathbb{R}} \{ xy - f^*(y) \} = \sup_{y \in \mathbb{R}} \{ xy - \frac{y^2}{2c} \} = x (cx) - \frac{(cx)^2}{2c} = \frac{c}{2}x^2 = f(x). \end{align*}$$
命题1.6.2[共轭定理]：扩展实值函数$f: \mathbb{R}^n \mapsto [-\infty, \infty]$的共轭函数和二次共轭函数分别是$f^*$和$f^{**}$，那么

$f(\boldsymbol{x}) \geq f^{**}(\boldsymbol{x}), \forall \boldsymbol{x} \in \mathbb{R}^n$.
当$f$是凸函数时，$f$，$f^*$和$f^{**}$这三个函数中若有一个是正常函数，则其它两个也是正常函数.
若$f$是正常闭凸函数，则$f(\boldsymbol{x}) = f^{**}(\boldsymbol{x}), \forall \boldsymbol{x} \in \mathbb{R}^n$.
$f$的共轭函数与其闭凸包的共轭函数等价，若$cl(conv(f))$是正常函数，则$cl(conv(f))(\boldsymbol{x}) = f^{**}(\boldsymbol{x}), \forall \boldsymbol{x} \in \mathbb{R}^n$.
证明：

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

支撑函数的几何示意图如右图所示，对于给定非空集合$X$和向量$\boldsymbol{y}$，将$X$投影到$\boldsymbol{y}$上，设$y$方向的极点为$\hat{\boldsymbol{x}}$，那么$$\begin{align*} \sigma_X(\boldsymbol{y}) = \\vert\hat{\boldsymbol{x}}\\vert \cdot \\vert\boldsymbol{y}\\vert. \end{align*}$$

例1.6.4[极锥]：设$C$为凸锥，由例1.6.3知$$\begin{align*} \sigma_C(\boldsymbol{y}) = \sup_{\boldsymbol{x} \in C} \boldsymbol{y}^\top \boldsymbol{x} = \begin{cases} 0 & \boldsymbol{y}^\top \boldsymbol{x} \leq 0, \forall \boldsymbol{x} \in C, \\ \infty & otherwise. \end{cases} \end{align*}$$故$\sigma_C(\boldsymbol{y})$是$C$的极锥(polar cone)$$\begin{align*} C^* = \{ \boldsymbol{y} \ \vert \ \boldsymbol{y}^\top \boldsymbol{x} \leq 0, \forall \boldsymbol{x} \in C \} \end{align*}$$的示性函数.又$C^*$是闭凸锥，同理可得$C^*$的支撑函数是$(C^*)^*$的示性函数.注意，$C^*$的支撑函数是$C^*$的示性函数的共轭函数，即$C$的示性函数的共轭函数的共轭函数，由共轭定理(d)知这等于$C$的示性函数的闭凸包，又$C$的示性函数的闭凸包是$C$的闭凸包的示性函数，综上，$(C^*)^*$的示性函数等于$C$的闭凸包的示性函数.注意$C$是凸锥，故$C$的闭凸包也即$C$的闭包，于是可得$(C^*)^* = cl(C)$，这是极锥定理的一个特例.

考虑一个特殊的例子，$C = cone({\boldsymbol{a}_1, \dots, \boldsymbol{a}_r})$，于是$C$可以看作正象限集合$\{ \boldsymbol{\alpha} \ \vert \ \boldsymbol{\alpha} \geq 0 \}$在线性变换$\sum_{j=1}^r \alpha_j \boldsymbol{a}_j$下的象，易知$C$是闭凸锥，那么易知有$(C^*)^* = C$，这就是有名的Farkas'引理.

若$C$是任意集合，除非$C$是锥，否则$C$的支撑函数将不再是示性函数，$(C^*)^* = C$也不会成立，但是若$C$是凸的，仍有$(C^*)^* = cl(cone(C))$成立，这在第二章会给出证明.



### 转载信息
这是一篇转载的博文，原地址为：

<del>[《凸优化理论》C1S1](http://www.cnblogs.com/murongxixi/p/3592798.html)</del>、
<del>[《凸优化理论》C1S2](http://www.cnblogs.com/murongxixi/p/3594796.html)</del>、
<del>[《凸优化理论》C1S3](http://www.cnblogs.com/murongxixi/p/3598645.html)</del>、
<del>[《凸优化理论》C1S4](http://www.cnblogs.com/murongxixi/p/3602923.html)</del>、
<del>[《凸优化理论》C1S5](http://www.cnblogs.com/murongxixi/p/3615034.html)</del>、
<del>[《凸优化理论》C1S6](http://www.cnblogs.com/murongxixi/p/3617054.html)</del>、

原博客无法进入，备用链接：

[《凸优化理论》C1S1](https://www.tuicool.com/articles/ye6Zze)、
[《凸优化理论》C1S2](https://www.tuicool.com/articles/NjyM7r)、
[《凸优化理论》C1S3](https://www.tuicool.com/articles/QRJJV3)、
[《凸优化理论》C1S4](https://www.tuicool.com/articles/nMnEveR)、
[《凸优化理论》C1S5](https://www.tuicool.com/articles/eQBFzyM)、
[《凸优化理论》C1S6](https://www.tuicool.com/articles/iYF3yu2)







[C1S1-pic1]: {{"/assets/images/C1S1-pic1.png" \vert site.baseurl }}
[C1S1-pic2]: {{"/assets/images/C1S1-pic2.png" \vert site.baseurl }}
[C1S1-pic3]: {{"/assets/images/C1S1-pic3.png" \vert site.baseurl }}

[C1S2-pic1]: {{"/assets/images/C1S2-pic1.png" \vert site.baseurl }}
[C1S2-pic2]: {{"/assets/images/C1S2-pic2.png" \vert site.baseurl }}

[C1S3-pic1]: {{"/assets/images/C1S3-pic1.png" \vert site.baseurl }}
[C1S3-pic2]: {{"/assets/images/C1S3-pic2.png" \vert site.baseurl }}
[C1S3-pic3]: {{"/assets/images/C1S3-pic3.png" \vert site.baseurl }}
[C1S3-pic4]: {{"/assets/images/C1S3-pic4.png" \vert site.baseurl }}

[C1S4-pic1]: {{"/assets/images/C1S4-pic1.png" \vert site.baseurl }}
[C1S4-pic2]: {{"/assets/images/C1S4-pic2.png" \vert site.baseurl }}
[C1S4-pic3]: {{"/assets/images/C1S4-pic3.png" \vert site.baseurl }}
[C1S4-pic4]: {{"/assets/images/C1S4-pic4.png" \vert site.baseurl }}
[C1S4-pic5]: {{"/assets/images/C1S4-pic5.png" \vert site.baseurl }}
[C1S4-pic6]: {{"/assets/images/C1S4-pic6.png" \vert site.baseurl }}
[C1S4-pic7]: {{"/assets/images/C1S4-pic7.png" \vert site.baseurl }}
[C1S4-pic8]: {{"/assets/images/C1S4-pic8.png" \vert site.baseurl }}
[C1S4-pic9]: {{"/assets/images/C1S4-pic9.png" \vert site.baseurl }}
[C1S4-pic10]: {{"/assets/images/C1S4-pic10.png" \vert site.baseurl }}

[C1S5-pic1]: {{"/assets/images/C1S5-pic1.png" \vert site.baseurl }}
[C1S5-pic2]: {{"/assets/images/C1S5-pic2.png" \vert site.baseurl }}
[C1S5-pic3]: {{"/assets/images/C1S5-pic3.png" \vert site.baseurl }}
[C1S5-pic4]: {{"/assets/images/C1S5-pic4.png" \vert site.baseurl }}
[C1S5-pic5]: {{"/assets/images/C1S5-pic5.png" \vert site.baseurl }}
[C1S5-pic6]: {{"/assets/images/C1S5-pic6.png" \vert site.baseurl }}
[C1S5-pic7]: {{"/assets/images/C1S5-pic7.png" \vert site.baseurl }}

[C1S6-pic1]: {{"/assets/images/C1S6-pic1.png" \vert site.baseurl }}
[C1S6-pic2]: {{"/assets/images/C1S6-pic2.png" \vert site.baseurl }}
[C1S6-pic3]: {{"/assets/images/C1S6-pic3.png" \vert site.baseurl }}
[C1S6-pic4]: {{"/assets/images/C1S6-pic4.png" \vert site.baseurl }}
