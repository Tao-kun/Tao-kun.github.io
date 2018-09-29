---
layout: post
title:  "算法-斐波那契数"
date:   2018-09-29 16:20:00 +0800
tags: [C++, Algorithm]
---

## 斐波那契数列

斐波那契数列及其相关算法问题

### 引入

Leonardo Fibonacci 在描述兔子生长的数目时用上了[这个数列](https://zh.wikipedia.org/wiki/%E6%96%90%E6%B3%A2%E9%82%A3%E5%A5%91%E6%95%B0%E5%88%97)

+ 第一个月初有一对刚诞生的兔子
+ 第二个月之后（第三个月初）它们可以生育
+ 每月每对可生育的兔子会诞生下一对新兔子
+ 兔子永不死去

### 分析

假设在n月有兔子总共a对，n+1月总共有b对。在n+2月必定总共有a+b对：因为在n+2月的时候，前一月（n+1月）的b对兔子可以存留至第n+2月（在当月属于新诞生的兔子尚不能生育）。而新生育出的兔子对数等于所有在n月就已存在的a对。

所以有

$$
\begin{align*} 
F(N)=
\begin{cases}
1 & x=1,2 \\
F(N-1)+F(N-2) & x > 2
\end{cases}
\end{align*} 
$$

当可以生育的间隔延长为时间T时（原问题间隔为3，即第三个月才能生育），这个函数将变为

$$
\begin{align*} 
F(N)=
\begin{cases}
1 & x=1,2,...,T-1 \\
F(N-1)+F(N-T+1) & x > T-1
\end{cases}
\end{align*} 
$$


## 算法问题

[Leetcode-爬楼梯](https://leetcode.com/problems/climbing-stairs/)

[BUAACODING-间隔为5](https://buaacoding.cn/problem/1442/index)

[BUAACODING-过台阶](https://buaacoding.cn/problem/860/index)

[BUAACODING-兔子会死亡](https://buaacoding.cn/problem/1430/index)