---
layout: post
title:  "变分法简介"
date:   2017-04-29 16:35:00 +0800
tags: [Mathematics]
---

这是一篇转载的博文，原地址为：<del>[变分法简介](http://www.cnblogs.com/murongxixi/p/3995788.html)</del>

原博客无法进入，备用链接：[变分法简介 - 慕容熙熙](https://www.tuicool.com/articles/E3eaqm)

## 泛函的基本概念

变分法的诞生要追溯到Johann Bernoulli(1667－1748)于1696年提出的“最速降线问题”，这个问题是一个求极值问题，但和普通的函数求极值又有不同，它的目标函数的自变量不是一个数，而是一个函数.由于问题很新颖，很快就引起了一些大家的兴趣，其中Johann的哥哥Jacob Bernoulli(1654-1705)给出了较为一般化的解法，后来Euler(1707～1783)和Lagrange(1736-1813)在此基础上得到了Euler-Lagrange方程，从而给出了这一类问题的通用解法.

变分法要处理的是函数到实数的映射，这样的映射被称作泛函，由于我们不是要写教科书，所以这里也就不给出精确定义了，就通过下面这个例子来简单说明下.

设函数$y = f(x) \geq 0$在$[0,1]$上连续，则

$$
\begin{align*}
Q[f(x)] = \int_0^1 f(x) \mathrm{d} x
\end{align*}
$$

就是一个泛函，它的输入是$[0,1]$上的非负连续函数，输出是$[0,1]$区间上该函数与x轴之间围成的面积.

显然泛函是函数这一概念的推广，唯一的区别就是**自变量不同**，那么为了求泛函极值，最直接的想法就是套用函数求极值的方法.不过在深入之前，我们需要先简单介绍些泛函的基本概念，包括**连续泛函**、**线性泛函**、**泛函极值**和**泛函变分**，它们分别对应于连续函数、线性函数、函数极值和函数微分.

+ 连续泛函：对于泛函$Q[y(x)]$，如果当$y(x)$的变化$\delta y(x)$充分小时，$Q$的改变量也可以任意的小，那么就称泛函$Q[y(x)]$是连续的.

例如对于泛函

$$
\begin{align*}
Q[y(x)]
= \int_a^b y(x) \mathrm{d} x
\end{align*}
$$

而言，当$y(x) \in C[a,b]$时，$Q[y(x)]$有定义.则对于任意$\epsilon>0$，只要

$$
\begin{align*}
\max_{a \leq x \leq b} |y_1(x) - y(x)|
< \frac{\epsilon}{b-a}
\end{align*}
$$

则有

$$
\begin{align*} 
\left| Q[y_1(x)] - Q[y(x)] \right|
& = \left| \int_a^b \left(y_1(x) - y(x)\right) \mathrm{d} x \right| \\
& \leq \int_a^b |y_1(x) - y(x)| \mathrm{d} x \\
& < \int_a^b \frac{\epsilon}{b-a} \mathrm{d} x \\
& = \epsilon
\end{align*}
$$

即$Q[y(x)]$是连续泛函.

+ 泛函极值：对于曲线$y(x)$，满足

$$
\begin{align*}
\max_x \left|y_1(x) - y(x)\right|
\leq \varepsilon
\end{align*}
$$

的一切连续曲线$y_1(x)$构成的集合就是$y(x)$的$\epsilon$-邻域，若对于邻域中的任意曲线$y_1(x)$都有

$$
\begin{align*}
Q[y_1(x)] \leq Q[y(x)]
\end{align*}
$$

则称泛函Q[y(x)]在y(x)的某个ε-邻域内取极值.

+ 线性泛函：若对于任意常数$c_1$和$c_2$，$Q[f(x)]$满足

$$
\begin{align*}
Q[c_1 y_1(x) + c_2 y_2(x)]
= c_1 Q[y_1(x)] + c_2 Q[y_2(x)]
\end{align*}
$$

则称$Q[y(x)]$是线性泛函

+ 泛函变分：先来看一个例子，设泛函$Q[y(x)]=\int_a^b y^2(x)\mathrm{d} x$，函数$y_1(x)=y(x) + \delta y(x)$是对$y(x)$的一个扰动，则$Q[y(x)]$的增量为

$$
\begin{align*} 
\Delta Q
& = Q[y_1(x)]-Q[y(x)] \\
& = Q[y(x)+\delta y(x)]-Q[y(x)] \\
& = \int_a^b (y(x) + \delta y(x))^2 \mathrm{d} x - \int_a^b y^2(x) \mathrm{d} x \\
& = \int_a^b 2y(x)\cdot\delta y(x) \mathrm{d} x + \int_a^b(\delta y(x))^2 \mathrm{d} x
\end{align*}
$$

可见$\Delta Q$由两部分构成，将第一项记为

$$
\begin{align*}
T[y(x),\delta y(x)]
= \int_a^b 2y(x) \delta y(x) \mathrm{d} x
\end{align*}
$$

故对第二项有

$$
\begin{align*} 
\lim_{\max_{a \leq x \leq b} |\delta y(x)| \rightarrow 0} \frac{\int_a^b (\delta y(x))^2 \mathrm{d} x}{\max_{a \leq x \leq b} |\delta y(x)|}
&\leq \lim_{\max_{a \leq x \leq b} |\delta y(x)| \rightarrow 0} \frac{\left( \max_{a \leq x \leq b} |\delta y(x)| \right)^2 (b-a)}{\max_{a \leq x \leq b} |\delta y(x)|} \\
&= \lim_{\max_{a \leq x \leq b} |\delta y(x)| \rightarrow 0} (\max_{a \leq x \leq b} |\delta y(x)| ) (b-a) \\
&= \lim_{t \rightarrow 0} t (b-a)，\left( 其中 t = \max_{a \leq x \leq b} |\delta y(x)| \right) \\
&= 0
\end{align*}
$$

即$\int_a^b (\delta y(x))^2 \mathrm{d} x$是关于$\delta y(x)$的高阶无穷小，记为$o(\delta y(x))$，于是

$$
\begin{align*}
\Delta Q
= T[y(x),\delta y(x)]+o(\delta y(x))
\end{align*}
$$

对比函数微分的概念，可以发现它们是何其地相似.故类似地，我们可以说，若对自变量$y(x)$作微小增量$\delta y(x)$，其相应的泛函的增量$\Delta Q$可以分为两部分，其中第一部分$T[y(x),\delta y(x)]$是关于$\delta y(x)$的线性泛函，第二部分是关于$\delta y(x)$的高阶无穷小，那么就将$T[y(x),\delta y(x)]$称作泛函$Q[y(x)]$的变分.

## 预备定理

在推导Euler-Lagrange方程前，我们需要如下的预备定理.

若函数$y=f(x)$在$[a,b]$上连续且$\int_a^b f(x)\eta(x) = 0$，其中$\eta(x)$在$[a,b]$上有连续导数，$\eta(a) = \eta(b)=0$且
$\left| \eta(x) \right| < \epsilon$
（$\epsilon \in \mathbb{R^+}$），那么函数$f(x)$在$[a,b]$上恒等于$0$.

证明：用反证法，假设存在$x_0 \in (a,b)$使得$f(x_0)>0$，由$f(x)$的连续性知存在正数$\delta$使得当
$\left| x-x_0 \right| < \delta$
时有$f(x)>0$. 现作函数

$$
\begin{align*} 
\psi(x) =
\begin{cases}
 0 & x \in [a, x_0 - \delta] \\
 e^{\frac{1}{(x - x_0)^2 - \delta^2}} & x \in (x_0 - \delta, x_0 + \delta) \\
 0 & x \in [x_0 + \delta, b] 
\end{cases}
\end{align*}
$$

显然$\psi(a) = \psi(b) = 0$，此外$\psi(x)$在$[a,b]$上有连续导数(这里先做假设，稍后给出证明)，又选取合适的$A$可使得$\eta(x) = A \psi(x)$满足
$\left| \eta(x) \right| < \epsilon$
，故这样的$\eta(x)$满足所有条件，于是

$$
\begin{align*}
\int_a^b f(x) \eta(x) \mathrm{d} x 
= \int_{x_0 - \delta}^{x_0 + \delta} f(x) \eta(x) \mathrm{d} x > 0
\end{align*}
$$

得出矛盾，故不存在这样的$x_0$，也即$f(x)$在$(a,b)$上不大于$0$，同理可证$f(x)$在$(a,b)$上也不小于$0$，故只可能是$f(x)$在$(a,b)$上恒等于$0$，又由$f(x)$的连续性知$f(a) = f(b) = 0$，故$f(x)$在$[a,b]$上恒为$0$.

最后证明$\psi(x)$在$[a,b]$上有连续导数，只需考虑$x_0 + \delta$和$x_0 - \delta$这两点即可，具体来说分两步，先证明左右导数相等也即导数存在，再证明导数的左右极限也相等即连续性成立.

先考虑右导数，易知

$$
\begin{align*}
\lim_{x \rightarrow (x_0 + \delta)^+} \frac{\psi(x) - \psi(x_0 + \delta)}{x - (x_0 + \delta)} 
= \lim_{x \rightarrow (x_0 + \delta)^+} \frac{0 - 0}{x - (x_0 + \delta)} 
= 0 
\end{align*}
$$

 再考虑左导数，易知

$$
\begin{align*}
\lim_{x \rightarrow (x_0 + \delta)^-} \frac{\psi(x) - \psi(x_0 + \delta)}{x - (x_0 + \delta)} 
& = \lim_{x \rightarrow (x_0 + \delta)^-} \frac{e^{\frac{1}{(x - x_0)^2 - \delta^2}} - 0}{x - (x_0 + \delta)} \\
& = \lim_{t \rightarrow - \infty} \frac{e^t}{\left( \frac{1}{t} + \delta^2 \right)^{\frac{1}{2}} - \delta} \left( 其中 t = \frac{1}{(x - x_0)^2 - \delta^2}\right) \\
& =  \lim_{t \rightarrow - \infty} \frac{e^t}{\frac{1}{2} \left( \frac{1}{t} + \delta^2 \right)^{-\frac{1}{2}} \left(-\frac{1}{t^2}\right)} \\
& = \lim_{t \rightarrow - \infty} (-2) e^t t^2 \left( \frac{1}{t} + \delta^2 \right)^{\frac{1}{2}} 
\end{align*}
$$

其中倒数第二个等号由L'Hospital法则推出.注意

$$
\begin{align*} 
\lim_{t \rightarrow - \infty} \left( \frac{1}{t} + \delta^2 \right)^{\frac{1}{2}} 
= \delta
\end{align*}
$$

且

$$
\begin{align*}
\lim_{t \rightarrow - \infty} e^t t^2 
= \lim_{t \rightarrow \infty} \frac{t^2}{e^t} 
= \lim_{t \rightarrow \infty} \frac{2t}{e^t} 
= \lim_{t \rightarrow \infty} \frac{2}{e^t} 
= 0 
\end{align*}
$$

故左导数也为$0$，由于左右导数相等，因此$\psi(x)$在$x_0 + \delta$导数为$0$.

下面再证导数的连续性，先考虑右极限，由于当$x > x_0 + \delta$时$\psi(x) \equiv 0$，所以当$x > x_0 + \delta$时$\psi'(x) \equiv 0$，于是$\lim_{x \rightarrow (x_0 + \delta)^+} \psi'(x) = 0$.

再考虑左极限，当$x < x_0 + \delta$时有

$$
\begin{align*}
\psi'(x)
= e^{\frac{1}{(x - x_0)^2 - \delta^2}} \frac{-2(x - x_0)}{((x - x_0)^2 - \delta^2)^2}
\end{align*}
$$

于是

$$
\begin{align*}
\lim_{x \rightarrow (x_0 + \delta)^-} \psi'(x) 
& = \lim_{x \rightarrow (x_0 + \delta)^-} e^{\frac{1}{(x - x_0)^2 - \delta^2}} \frac{-2(x - x_0)}{((x - x_0)^2 - \delta^2)^2} \\
& = \lim_{t \rightarrow -\infty} (-2) e^t t^2 \left( \frac{1}{t} + \delta^2 \right)^{\frac{1}{2}} \left( 其中 t = \frac{1}{(x - x_0)^2 - \delta^2}\right) \\
& = 0 
\end{align*}
$$

故左右极限也相等，因此$\psi'(x)$在$x_0 + \delta$处连续，综上$\psi(x)$在$x_0 + \delta$处有连续导数，同理也可证$\psi(x)$ 在$x_0 - \delta$处有连续导数.

## Euler-Lagrange方程（ E-L equation）的推导
现在我们转入正题，考虑如下形式的泛函

$$
\begin{align*}
Q[y(x)]
= \int_a^b F(x, y(x), y'(x)) \mathrm{d} x
\end{align*}
$$

其中$F(x, y(x), y'(x))$是三个变量的连续函数且当点$x,y$在平面上某个有界域内，$F(x, y(x), y'(x))$及其直到二阶的偏导数均连续.

求泛函极值的基本思想还是套用微积分里的Fermat定理，现假设$Q[f(x)]$在$y(x)$处取得极值，任取一个函数$\eta(x)$满足$\eta(a) = \eta(b) = 0$且有连续导数，考虑$y(x)$某个领域内的函数$y_1(x) = y(x) + \alpha \eta(x)$，那么当$\alpha$充分小，应该有$Q[y_1(x)] \leq Q[y(x)]$.由于泛函$Q[y(x) + \alpha \eta(x)] = \psi(\alpha)$也是$\alpha$的函数，于是由Fermat定理知应该有$\psi'(0) = 0$.

又有

$$\begin{align} 
\psi'(0)
= \psi'(\alpha) |_{\alpha = 0} 
& =  \left. \frac{\mathrm{d}}{\mathrm{d} \alpha} \left( \int_a^b F(x, y(x) + \alpha \eta(x), y'(x) + \alpha \eta'(x)) \mathrm{d} x \right) \right|_{\alpha = 0} \nonumber \\ \label{Euler-Lagrange} 
& = \left. \left( \int_a^b \frac{\mathrm{d} F(x, y(x) + \alpha \eta(x), y'(x) + \alpha \eta'(x))}{\mathrm{d} \alpha} \mathrm{d} x \right) \right|_{\alpha = 0} \\ 
& = \left. \left( \int_a^b F_y \frac{\mathrm{d} (y(x) + \alpha \eta(x))}{\mathrm{d} \alpha} + F_{y'} \frac{\mathrm{d} (y'(x) + \alpha \eta'(x))}{\mathrm{d} \alpha} \mathrm{d} x \right) \right|_{\alpha = 0} \nonumber \\ 
& = \left. \left( \int_a^b F_y \eta(x) + F_{y'} \eta'(x) \mathrm{d} x \right) \right|_{\alpha = 0} \nonumber \\ 
& = \int_a^b F_y \eta(x) \mathrm{d} x + \int_a^b F_{y'} \eta'(x) \mathrm{d} x \nonumber \\ 
& = \int_a^b F_y \eta(x) \mathrm{d} x + \left. F_{y'} \eta(x) \right|_a^b - \int_a^b  \eta(x) \mathrm{d} F_{y'}  \left( 其中 \eta(a) = \eta(b) = 0 \right) \nonumber \\
& = \int_a^b \left( F_y - \frac{\mathrm{d} F_{y'}}{\mathrm{d} x} \right) \eta(x) \mathrm{d} x \nonumber
\end{align}
$$

其中($\ref{Euler-Lagrange}$)式交换了积分和求导的顺序(正确性稍后给出证明).于是

$$
\begin{align*}
\int_a^b \left( F_y - \frac{\mathrm{d} F_{y'}}{\mathrm{d} x} \right) \eta(x) \mathrm{d} x
= 0
\end{align*}
$$

由预备定理知

$$
\begin{align*}
F_y
= \frac{\mathrm{d} F_{y'}}{\mathrm{d} x}
\end{align*}
$$

这就是Euler-Lagrange方程.


($\ref{Euler-Lagrange}$)式中第三个等号可以交换积分和求导的顺序是因为

$$
\begin{align*}
\frac{\psi(\alpha + \Delta \alpha) - \psi(\alpha)}{\Delta \alpha}
& = \frac{Q[y(x) + (\alpha + \Delta \alpha) \eta(x)] - Q[y(x) + \alpha \eta(x)]}{\Delta \alpha} \\
& = \int_a^b \frac{F(x, y(x) + (\alpha + \Delta \alpha) \eta(x), y'(x) + (\alpha + \Delta \alpha) \eta'(x)) - F(x, y(x) + \alpha \eta(x), y'(x) + \alpha \eta'(x))}{\Delta \alpha} \mathrm{d} x \\
& = \int_a^b F_{\alpha}(x, y(x) + (\alpha + \theta \Delta \alpha) \eta(x), y'(x) + (\alpha + \theta \Delta \alpha) \eta'(x)) \mathrm{d} x  (\theta \in (0, 1))
\end{align*}
$$

其中最后一个等号是因为Lagrange中值定理(所以$F$的连续性和可导性是必须的，否则无法使用中值定理).于是由$F$各个偏导数的连续性可知对于$\forall \epsilon > 0$，总可以找到充分小的$\Delta \alpha$使得

$$
\begin{align*}
\left|F_{\alpha}(x, y(x) + (\alpha + \theta \Delta \alpha) \eta(x), y'(x) + (\alpha + \theta \Delta \alpha) \eta'(x)) - F_{\alpha}(x, y(x) + \alpha \eta(x), y'(x) + \alpha \eta'(x)) \right|
< \epsilon
\end{align*}
$$

因此

$$
\begin{align*}
& \left| \frac{\psi(\alpha + \Delta \alpha) - \psi(\alpha)}{\Delta \alpha} - \int_a^b F_{\alpha}(x, y(x) + \alpha \eta(x), y'(x) + \alpha \eta'(x)) \mathrm{d} x \right| \\ 
& \leq \int_a^b |F_{\alpha}(x, y(x) + (\alpha + \theta \Delta \alpha) \eta(x), y'(x) + (\alpha + \theta \Delta \alpha) \eta'(x)) - F_{\alpha}(x, y(x) + \alpha \eta(x), y'(x) + \alpha \eta'(x))| \mathrm{d} x \\ 
& < \epsilon (b - a)
\end{align*}
$$

当$\epsilon \rightarrow 0$有$\Delta \alpha \rightarrow 0$，于是

$$
\begin{align*}
\frac{\mathrm{d}}{\mathrm{d} \alpha} \left( \int_a^b F(x, y(x) + \alpha \eta(x), y'(x) + \alpha \eta'(x)) \mathrm{d} x \right)
= \int_a^b \frac{\mathrm{d} F(x, y(x) + \alpha \eta(x), y'(x) + \alpha \eta'(x))}{\mathrm{d} \alpha} \mathrm{d} x
\end{align*}
$$

## 具体应用

下面有三个具体的应用

+ 求连接$(0,0)$和$(1,1)$的所有曲线中长度最短的曲线，借助几何知识可知应该是直线的长度最短，下面我们用变分法来求解，也即求泛函

$$
\begin{align*}
\int_0^1 \sqrt{1 + y'^2} \mathrm{d} x 
\end{align*}
$$

的极值，记$F(x, y(x), y'(x)) = \sqrt{1 + y'^2}$，于是

$$
\begin{align*}
F_y & = 0 \\ F_{y'}
& = \frac{y'}{\sqrt{1 + y'^2}}
\end{align*}
$$

由Euler-Lagrange方程知

$$
\begin{align*}
\frac{\mathrm{d}}{\mathrm{d} x} \left( \frac{y'}{\sqrt{1 + y'^2}} \right)
= 0 
\end{align*}
$$

故

$$
\begin{align*}
\frac{y'}{\sqrt{1 + y'^2}}
= C
\end{align*}
$$

其中$C$为某一常数，整理得

$$
\begin{align*}
y'
= \pm \frac{c}{\sqrt{1-c^2}}
\end{align*}
$$

故最优曲线的斜率为常数，也即直线，由边界条件可知是$y = x$.

+ 回归问题的目标函数可以写成

$$
\begin{align*}
\min_y  \mathbb{E}[L] 
= \int_{\boldsymbol{x}} \int_t L(t, y(\boldsymbol{x})) p(\boldsymbol{x},t) \mathrm{d} t \mathrm{d} \boldsymbol{x}
\end{align*}
$$

其中$y$是待求的对观测数据的拟合函数，$t$是样本$\boldsymbol{x}$的观测值，$L$是损失函数，目标则是找到最优的$y$使得期望损失最小.特别地，若取损失函数为平方损失，即$L = (y(\boldsymbol{x}) - t)^2$，则记

$$
\begin{align*}
F(x, y(x), y'(x))
= \int_t (y(\boldsymbol{x}) - t)^2 p(\boldsymbol{x},t) \mathrm{d} t
\end{align*}
$$

于是

$$
\begin{align*}
F_y & = \int_t 2 (y(\boldsymbol{x}) - t) p(\boldsymbol{x},t) \mathrm{d} t \\
F_{y'} & = 0
\end{align*}
$$

由Euler-Lagrange方程知

$$
\begin{align*}
\int_t t p(\boldsymbol{x},t) \mathrm{d} t
& = \int_t y(\boldsymbol{x}) p(\boldsymbol{x},t) \mathrm{d} t \\
& = y(\boldsymbol{x}) p(\boldsymbol{x})
\end{align*}
$$

故

$$\begin{align*}
y(\boldsymbol{x})
& = \frac{\int_t t p(\boldsymbol{x},t) \mathrm{d} t}{p(\boldsymbol{x})} \\
& = \int_t t p(t | \boldsymbol{x}) \mathrm{d} \\
& = \mathbb{E}[t|\boldsymbol{x}]
\end{align*}
$$

也即对于最小二乘回归，其最优拟合函数是给定输入的条件期望.

+ 对于任意满足如下限制条件
 
$$
\begin{align}
\label{Gauss 1} \int_{-\infty}^\infty p(x) \mathrm{d} x 
& = 1 \\
\label{Gauss 2} \int_{-\infty}^\infty x p(x) \mathrm{d} x 
& = \mu \\ \label{Gauss 3} \int_{-\infty}^\infty (x - \mu)^2 p(x) \mathrm{d} x 
& = \sigma^2
\end{align}
$$

的概率分布，其中使得熵最大的是正态分布. 
由于是约束优化问题，引入Lagrange乘子$\lambda_1$，$\lambda_2$和$\lambda_3$，目标函数可写为

$$
\begin{align*}
\min_{p(x)} \int_{-\infty}^\infty p(x) \ln p(x) \mathrm{d} x
- \lambda_1 \left( \int_{-\infty}^\infty p(x) \mathrm{d} x - 1 \right)
- \lambda_2 \left( \int_{-\infty}^\infty x p(x) \mathrm{d} x - \mu \right) 
- \lambda_3 \left( \int_{-\infty}^\infty (x - \mu)^2 p(x) \mathrm{d} x - \sigma^2 \right)
\end{align*}
$$

将关于$p(x)$的项单独提出来记为$F(x, p(x), p'(x))$，则

$$\begin{align*} F(x, p(x), p'(x)) = p(x) \ln p(x) - \lambda_1 p(x) - \lambda_2 x p(x) - \lambda_3 (x - \mu)^2 p(x) \end{align*}$$

于是

$$\begin{align*} F_p & = \ln p(x) + 1 - \lambda_1 - \lambda_2 x - \lambda_3 (x - \mu)^2 \\ F_{p'} & = 0 \end{align*}$$

由Euler-Lagrange方程知

$$\begin{align} \label{Gauss 4} p(x) = \mathrm{exp} (- 1 + \lambda_1 + \lambda_2 x + \lambda_3 (x - \mu)^2) \end{align}$$

将($\ref{Gauss 4}$)回代入($\ref{Gauss 1}$)、($\ref{Gauss 2}$)、($\ref{Gauss 3}$)并令$y = x - \mu$可得

$$\begin{align} \label{Gauss 5} \int_{-\infty}^\infty \mathrm{exp} (- 1 + \lambda_1 + \lambda_2 (y + \mu) + \lambda_3 y^2) \mathrm{d}y & = 1 \\ \label{Gauss 6} \int_{-\infty}^\infty (y + \mu) \mathrm{exp} (- 1 + \lambda_1 + \lambda_2 (y + \mu) + \lambda_3 y^2) \mathrm{d}y & = \mu \\ \label{Gauss 7} \int_{-\infty}^\infty y^2 \mathrm{exp} (- 1 + \lambda_1 + \lambda_2 (y + \mu) + \lambda_3 y^2) \mathrm{d}y & = \sigma^2 \end{align}$$

($\ref{Gauss 6}$) - $\mu$($\ref{Gauss 5}$)可得

$$
\begin{align}
\int_{-\infty}^\infty y \cdot \mathrm{exp} ( -1 + \lambda_1 + \lambda_2 \mu + \lambda_2 y + \lambda_3 y^2) \mathrm{d}y 
= 0
\end{align}
$$

将其中的非零常数项$\mathrm{exp} (- 1 + \lambda_1 + \lambda_2 \mu)$丢掉，然后$2 \lambda_3$($\ref{Gauss 7}$)$+ \lambda_2$($\ref{Gauss 5}$)可得

$$
\begin{align*}
\lambda_2 
& = \int_{-\infty}^\infty (\lambda_2 + 2 \lambda_3 y) \mathrm{exp} (\lambda_2 y + \lambda_3 y^2) \mathrm{d}y \\
& = \lim_{y \rightarrow \infty} \mathrm{exp} (\lambda_2 y + \lambda_3 y^2) - \lim_{y \rightarrow -\infty} \mathrm{exp} (\lambda_2 y + \lambda_3 y^2)
\end{align*}
$$

注意$\lambda_2$和$\lambda_3$都是有限常数，因此随着$y$趋向无穷，$\lambda_2 y + \lambda_3 y^2$要么趋向$\infty$，要么趋向$-\infty$，又

$$
\begin{align*}
\lim_{x \rightarrow \infty} \mathrm{exp} (x) & = \infty, \\
lim_{x \rightarrow -\infty} \mathrm{exp} (x) &= 0 
\end{align*}
$$

因此只可能是$\lambda_2 = 0$且

$$
\begin{align*}
\lim_{y \rightarrow \infty} \lambda_2 y + \lambda_3 y^2 & = -\infty, \\
\lim_{y \rightarrow -\infty} \lambda_2 y + \lambda_3 y^2 & = -\infty
\end{align*}
$$

故$\lambda_3 < 0$.此时，由($\ref{Gauss 5}$)可知

$$
\begin{align*}
1
& = \int_{-\infty}^\infty \mathrm{exp} (- 1 + \lambda_1 + \lambda_3 y^2) \mathrm{d}y \\
& = \mathrm{exp} (- 1 + \lambda_1) \int_{-\infty}^\infty \mathrm{exp} \left( -\frac{(\sqrt{-2 \lambda_3} y)^2}{2} \right) \mathrm{d}y \\
& = \mathrm{exp} (- 1 + \lambda_1) \frac{1}{\sqrt{-2 \lambda_3}} \int_{-\infty}^\infty \mathrm{exp} \left( -\frac{z^2}{2} \right) \mathrm{d}z \ \left( 其中 z = \sqrt{-2 \lambda_3} y \right) \\
& =  \mathrm{exp} (- 1 + \lambda_1) \frac{\sqrt{2 \pi}}{\sqrt{-2 \lambda_3}}
\end{align*}
$$

于是

$$
\begin{align}
\label{Gauss 8} \mathrm{exp} (- 1 + \lambda_1) 
= \sqrt{-\frac{\lambda_3}{\pi}}
\end{align}
$$

由($\ref{Gauss 7}$)可知

$$\begin{align*}
\sigma^2 
& = \sqrt{-\frac{\lambda_3}{\pi}} \int_{-\infty}^\infty y^2 \mathrm{exp} (\lambda_3 y^2) \mathrm{d}y \\ 
& = 2 \sqrt{-\frac{\lambda_3}{\pi}} \int_0^\infty y^2 \mathrm{exp} (\lambda_3 y^2) \mathrm{d}y \\ 
& = \sqrt{-\frac{\lambda_3}{\pi}} \frac{1}{\lambda_3} \int_0^\infty y (2 \lambda_3 y \mathrm{exp} (\lambda_3 y^2)) \mathrm{d}y \\ 
& = \left. \sqrt{-\frac{\lambda_3}{\pi}} \frac{y \mathrm{exp} (\lambda_3 y^2)}{\lambda_3} \right|_0^\infty - \sqrt{-\frac{\lambda_3}{\pi}} \frac{1}{\lambda_3} \int_0^\infty \mathrm{exp} (\lambda_3 y^2) \mathrm{d}y \\ 
& = - \sqrt{-\frac{\lambda_3}{\pi}} \frac{1}{\lambda_3} \frac{1}{2} \sqrt{-\frac{\pi}{\lambda_3}} \\ 
& = -\frac{1}{2 \lambda_3}
\end{align*}
$$

于是

$$
\begin{align}
\label{Gauss 9} \lambda_3
= - \frac{1}{2 \sigma^2}
\end{align}
$$

将($\ref{Gauss 8}$)和($\ref{Gauss 9}$)代入($\ref{Gauss 4}$)可得

$$
\begin{align*}
p(x)
& = \mathrm{exp} (- 1 + \lambda_1 + \lambda_3 (x - \mu)^2) \\
& = \sqrt{-\frac{\lambda_3}{\pi}} \mathrm{exp} (\lambda_3 (x - \mu)^2) \\
& = \frac{1}{\sqrt{2 \pi \sigma^2}} \mathrm{exp} \left( - \frac{(x - \mu)^2}{2 \sigma^2} \right)
\end{align*}
$$