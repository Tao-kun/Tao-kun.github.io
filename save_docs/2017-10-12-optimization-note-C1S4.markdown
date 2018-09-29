---
layout: post
title:  "[转] C1S4 - 回收锥"
date:   2017-10-12 18:04:00 +0800
tags: [Mathematics]
---

《凸优化理论》笔记

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

回缩集合序列的任一渐进序列，沿其对应的公共回收方向$\boldsymbol{d}$反向平移后，都存在充分大的$\bar{k}$，使得$\boldsymbol{x}_k \in C_k, k \geq \bar{k}$.例如设$C_k = \{ (x_1, x_2) \ \vert \ \vert x_1\vert \leq 1/k \}$，则其渐进序列是回缩的：若$\boldsymbol{x}_{k,1} \rightarrow 0$，$\boldsymbol{x}_{k,2} \rightarrow \infty$，则对应$\boldsymbol{d} = (0, 1)$；若$\boldsymbol{x}_{k,1} \rightarrow 0$，$\boldsymbol{x}_{k,2} \rightarrow -\infty$，则对应$\boldsymbol{d} = (0, -1)$.

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


[C1S4-pic1]: {{"/assets/images/C1S4-pic1.png" | site.baseurl }}
[C1S4-pic2]: {{"/assets/images/C1S4-pic2.png" | site.baseurl }}
[C1S4-pic3]: {{"/assets/images/C1S4-pic3.png" | site.baseurl }}
[C1S4-pic4]: {{"/assets/images/C1S4-pic4.png" | site.baseurl }}
[C1S4-pic5]: {{"/assets/images/C1S4-pic5.png" | site.baseurl }}
[C1S4-pic6]: {{"/assets/images/C1S4-pic6.png" | site.baseurl }}
[C1S4-pic7]: {{"/assets/images/C1S4-pic7.png" | site.baseurl }}
[C1S4-pic8]: {{"/assets/images/C1S4-pic8.png" | site.baseurl }}
[C1S4-pic9]: {{"/assets/images/C1S4-pic9.png" | site.baseurl }}
[C1S4-pic10]: {{"/assets/images/C1S4-pic10.png" | site.baseurl }}

