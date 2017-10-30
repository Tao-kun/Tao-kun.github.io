---
layout: post
title:  "C1S2 - 凸包和仿射包"
date:   2017-10-12 18:04:00 +0800
tags: [Mathematics]
---

《凸优化理论》笔记

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

1. $X$，$conv(X)$和$cl(X)$有相同的仿射包.
2. $cone(X) = cone(conv(X))$.
3. $aff(conv(X)) \subseteq aff(cone(X))$.
4. 如果$\boldsymbol{0} \in conv(X)$，那么$aff(conv(X)) = aff(cone(X))$.

**证明**：

1.先证$X$和$cl(X)$有相同的仿射包.一方面，由$X \subseteq cl(X)$易知有$aff(X) \subseteq aff(cl(X))$.另一方面，$X \subseteq aff(X)$，而$aff(X)$是闭集，由闭包的定义知$cl(X) \subseteq aff(X)$，故$aff(cl(X)) \subseteq aff(X)$. 再证$X$和$conv(X)$有相同的仿射包，不妨设$\boldsymbol{0} \in X$，否则可以将$X$平移使其包含$\boldsymbol{0}$，这不影响结论.于是$aff(X)$和$aff(conv(X))$都是子空间.一方面，由$X \subseteq conv(X)$易知有$aff(X) \subseteq aff(conv(X))$.另一方面，设$aff(conv(X))$的维度为$m$，易知存在$\boldsymbol{x}_1, \dots, \boldsymbol{x}_m \in conv(X)$张成了$aff(conv(X))$，于是$\forall \boldsymbol{x} \in aff(conv(X))$都可以写成$\boldsymbol{x}_1, \dots, \boldsymbol{x}_m$的线性组合，由凸包的定义知$\boldsymbol{x}_i, 1 \leq i \leq m$都是$X$中元素的凸组合，故$\boldsymbol{x}$也是$X$中元素的线性组合，所以$\boldsymbol{x} \in aff(X)$，于是$aff(conv(X)) \subseteq aff(X)$.

2.因为$X \subseteq conv(X)$，故$cone(X) \subseteq cone(conv(X))$；对于$\forall \boldsymbol{x} \in cone(conv(X))$，由锥的定义知$\boldsymbol{x}$是$conv(X)$中元素的非负组合，又$conv(X)$中元素是$X$中元素的凸组合，故$\boldsymbol{x}$是$X$中元素的非负组合，所以，$\boldsymbol{x} \in cone(X)$，于是$cone(conv(X)) \subseteq cone(X)$.
.
3.因为$conv(X)$是$X$中所有元素的凸组合，$cone(X)$是$X$中所有元素的非负组合，故$conv(X) \subseteq cone(X)$，于是$aff(conv(X)) \subseteq aff(cone(X))$. 
事实上，设$X = \{(1, 1)\} \in \mathbb{R}^2$，那么$conv(X) = X$，$cone(X) = \{(\alpha, \alpha) \ \vert \ \alpha \geq 0 \}$，于是

$$
\begin{align*}
aff(conv(X)) & = \{(1, 1)\} \\
aff(cone(X)) & = \{(x_1, x_2) \vert x_1 = x_2 \}
\end{align*}
$$

即$aff(conv(X))$是$aff(cone(X))$的真子集.

4.由(1)和(3)的结论知，只需证$aff(cone(X)) \subseteq aff(X)$.由于$\boldsymbol{0} \in cone(X)$，故$aff(cone(X))$是一个子空间，设$aff(cone(X))$的维度为$m$，易知存在$\boldsymbol{x}_1, \dots, \boldsymbol{x}_m \in cone(X)$张成了$aff(cone(X))$，于是$\forall \boldsymbol{x} \in aff(cone(X))$都可以写成$\boldsymbol{x}_1, \dots, \boldsymbol{x}_m$的线性组合，由锥的定义知$\boldsymbol{x}_i, 1 \leq i \leq m$都是$X$中元素的非负组合，故$\boldsymbol{x}$也是$X$中元素的线性组合.又$\boldsymbol{0} \in conv(X)$，故$aff(conv(X))$是一个子空间，由(1)知，$aff(X)$是子空间，因此有$\boldsymbol{x} \in aff(X)$，于是$aff(cone(X)) \subseteq aff(X)$.

**命题1.2.2** [**Caratheodory's定理**]：集合$X$是$\mathbb{R}^n$的非空子集，则

1. $cone(X)$中的任意非零向量可表示为$X$中的线性无关的向量的正组合.
2. $conv(X)$中的任意向量可表示为$X$中不超过$n + 1$个向量的凸组合，$n$是$X$的仿射包的维度.

**证明**：

1. 设向量$\boldsymbol{x} \neq \boldsymbol{0} \in cone(X)$，设$m$是最小的使得$\boldsymbol{x}$满足如下形式

$$
\begin{align*}
\sum_{i=1}^m \alpha_i \boldsymbol{x}_i,
\alpha_i > 0,
\boldsymbol{x}_i \in X,
i = 1, \dots, m
\end{align*}
$$

的正整数，那么向量$$\boldsymbol{x}_i, i = 1, \dots, m$$必然是线性无关的.

反证法，假设向量$$\boldsymbol{x}_i$$线性相关，那么存在实数$$\lambda_1, \dots, \lambda_m$$满足$$\sum_{i=1}^m \lambda_i \boldsymbol{x}_i = \boldsymbol{0}$$且至少有一个$$\lambda_i$$是正数，考虑线性组合$$\sum_{i=1}^m (\alpha_i - \bar{\gamma} \lambda_i) \boldsymbol{x}_i$$，其中$$\bar{\gamma}$$是使得$$\alpha_i - \gamma \lambda_i \geq 0$$对所有$$i$$成立的最大的$$\gamma$$，这个线性组合给出了$$\boldsymbol{x}$$的一个少于$$m$$个向量的正组合，矛盾，故向量$$\boldsymbol{x}_i, i = 1, \dots, m$$必然是线性无关的.

![C1S2 Pic2][C1S2-pic2]

2. 如右图所示，考虑$\mathbb{R}^{n+1}$中的子集：$Y = \{ (y, 1) \ \vert \ y \in X \}$. 如果$\boldsymbol{x} \in conv(X)$，那么$\boldsymbol{x}$可表示为
 
$$
\begin{align*}
\boldsymbol{x}
= \sum_{i=1}^I \gamma_i \boldsymbol{x}_i, I > 0
, \gamma_i \geq 0, \sum_{i=1}^I \gamma_i = 1
\end{align*}
$$

于是$$(\boldsymbol{x}, 1) = (\sum_{i=1}^I \gamma_i \boldsymbol{x}_i, \sum_{i=1}^I \gamma_i) = \sum_{i=1}^I \gamma_i (\boldsymbol{x}_i, 1) \in cone(Y)$$，由(a)易知

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

**证明**：只需证明$$conv(X)$$中的序列$$\{\boldsymbol{x}_k\}$$收敛时，其极限$$\bar{\boldsymbol{x}} \in conv(X)$$即可.由Caratheodory's定理易知序列中的任意$$\boldsymbol{x}_k$$可表示为$$n + 1$$个向量$$\boldsymbol{x}_{k,1}, \dots, \boldsymbol{x}_{k,n+1}$$的凸组合，即 

$$
\begin{align*}
\boldsymbol{x}_k = \alpha_{k,1} \boldsymbol{x}_{k,1} + \dots + \alpha_{k,n+1} \boldsymbol{x}_{k,n+1}, \sum_{i=1}^{n+1} \alpha_{k,i} = 1, \alpha_{k,i} \geq 0, i = 1, \dots, n+1
\end{align*}
$$

令

<!--
$$
\begin{align*}
\tilde{{\boldsymbol{\alpha}}}_k = \begin{bmatrix} \alpha_{k,1} \\
\vdots \\
\alpha_{k,n+1} \end{bmatrix} \in \mathbb{R}^{n+1},
\tilde{\boldsymbol{x}}_k = \begin{bmatrix} \boldsymbol{x}_{k,1} \\
\vdots \\
\boldsymbol{x}_{k,n+1} \end{bmatrix} \in \mathbb{R}^{(n+1)n}
\end{align*}
$$
-->

<math xmlns="http://www.w3.org/1998/Math/MathML" display="block">
  <mtable columnalign="right left right left right left right left right left right left" rowspacing="3pt" columnspacing="0.278em 2em 0.278em 2em 0.278em 2em 0.278em 2em 0.278em 2em 0.278em">
    <mtr>
      <mtd>
        <msub>
          <mrow class="MJX-TeXAtom-ORD">
            <mover>
              <mrow class="MJX-TeXAtom-ORD">
                <mi mathvariant="bold-italic">&#x03B1;<!-- α --></mi>
              </mrow>
              <mo stretchy="false">&#x007E;<!-- ~ --></mo>
            </mover>
          </mrow>
          <mi>k</mi>
        </msub>
        <mo>=</mo>
        <mfenced open="[" close="]">
          <mtable rowspacing="4pt" columnspacing="1em">
            <mtr>
              <mtd>
                <msub>
                  <mi>&#x03B1;<!-- α --></mi>
                  <mrow class="MJX-TeXAtom-ORD">
                    <mi>k</mi>
                    <mo>,</mo>
                    <mn>1</mn>
                  </mrow>
                </msub>
              </mtd>
            </mtr>
            <mtr>
              <mtd>
                <mo>&#x22EE;<!-- ⋮ --></mo>
              </mtd>
            </mtr>
            <mtr>
              <mtd>
                <msub>
                  <mi>&#x03B1;<!-- α --></mi>
                  <mrow class="MJX-TeXAtom-ORD">
                    <mi>k</mi>
                    <mo>,</mo>
                    <mi>n</mi>
                    <mo>+</mo>
                    <mn>1</mn>
                  </mrow>
                </msub>
              </mtd>
            </mtr>
          </mtable>
        </mfenced>
        <mo>&#x2208;<!-- ∈ --></mo>
        <msup>
          <mrow class="MJX-TeXAtom-ORD">
            <mi mathvariant="double-struck">R</mi>
          </mrow>
          <mrow class="MJX-TeXAtom-ORD">
            <mi>n</mi>
            <mo>+</mo>
            <mn>1</mn>
          </mrow>
        </msup>
        <mo>,</mo>
        <msub>
          <mrow class="MJX-TeXAtom-ORD">
            <mover>
              <mi mathvariant="bold-italic">x</mi>
              <mo stretchy="false">&#x007E;<!-- ~ --></mo>
            </mover>
          </mrow>
          <mi>k</mi>
        </msub>
        <mo>=</mo>
        <mfenced open="[" close="]">
          <mtable rowspacing="4pt" columnspacing="1em">
            <mtr>
              <mtd>
                <msub>
                  <mi mathvariant="bold-italic">x</mi>
                  <mrow class="MJX-TeXAtom-ORD">
                    <mi>k</mi>
                    <mo>,</mo>
                    <mn>1</mn>
                  </mrow>
                </msub>
              </mtd>
            </mtr>
            <mtr>
              <mtd>
                <mo>&#x22EE;<!-- ⋮ --></mo>
              </mtd>
            </mtr>
            <mtr>
              <mtd>
                <msub>
                  <mi mathvariant="bold-italic">x</mi>
                  <mrow class="MJX-TeXAtom-ORD">
                    <mi>k</mi>
                    <mo>,</mo>
                    <mi>n</mi>
                    <mo>+</mo>
                    <mn>1</mn>
                  </mrow>
                </msub>
              </mtd>
            </mtr>
          </mtable>
        </mfenced>
        <mo>&#x2208;<!-- ∈ --></mo>
        <msup>
          <mrow class="MJX-TeXAtom-ORD">
            <mi mathvariant="double-struck">R</mi>
          </mrow>
          <mrow class="MJX-TeXAtom-ORD">
            <mo stretchy="false">(</mo>
            <mi>n</mi>
            <mo>+</mo>
            <mn>1</mn>
            <mo stretchy="false">)</mo>
            <mi>n</mi>
          </mrow>
        </msup>
      </mtd>
    </mtr>
  </mtable>
</math>

由于序列<!--$$\{\tilde{{\boldsymbol{\alpha}}}_k^\top, \tilde{\boldsymbol{x}}_k^\top\}$$--><math xmlns="http://www.w3.org/1998/Math/MathML" display="block"><mo fence="false" stretchy="false">{</mo><msubsup><mrow class="MJX-TeXAtom-ORD"><mover><mrow class="MJX-TeXAtom-ORD"><mi mathvariant="bold-italic">&#x03B1;<!-- α --></mi></mrow><mo stretchy="false">&#x007E;<!-- ~ --></mo></mover></mrow><mi>k</mi><mi mathvariant="normal">&#x22A4;<!-- ⊤ --></mi></msubsup><mo>,</mo><msubsup><mrow class="MJX-TeXAtom-ORD"><mover><mi mathvariant="bold-italic">x</mi><mo stretchy="false">&#x007E;<!-- ~ --></mo></mover></mrow><mi>k</mi><mi mathvariant="normal">&#x22A4;<!-- ⊤ --></mi></msubsup><mo fence="false" stretchy="false">}</mo></math>有界，故必存在极限，设为<!--$$(\tilde{{\boldsymbol{\alpha}}}_\infty^\top, \tilde{\boldsymbol{x}}_\infty^\top)$$--><math xmlns="http://www.w3.org/1998/Math/MathML" display="block"><mo stretchy="false">(</mo><msubsup><mrow class="MJX-TeXAtom-ORD"><mover><mrow class="MJX-TeXAtom-ORD"><mi mathvariant="bold-italic">&#x03B1;<!-- α --></mi></mrow><mo stretchy="false">&#x007E;<!-- ~ --></mo></mover></mrow><mi mathvariant="normal">&#x221E;<!-- ∞ --></mi><mi mathvariant="normal">&#x22A4;<!-- ⊤ --></mi></msubsup><mo>,</mo><msubsup><mrow class="MJX-TeXAtom-ORD"><mover><mi mathvariant="bold-italic">x</mi><mo stretchy="false">&#x007E;<!-- ~ --></mo></mover></mrow><mi mathvariant="normal">&#x221E;<!-- ∞ --></mi><mi mathvariant="normal">&#x22A4;<!-- ⊤ --></mi></msubsup><mo stretchy="false">)</mo></math>，其中 

<!--
$$
\begin{align*}
\tilde{{\boldsymbol{\alpha}}}_\infty = \begin{bmatrix} \alpha_{\infty,1} \\
\vdots \\
\alpha_{\infty,n+1} \end{bmatrix} \in \mathbb{R}^{n+1},
\tilde{\boldsymbol{x}}_\infty = \begin{bmatrix} \boldsymbol{x}_{\infty,1} \\
\vdots \\
\boldsymbol{x}_{\infty,n+1} \end{bmatrix} \in \mathbb{R}^{(n+1)n}
\end{align*}
$$
-->

<math xmlns="http://www.w3.org/1998/Math/MathML" display="block">
  <mtable columnalign="right left right left right left right left right left right left" rowspacing="3pt" columnspacing="0.278em 2em 0.278em 2em 0.278em 2em 0.278em 2em 0.278em 2em 0.278em">
    <mtr>
      <mtd>
        <msub>
          <mrow class="MJX-TeXAtom-ORD">
            <mover>
              <mrow class="MJX-TeXAtom-ORD">
                <mi mathvariant="bold-italic">&#x03B1;<!-- α --></mi>
              </mrow>
              <mo stretchy="false">&#x007E;<!-- ~ --></mo>
            </mover>
          </mrow>
          <mi mathvariant="normal">&#x221E;<!-- ∞ --></mi>
        </msub>
        <mo>=</mo>
        <mfenced open="[" close="]">
          <mtable rowspacing="4pt" columnspacing="1em">
            <mtr>
              <mtd>
                <msub>
                  <mi>&#x03B1;<!-- α --></mi>
                  <mrow class="MJX-TeXAtom-ORD">
                    <mi mathvariant="normal">&#x221E;<!-- ∞ --></mi>
                    <mo>,</mo>
                    <mn>1</mn>
                  </mrow>
                </msub>
              </mtd>
            </mtr>
            <mtr>
              <mtd>
                <mo>&#x22EE;<!-- ⋮ --></mo>
              </mtd>
            </mtr>
            <mtr>
              <mtd>
                <msub>
                  <mi>&#x03B1;<!-- α --></mi>
                  <mrow class="MJX-TeXAtom-ORD">
                    <mi mathvariant="normal">&#x221E;<!-- ∞ --></mi>
                    <mo>,</mo>
                    <mi>n</mi>
                    <mo>+</mo>
                    <mn>1</mn>
                  </mrow>
                </msub>
              </mtd>
            </mtr>
          </mtable>
        </mfenced>
        <mo>&#x2208;<!-- ∈ --></mo>
        <msup>
          <mrow class="MJX-TeXAtom-ORD">
            <mi mathvariant="double-struck">R</mi>
          </mrow>
          <mrow class="MJX-TeXAtom-ORD">
            <mi>n</mi>
            <mo>+</mo>
            <mn>1</mn>
          </mrow>
        </msup>
        <mo>,</mo>
        <msub>
          <mrow class="MJX-TeXAtom-ORD">
            <mover>
              <mi mathvariant="bold-italic">x</mi>
              <mo stretchy="false">&#x007E;<!-- ~ --></mo>
            </mover>
          </mrow>
          <mi mathvariant="normal">&#x221E;<!-- ∞ --></mi>
        </msub>
        <mo>=</mo>
        <mfenced open="[" close="]">
          <mtable rowspacing="4pt" columnspacing="1em">
            <mtr>
              <mtd>
                <msub>
                  <mi mathvariant="bold-italic">x</mi>
                  <mrow class="MJX-TeXAtom-ORD">
                    <mi mathvariant="normal">&#x221E;<!-- ∞ --></mi>
                    <mo>,</mo>
                    <mn>1</mn>
                  </mrow>
                </msub>
              </mtd>
            </mtr>
            <mtr>
              <mtd>
                <mo>&#x22EE;<!-- ⋮ --></mo>
              </mtd>
            </mtr>
            <mtr>
              <mtd>
                <msub>
                  <mi mathvariant="bold-italic">x</mi>
                  <mrow class="MJX-TeXAtom-ORD">
                    <mi mathvariant="normal">&#x221E;<!-- ∞ --></mi>
                    <mo>,</mo>
                    <mi>n</mi>
                    <mo>+</mo>
                    <mn>1</mn>
                  </mrow>
                </msub>
              </mtd>
            </mtr>
          </mtable>
        </mfenced>
        <mo>&#x2208;<!-- ∈ --></mo>
        <msup>
          <mrow class="MJX-TeXAtom-ORD">
            <mi mathvariant="double-struck">R</mi>
          </mrow>
          <mrow class="MJX-TeXAtom-ORD">
            <mo stretchy="false">(</mo>
            <mi>n</mi>
            <mo>+</mo>
            <mn>1</mn>
            <mo stretchy="false">)</mo>
            <mi>n</mi>
          </mrow>
        </msup>
      </mtd>
    </mtr>
  </mtable>
</math>

显然有$$\sum_{i=1}^{n+1} \alpha_{\infty,i} = 1, \alpha_{\infty,i} \geq 0, i = 1, \dots, n + 1$$，由于$$X$$是闭集，故$$\boldsymbol{x}_{\infty, i} \in X, i = 1, \dots, n + 1$$，再由序列极限$$\bar{\boldsymbol{x}}$$可表示为$$\bar{\boldsymbol{x}} = \alpha_{\infty,1} \boldsymbol{x}_{\infty,1} + \dots + \alpha_{\infty,n+1} \boldsymbol{x}_{\infty,n+1}$$可知$$\bar{\boldsymbol{x}} \in conv(X)$$.

$X$有界的假设是不可或缺的，否则序列<!--${\tilde{{\boldsymbol{\alpha}}}_k^\top, \tilde{\boldsymbol{x}}_k^\top}$--><math xmlns="http://www.w3.org/1998/Math/MathML"><mrow class="MJX-TeXAtom-ORD"><msubsup><mrow class="MJX-TeXAtom-ORD"><mover><mrow class="MJX-TeXAtom-ORD"><mi mathvariant="bold-italic">&#x03B1;<!-- α --></mi></mrow><mo stretchy="false">&#x007E;<!-- ~ --></mo></mover></mrow><mi>k</mi><mi mathvariant="normal">&#x22A4;<!-- ⊤ --></mi></msubsup><mo>,</mo><msubsup><mrow class="MJX-TeXAtom-ORD"><mover><mi mathvariant="bold-italic">x</mi><mo stretchy="false">&#x007E;<!-- ~ --></mo></mover></mrow><mi>k</mi><mi mathvariant="normal">&#x22A4;<!-- ⊤ --></mi></msubsup></mrow></math>的极限不一定存在.一个反例，设 

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



[C1S2-pic1]: {{"/assets/images/C1S2-pic1.png" |site.baseurl }}
[C1S2-pic2]: {{"/assets/images/C1S2-pic2.png" | site.baseurl }}

