---
layout: post
title:  "Gamma函数是如何被发现的？"
date:   2017-10-12 21:23:00 +0800
tags: [Mathematics]
---

这是一篇转载的博文，原地址为：<del>[Gamma函数是如何被发现的？](http://www.cnblogs.com/murongxixi/p/3663125.html)</del>

原博客无法进入，备用链接：[Gamma函数是如何被发现的？](https://www.tuicool.com/articles/7JFRf2)


学过微积分的人，肯定都接触过Euler积分，按教科书上的说法，这是两种含有参变量的定积分，但其实没那么玄乎，它们只是两个函数。其中第一型Euler积分叫$B$-函数，第二型Euler积分叫$\Gamma$-函数，这两个函数的定义如下：

$$
\begin{align} 
\label{eq: beta} B (m, n) & = \int_0^1 x^{m-1} (1-x)^{n-1} \mathrm{d} x \\
\label{eq: gamma} \Gamma (n) & = \int_0^{\infty} x^{n-1} e^{-x} \mathrm{d} x
\end{align}
$$

一般教科书上的解释就仅限于此了，最多再给几个恒等式，至于它们为何长得如此奇怪，基本都是缄口不提的。今天笔者闲来无聊，考证了一番，才弄明白这其中的来龙去脉。

故事要追溯到18世纪初，当时数学界两个比较热门的研究方向是插值理论和积分方法。积分想必大家都知道，那什么是插值呢？举个简单的例子，考虑如下的一系列数：$1$，$1+2$，$1+2+3$，$\cdots$，这样的数被称作三角形数(triangular numbers)，因为这些数量的(石子)可以排成不同尺寸的等边三角形。那么很自然地，就会有人问第$n$个三角形数$T_n$是多少，答案很简单，一般小学生都能答出来：

$$
\begin{align}
\label{eq: triangular numbers} T_n = \frac{1}{2} n (n+1)
\end{align}
$$

但是再仔细看一下(\ref{eq: triangular numbers})式，你会发现它又不是那么简单。本来我们只关心$n$为正整数时，$T_n$的取值是多少，但实际上有了(\ref{eq: triangular numbers})式后，$n$即使取$\sqrt{2}$这样的数，我们也可以算出一个值来。换言之，函数的定义域被扩展了，本来$T_n$的定义域是正整数集，现在扩展到了整个实数集，在函数本来没有定义的地方赋一个新值就是插值。类似的问题还有很多，比如指数运算$a^x$本来是为了方便表达$x$个$a$连乘而引入的，因此最初$x$只取正整数，但是我们也好奇$2.5$个$ a $连乘会是什么情况，$-\sqrt{3}$个$a$连乘的值是多少，因此我们就需要将定义域进行扩展。

用现代数学的观点看，插值似乎是个很无厘头的问题，因为函数只是一个数集到另一个数集的对应关系，对于定义域中需要扩展的部分，大可以赋以任意值，这样可以得到无穷多个插值函数。但是在18世纪初，数学家们普遍认为函数是必须有一个代数表达式的，插值就是要找到一个代数表达式，在满足原本定义域上的对应关系的基础上有更广的定义域。

在形形色色的插值问题中，有一个问题困扰了Christian Goldbach(1690-1764)很久，就是阶乘函数$n!$的插值问题。于是他就写信求助于Daniel Bernoulli(1700-1784)，当时Leonhard Euler(1707-1783)和Bernoulli在一起，因此也知晓了这个问题。后来1729年，Euler漂亮地解决了这个问题，并给Goldbach去了一封信，$\Gamma$-函数就诞生于这封信中，这一年，Euler只有22岁。

下面就让我们怀着景仰的心情，来近距离观察一下，数学大师是如何思考并解决问题的。众所周知，Euler对求和有着极其狂热的崇拜，因此他首先考虑了通项为$n!$的级数：$$\begin{align*} 1 + 1 \cdot 2 + 1 \cdot 2 \cdot 3 + \cdots \end{align*}$$通过观察，Euler发现随着$n$趋向于无穷，这个级数会越来越像等比级数，据此他得到通项的一个表达式，即

$$
\begin{align}
\label{eq: factorial} 
\left[ \left( \frac{2}{1} \right)^n \frac{1}{n+1} \right]
\left[ \left( \frac{3}{2} \right)^n \frac{2}{n+2} \right]
\left[ \left( \frac{4}{3} \right)^n \frac{3}{n+3} \right] \cdots
= n!
\end{align}
$$

恕笔者能力有限，实在无法理解大师这突破天际的脑回路。但我们不难验证有

$$
\begin{align*}
& \left[ \left( \frac{2}{1} \right)^n \frac{1}{n+1} \right]
\left[ \left( \frac{3}{2} \right)^n \frac{2}{n+2} \right]
\left[ \left( \frac{4}{3} \right)^n \frac{3}{n+3} \right] \cdots \\
= &\lim_{m \rightarrow \infty} \frac{1 \cdot 2 \cdots m}{(n+1)(n+2)\cdots(n+m)} (m+1)^n \\  
= & \lim_{m \rightarrow \infty} 1 \cdot 2 \cdots n \frac{(n+1)(n+2)\cdots m}{(n+1)(n+2)\cdots m} \frac{(m+1)^n}{(m+1)(m+2)\cdots(m+n)} \\  
= & n! \lim_{m \rightarrow \infty} \frac{(m+1)^n}{(m+1)(m+2)\cdots(m+n)} \\ 
= & n!
\end{align*}
$$

有了(\ref{eq: factorial})式，Euler就尝试将$n$取一些具体的值。特别地，当$n = \frac{1}{2}$时有

$$
\begin{align*}
\left(\frac{1}{2}\right)!
= \sqrt{\frac{2}{1} \cdot \frac{1^2 \cdot 2 \cdot 2}{3 \cdot 3} \cdot \frac{3}{2} \cdot \frac{2^2 \cdot 2 \cdot 2}{5 \cdot 5} \cdot \frac{4}{3} \cdot \frac{3^2 \cdot 2 \cdot 2}{7 \cdot 7} \cdots} 
= \sqrt{\frac{2 \cdot 4}{3 \cdot 3} \cdot \frac{4 \cdot 6}{5 \cdot 5} \cdot \frac{6 \cdot 8}{7 \cdot 7} \cdots}
\end{align*}
$$

而恰巧John Wallis(1616-1703)在1665年研究半圆曲线$y = \sqrt{x(1-x)}$下的面积时曾得到

$$
\begin{align*}
\frac{2 \cdot 4}{3 \cdot 3} \cdot \frac{4 \cdot 6}{5 \cdot 5} \cdot \frac{6 \cdot 8}{7 \cdot 7} \cdots
= \frac{\pi}{4}
\end{align*}
$$

于是结合上面两式可得

$$
\begin{align*}
\left(\frac{1}{2}\right)! = \frac{\sqrt{\pi}}{2}
\end{align*}
$$

在Euler这样的老狐狸眼里，一旦扯上$\pi$，自然就和圆相关的积分逃不了干系，事实上Wallis公式就是在处理$\int_0^1 x^{\frac{1}{2}} (1-x)^{\frac{1}{2}} \mathrm{d} x$这样的积分。既然$\frac{1}{2}!$和积分相关，那么$n!$应该也可以表达为某种积分的形式，于是Euler开始考虑如下一般形式的积分

$$
\begin{align*}
E(m,n) = \int_0^1 x^m (1-x)^n \mathrm{d} x
\end{align*}
$$

其中$m$是任意数，$n$是整数。由分部积分易知有

$$
\begin{align*}
E(m,n) & = \frac{1}{m+1} \int_0^1 (1-x)^n \mathrm{d} x^{m+1} \\
& = \frac{1}{m+1} x^{m+1} (1-x)^n |_0^1 - \frac{1}{m+1} \int_0^1 x^{m+1} \mathrm{d} (1-x)^n \\
& = \frac{n}{m+1} \int_0^1 x^{m+1}(1-x)^{n-1} \mathrm{d} x \\
& = \frac{n}{m+1} E(m+1,n-1)
\end{align*}
$$

于是递推下去有

$$
\begin{align*}
E(m,n)
& = \frac{n}{m+1} E(m+1,n-1) \\
& = \frac{n}{m+1} \frac{n-1}{m+2} E(m+2,n-2) \\
& = \cdots \\
& = \frac{n}{m+1} \frac{n-1}{m+2} \cdots \frac{1}{m+n} E(m+n,0) \\
\end{align*}
$$

又

$$
\begin{align*}
E(m+n,0) = \int_0^1 x^{m+n} \mathrm{d} x = \frac{1}{m+n+1}
\end{align*}
$$

于是

$$
\begin{align}
\label{eq: E} E(m,n)
= \frac{n}{m+1} \frac{n-1}{m+2} \cdots \frac{1}{m+n} \frac{1}{m+n+1}
\end{align}
$$

整理一下(\ref{eq: E})式可得

$$
\begin{align*}
\frac{n!}{(m+1)(m+2) \cdots (m+n)} = (m+n+1) \int_0^1 x^m (1-x)^n \mathrm{d} x
\end{align*}
$$

下面就是体现Euler技巧的地方了，先做一个变量代换$m = u/v$，于是

$$\begin{align}
\label{eq: Euler trick} \frac{n!}{(u+v)(u+2v)\cdots (u+nv)} 
= \frac{u+(n+1)v}{v^{n+1}} \int_0^1 x^{u/v} (1-x)^n \mathrm{d} x
\end{align}
$$

注意当$u \rightarrow 1$且$v \rightarrow 0$时，(\ref{eq: Euler trick})式左端$\rightarrow n!$。下面考察(\ref{eq: Euler trick})式右端，做变量代换$x = y^{v/(u+v)}$，于是

$$
\begin{align*}
\mathrm{d} x = \frac{v}{u+v} y^{-u/(u+v)} \mathrm{d} y
\end{align*}
$$

故(\ref{eq: Euler trick})式右端变为

$$
\begin{align*}
\frac{u+(n+1)v}{v^{n+1}} & \int_0^1 y^{u/(u+v)} (1-y^{v/(u+v)})^n \frac{v}{u+v} y^{-u/(u+v)} \mathrm{d} y \\
= \frac{u+(n+1)v}{v^n (u+v)} & \int_0^1 (1-y^{v/(u+v)})^n \mathrm{d} y \\
= \frac{u+(n+1)v}{(u+v)^{n+1}} & \int_0^1 \left(\frac{1-y^{v/(u+v)}}{v/(u+v)}\right)^n \mathrm{d} y
\end{align*}
$$

综上我们有

$$
\begin{align*}
n! 
& = \lim_{u \rightarrow 1, v \rightarrow 0} \frac{u+(n+1)v}{(u+v)^{n+1}} \int_0^1 \left(\frac{1-y^{v/(u+v)}}{v/(u+v)}\right)^n \mathrm{d} y \\
& = \int_0^1 \left(\lim_{u \rightarrow 1, v \rightarrow 0} \frac{1-y^{v/(u+v)}}{v/(u+v)}\right)^n \mathrm{d} y \\
& = \int_0^1 (-\ln y)^n \mathrm{d} y
\end{align*}
$$

其中第二个等号成立(交换极限和积分的次序)是因为关于$y$的函数$\left(\frac{1-y^{v/(u+v)}}{v/(u+v)}\right)^n$在$(0,1]$上一致收敛于$\left( -y^{v/(u+v)} \ln y \right)^n$且$\int_0^1 \left( -y^{v/(u+v)} \ln y \right)^n \mathrm{d} y$是良定义的，第三个等号可由L'Hospital法则推出。

进一步设$-\ln y = x$，即$y = e^{-x}$，可得

$$
\begin{align*}
n!
= \int_0^1 (-\ln y)^n \mathrm{d} y = \int_\infty^0 x^n (- e^{-x}) \mathrm{d} x
= \int_0^\infty x^n e^{-x} \mathrm{d} x
\end{align*}
$$

这和(\ref{eq: gamma})式的形式已经很像了，区别仅仅是$x$的指数。事实上一开始Euler确实就是把$\Gamma (n)$定义成上式右端那样的，也即$\Gamma (n) = n!$。注意(\ref{eq: E})式也可写成

$$
\begin{align*}
E(m,n) = \frac{m!n!}{(m+n+1)!}
\end{align*}
$$

于是此时有

$$
\begin{align*}
E(m,n) = \frac{\Gamma (m) \Gamma (n)}{\Gamma (m+n+1)}
\end{align*}
$$

后来可能是出于方便美观的原因吧，Adrien Marie Legendre(1752-1833)将$\Gamma$-函数的定义修改成了(\ref{eq: gamma})式那样，也即$\Gamma (n) = (n-1)!$，并将$E(m,n)$修改成 (\ref{eq: beta}) 式 那样，也即$B(m,n) = \frac{(m-1)!(n-1)!}{(m+n-1)!}$，于是此时有

$$
\begin{align*}
B(m,n) = \frac{\Gamma (m) \Gamma (n)}{\Gamma (m+n)}
\end{align*}
$$

这显然比前一个式子要漂亮不少，于是这个定义就被人们普遍接受了，现在教科书上看到的也都是这个形式。