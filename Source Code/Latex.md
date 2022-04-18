---
title: latex语法
tag: Latex
thumbnail: https://www.latex-project.org/img/latex-project-logo.svg
---
# Latex数学公式语法
自己写一下，方便你我他。
||符号|例子|
|--|--|--|
|下标|_|$a_1+a_2+...+a_n$|
上标|^|$2^3+3^3+4^3$
分数|\frac{1}{2}|$\frac{1}{2}$
|根号|\sqrt[4]5|$\sqrt[4]5$
累加|\sum|$\sum^k_{i = 0}a_i$|
累乘|\prod|$\prod^k_{i=0}n_ip^i$| 
极限|\lim|$\lim_{i\to0}\frac{sinx}x$|
|积分|\int|$\int_a^b{sinx}\mathrm{d}x$|
Latex会默认压缩上下的空间，所以写的时候可以加上`\limits`变成我们熟悉的样子
$\sum\limits^k_{i = 0}a_i$
`\sum\limits^k_{i = 0}a_i`
$\prod\limits^k_{i=0}n_ip^i$
`\prod\limits ^k_{i=0}n_ip ^i`
$\lim\limits_{i\to0}\frac{sinx}x$
`\lim\limits_{i\to0}\frac{sinx}x`
$\int_a^b{sinx}dx$
`\int_a^b{sinx}dx`

## 一些运算符
|运算符名称	|加减	|乘|	除|	点乘	|大于等于|	小于等于|	不等于|	约等于|	恒等于
|--|--|--|--|--|--|--|--|--|--|
|code	|\pm	|\times|	\div|	\cdot|	\geq|	\leq	|\neq	|\approx|	\equiv
|数学符号|	±	|×|	÷|	⋅|	≥|	≤|	≠	|≈|	≡|
其他常用的：

|\ll | \gg | \prec|  \succ| \preceq| \succeq |\mp|  \leftrightarrow|  \Rightarrow| \exists| \forall|\in|  \cup|  \cap| \infty|
|--|--|--|--|--|--|--|--|--|--|--|--|--|--|--|
$\ll  \gg  \prec  \succ \preceq \succeq \mp  \leftrightarrow  \Rightarrow \exists \forall  \in  \cup  \cap \infty$

文章很多参考了[这篇](https://www.cnblogs.com/endlesscoding/p/9797237.html)博客的内容