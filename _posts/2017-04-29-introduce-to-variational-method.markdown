---
layout: post
title:  "变分法简介"
date:   2017-04-29 16:35:00 +0800
tags: [Mathematics]
---

这是一篇转载的博文，原地址为：[变分法简介](http://www.cnblogs.com/murongxixi/p/3995788.html)

## 泛函的基本概念
变分法的诞生要追溯到Johann Bernoulli(1667－1748)于1696年提出的“最速降线问题”，这个问题是一个求极值问题，但和普通的函数求极值又有不同，它的目标函数的自变量不是一个数，而是一个函数.由于问题很新颖，很快就引起了一些大家的兴趣，其中Johann的哥哥Jacob Bernoulli(1654-1705)给出了较为一般化的解法，后来Euler(1707～1783)和Lagrange(1736-1813)在此基础上得到了Euler-Lagrange方程，从而给出了这一类问题的通用解法.

变分法要处理的是函数到实数的映射，这样的映射被称作泛函，由于我们不是要写教科书，所以这里也就不给出精确定义了，就通过下面这个例子来简单说明下.

设函数$$y = f(x) \geq 0$$在$$[0,1]$$上连续，则

$$\begin{align*} Q[f(x)] = \int_0^1 f(x) \mathrm{d}x \end{align*}$$

就是一个泛函，它的输入是$$[0,1]$$上的非负连续函数，输出是$$[0,1]$$区间上该函数与x轴之间围成的面积.

显然泛函是函数这一概念的推广，唯一的区别就是**自变量不同**，那么为了求泛函极值，最直接的想法就是套用函数求极值的方法.不过在深入之前，我们需要先简单介绍些泛函的基本概念，包括**连续泛函**、**线性泛函**、**泛函极值**和**泛函变分**，它们分别对应于连续函数、线性函数、函数极值和函数微分.

+ 连续泛函：对于泛函$$Q[y(x)]$$，如果当$$y(x)$$的变化$$\delta y(x)$$充分小时，$$Q$$的改变量也可以任意的小，那么就称泛函$$Q[y(x)]$$是连续的.例如对于泛函
$$Q[y(x)]=\int_a^b y(x)\mathrm{d}x$$
而言，当$$y(x) \in C[a,b]$$时，$$Q[y(x)]$$有定义.则对于任意$$\epsilon>0$$，只要
$$\begin{align*} \max_{a \leq x \leq b} |y_1(x) - y(x)| < \frac{\epsilon}{b-a} \end{align*}$$

则有

$$\begin{align*} \left| Q[y_1(x)] - Q[y(x)] \right| = \left| \int_a^b \left(y_1(x) - y(x)\right) \mathrm{d}x \right| \leq \int_a^b |y_1(x) - y(x)| \mathrm{d}x < \int_a^b \frac{\epsilon}{b-a} \mathrm{d}x = \epsilon \end{align*}$$

即$$Q[y(x)]$$是连续泛函.

+ 泛函极值：对于曲线$$y(x)$$，满足

$$\begin{align*} \max_x \ |y_1(x) - y(x)| \leq \varepsilon \end{align*}$$

的一切连续曲线$$y_1(x)$$构成的集合就是$$y(x)$$的$$\epsilon$$-邻域，若对于邻域中的任意曲线$$y_1(x)$$都有

$$\begin{align*} Q[y_1(x)] \leq Q[y(x)] \end{align*}$$

则称泛函Q[y(x)]在y(x)的某个ε-邻域内取极值.

+ 线性泛函：若对于任意常数$$c1$$和$$c2$$，$$Q[f(x)]$$满足

$$\begin{align*} Q[c_1 y_1(x) + c_2 y_2(x)] = c_1 Q[y_1(x)] + c_2 Q[y_2(x)] \end{align*}$$

则称$$Q[f(x)]$$是线性泛函

+ 泛函变分：先来看一个例子，设泛函$$Q[f(x)]=\int_a^b y^2(x)\mathrm{d}x$$，函数$$y_1(x)=y(x) + \delta y(x)$$是对$$y(x)$$的一个扰动，则$$Q[f(x)]$$的增量为

$$\Delta Q=Q[y_1(x)]-Q[y(x)]=Q[y(x)+\delta y(x)]-Q[y(x)]=\int_a^b (y(x) + \delta y(x))^2 \mathrm{d}x-\int_a^b y^2(x) \mathrm{d}x$$

可见$$\Delta Q$$由两部分构成，将第一项记为

$$T[y(x),\delta y(x)] = \int_a^b 2y(x) \delta y(x) \mathrm{d}x$$

故对第二项有

$$
\begin{align*} 
\lim_{\max_{a \leq x \leq b} |\delta y(x)| \rightarrow 0} \frac{\int_a^b (\delta y(x))^2 \mbox{d}x}{\max_{a \leq x \leq b} |\delta y(x)|}
\leq \lim_{\max_{a \leq x \leq b} |\delta y(x)| \rightarrow 0} \frac{\left( \max_{a \leq x \leq b} |\delta y(x)| \right)^2 (b-a)}{\max_{a \leq x \leq b} |\delta y(x)|} 
= \lim_{\max_{a \leq x \leq b} |\delta y(x)| \rightarrow 0} \max_{a \leq x \leq b} |\delta y(x)| (b-a) 
= 0
\end{align*}
$$

即$$\int_a^b (\delta y(x))^2 \mathrm{d}x$$是关于$$\delta y(x)$$的高阶无穷小，记为$$o(\delta y(x))$$，于是

$$\Delta Q=T[y(x),\delta y(x)]+o(\delta y(x))$$

对比函数微分的概念，可以发现它们是何其地相似.故类似地，我们可以说，若对自变量$$y(x)$$作微小增量$$\delta y(x)$$，其相应的泛函的增量$$\Delta Q$$可以分为两部分，其中第一部分$$T[y(x),\delta y(x)]$$是关于$$\delta y(x)$$的线性泛函，第二部分是关于$$\delta y(x)$$的高阶无穷小，那么就将$$T[y(x),\delta y(x)]$$称作泛函$$Q[y(x)]$$的变分

## 预备定理

## Euler-Lagrange方程（ E-L quation）的推导

## 具体应用

下面有三个具体的应用

1.求连接$$(0,0)$$和$$(1,1)$$的所有曲线中长度最短的曲线.即求泛函$$\int_0^1 \sqrt{1 + y'^2} \mathrm{d}x$$的极值，记$$F(x, y(x), y'(x)) = \sqrt{1 + y'^2}$$，于是

$$\begin{align*}
F_y & = 0 \\
F_{y'} & = \frac{y'}{\sqrt{1 + y'^2}}
\end{align*}
$$

由E-L方程知

$$
\begin{align*}
\frac{\mbox{d}}{\mbox{d} x} \left( \frac{y'}{\sqrt{1 + y'^2}} \right) = 0 
\end{align*}
$$

故

$$\begin{align*}\frac{y'}{\sqrt{1 + y'^2}} = C \end{align*}$$

，其中$$C$$为某一常数，整理得

$$\begin{align*} y' = \pm \frac{c}{\sqrt{1-c^2}} \end{align*}$$

故最优曲线的斜率为常数，也即直线，由边界条件可知是$$y=x$$.