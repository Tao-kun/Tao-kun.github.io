---
layout: post
title:  "《凸优化理论》笔记 - C1S1"
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

于是存在序列$\{\boldsymbol{x}_k\}$的一个子序列$\{\boldsymbol{x}_k\}_\mathcal{K}$对于$\forall k \in \mathcal{K}$有$f(\boldsymbol{x}_k) \leq \gamma$，即$\{\boldsymbol{x}_k\}_\mathcal{K} \subseteq S_\gamma$，因为水平集$S_\gamma$是闭的，故$\boldsymbol{x}bar \in S_\gamma$，即$f(\boldsymbol{x}bar) \leq \gamma$，矛盾.

2$\Rightarrow$3：设$epi(f)$中的序列$\{(\boldsymbol{x}_k, w_k)\}$收敛于$(\boldsymbol{x}bar, \bar{\boldsymbol{w}})$，由上境图的定义知$f(\boldsymbol{x}_k) \leq w_k$，取极限令$k \rightarrow \infty$并结合下半连续的定义知

$$
\begin{align*}
f(\boldsymbol{x}bar)
\leq \liminf_{k \rightarrow \infty} f(\boldsymbol{x}_k)
= \lim_{k \rightarrow \infty} f(\boldsymbol{x}_k)
\leq \bar{\boldsymbol{w}}
\end{align*}
$$

因此，$(\boldsymbol{x}bar, \bar{\boldsymbol{w}}) \in epi(f)$，故$epi(f)$是闭的.

3$\Rightarrow$1：设水平集$S_\gamma$中的序列$\{\boldsymbol{x}_k\}$收敛于$\boldsymbol{x}bar$，于是对于$\forall k$有$(\boldsymbol{x}_k, \gamma) \in epi(f)$，因为$epi(f)$是闭的，故序列$\{(\boldsymbol{x}_k, \gamma)\}$的极限$(\boldsymbol{x}bar, \gamma) \in epi(f)$，即$\boldsymbol{x}bar \in S_\gamma$，故$S_\gamma$是闭的.

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

**证明**：点$(\boldsymbol{x}, w) \in epi(F)$当且仅当$F(\boldsymbol{x}) \leq w$，即当且仅当$f_i(\boldsymbol{x}) \leq w, i \in I$，即$(\boldsymbol{x}, w) \in \cap_{i \in I} epi(f_i)$，即

$$
\begin{align*}
epi(F) = \cap_{i \in I} epi(f_i)
\end{align*}
$$

若$f_i, i \in I$是凸的，由命题1.1.4知$epi(f_i)$是凸的，再由命题1.1.2(a)知$epi(F)$是凸的.若$f_i, i \in I$是闭的，由命题1.1.6知$epi(f_i)$是闭的，故$epi(F)$是闭的.

对于一阶和二阶可微凸函数，有一些额外的解析性质，还可以以此判别凸性.

**命题1.1.11** [**一阶性质**]：凸集$C$是$\mathbb{R}^n$的非空子集，函数$f: C \rightarrow \mathbb{R}$一阶可微，那么$f$是凸函数当且仅当对于$\forall \boldsymbol{x}, \boldsymbol{z} \in C$有

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

**命题1.1.12** [**二阶性质**]：凸集$C$是$\mathbb{R}^n$的非空子集，函数$f: C \rightarrow \mathbb{R}$二阶可微，那么

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


[C1S1-pic1]: {{"/assets/images/C1S1-pic1.png" | site.baseurl }}
[C1S1-pic2]: {{"/assets/images/C1S1-pic2.png" | site.baseurl }}
[C1S1-pic3]: {{"/assets/images/C1S1-pic3.png" | site.baseurl }}