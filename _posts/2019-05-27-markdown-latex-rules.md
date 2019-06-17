---
layout: post
title: "Jekyll+Markdown中的Latex公式"
excerpt: markdown和Latex.
cover: /img/head/markdown-latex.jpg
categories:
  - markdown-latex
tags:
  - markdown
  - Latex
---

# 引入

> 如果你的 Jekyll 主题已经支持了 Latex 公式，可以跳过引入部分。

如果你的主题没有引入`mathjax`库来为 Latex 公式提供支持，需要在主题的布局文件（如`_layouts/default.html`）中引入：

```html
<script
  src="http://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS_HTML"
  type="text/javascript"
></script>
<!-- mathjax config similar to math.stackexchange -->
<script type="text/x-mathjax-config">
  MathJax.Hub.Config({
   jax: ["input/TeX", "output/HTML-CSS"],
   tex2jax: {
       inlineMath: [ ['$', '$'] ],
       displayMath: [ ['$$', '$$']],
       processEscapes: true,
       skipTags: ['script', 'noscript', 'style', 'textarea', 'pre', 'code'] },
   messageStyle: "none",
   "HTML-CSS": { preferredFont: "TeX", availableFonts: ["STIX","TeX"] }
  });
</script>
```

# 使用

在 Markdown 中，使用单美元符号`$ 公式 $`插入行内公式，如 $$a + b = 1$$ ，行间公式使用双美元号`$$ 公式 $$`。如：

```
$$ (\overbrace{a_0,a_1,...,a_n}^{\text{共 \\\\\\$n+1\\\\\\$ 项}}) = (\underbrace{0,0,...,0}\\\\\\_n,1) $$
```

$$ (\overbrace{a_0,a_1,...,a_n}^{\text{共 \\\\\\$n+1\\\\\\$ 项}}) = (\underbrace{0,0,...,0}\\\\\\_n,1) $$

# 上标与下标

*上标*使用`^`表示，*下标*使用`_`表示。如`$10^n$`表示$$10^n$$，而`$a_i$`将会得到$$ a_i$$。当上标与下标**多于一个字符**时。使用花括号`{}`进行分组，以确定上下标范围，如`$A\\\\\\\_{ij} = 2^{i+j}$`得到$$A_{ij} = 2^{i+j}$$。

同时使用上标和下标时，上下标的先后次序并不重要，二者互不影响。如`$a_i^j$`与`$a^j_i$`都会得到$$a^j_i$$。嵌套使用上下标时，外层公式一定要使用分组。如`$a^b^c$`是**一个错误的公式($$a^b^c$$)**, 而`${a^b}^c$`或者`$a^{b^c}$`将会得到$$a^{b^c}$$。

数学公式中单引号是一种特殊的上标，表示用符号`\prime`(即’)做上标，可以与下标混用，也可以连续使用，但不能与上标直接混用（_混用就相当于嵌套了_），如：

```
$a=a'$,$b_0'=b_0''$,
${c'}^2=(c')^2$
```

表示：

$$a=a'$$,$$b_0'=b_0''$$,
$${c'}^2=(c')^2$$

# 上下划线和花括号

`\overline` 和 `\underline`命令可用来在公式的上方和下方划横线。`\overbrace`和`\underbrace`为公式添加上下花括号。

|                    代码                    |                    结果                    |
| :----------------------------------------: | :----------------------------------------: |
|          `$\overleftarrow {a+b}$`          |          $$\overleftarrow {a+b}$$          |
|         `$\overrightarrow {a+b}$`          |         $$\overrightarrow {a+b}$$          |
|       `$\overleftrightarrow {a+b}$`        |       $$\overleftrightarrow {a+b}$$        |
|         `$\underleftarrow {a+b}$`          |         $$\underleftarrow {a+b}$$          |
|         `$\underrightarrow {a+b}$`         |         $$\underrightarrow {a+b}$$         |
|       `$\underleftrightarrow {a+b}$`       |       $$\underleftrightarrow {a+b}$$       |
|    `$\vec {ab} = \overrightarrow {AB}$`    |    $$\vec {ab} = \overrightarrow {AB}$$    |
| `$\overbrace{a+b+c} = \underbrace{a+b+c}$` | $$\overbrace{a+b+c} = \underbrace{a+b+c}$$ |

还可以使用上下标在花括号上做标注：

```
$$ (\overbrace{a_0,a_1,...,a_n}^{\text{共 $n+1$ 项}}) = (\underbrace{0,0,...,0}_n,1) $$
```

$$(\overbrace{a_0, a_1, ..., a_n}^{\text{共n+1项}}) = (\underbrace{0, 0, ... , 0, 1}_n)$$

# 分式

Latex 中，分式格式为`\frac<分子><分母>`，如：

`$\frac 12 + \frac 1a = \frac {2+a}{2a}$`$$\frac 12 + \frac 1a = \frac {2+a}{2a}$$

连分式是一种特殊的分式，`amsmath`提供的`\cfrac`专用于输入连分式。这个命令可以带一个可选的参数 l、c、r，表示左、中、右（对齐），默认是居中，如：
`$$ \cfrac{1}{1+\cfrac{2}{1+\cfrac{3}{1+x}}} = \cfrac[r]{1}{1+\cfrac[c]{2}{1+\cfrac[l]{3}{1+x}}} $$`

得到

$$  \cfrac{1}{1+\cfrac{2}{1+\cfrac{3}{1+x}}} = \cfrac[r]{1}{1+\cfrac{2}{1+\cfrac[l]{3}{1+x}}} $$

`amsmath`提供了`\binom`来输入二项式系数，用法与`\frac`类似：

```
$$ (a+b)^2 = \binom {20}{02} a^2 + \binom 21 ab + \binom 22 b^2 $$
```

$$ (a+b)^2 = \binom {20}{02} a^2 + \binom 21 ab + \binom 22 b^2 $$

# 根式

`\sqrt`表示根式，可以带一个可选参数，表示开方次数，如:

`$\sqrt 4 = \sqrt[3] 8 = 2$`得到$$\sqrt 4 = \sqrt[3] 8 = 2$$。

# 希腊字母

|   $$\alpha$$    |   `\alpha`    |  $$\theta$$   |  `\theta`   |     $$o$$     |     `o`     | $$\upsilon$$ | `\upsilon` |
| :-------------: | :-----------: | :-----------: | :---------: | :-----------: | :---------: | :----------: | :--------: |
|    $$\beta$$    |    `\beta`    | $$\vartheta$$ | `\vartheta` |    $$\pi$$    |    `\pi`    |   $$\phi$$   |   `\phi`   |
|   $$\gamma$$    |   `\gamma`    |   $$\iota$$   |   `\oita`   |  $$\varpi$$   |  `\varpi`   | $$\varphi$$  | `\varphi`  |
|   $$\delta$$    |   `\delta`    |  $$\kappa$$   |  `\kappa`   |   $$\rho$$    |   `\rho`    |   $$\chi$$   |   `\chi`   |
|  $$\epsilon$$   |  `\epsilon`   |  $$\lambda$$  |  `\lambda`  |  $$\varrho$$  |  `\varrho`  |   $$\psi$$   |   `\psi`   |
| $$\varepsilon$$ | `\varepsilon` |    $$\mu$$    |    `\mu`    |  $$\sigma$$   |  `\sigma`   |  $$\omega$$  |  `\omega`  |
|    $$\zeta$$    |    `\zeta`    |    $$\nu$$    |    `\nu`    | $$\varsigma$$ | `\varsigma` |              |            |
|    $$\eta$$     |    `\eta`     |    $$\xi$$    |    `\xi`    |   $$\tau$$    |   `\tau`    |              |            |
|   $$\Gamma$$    |   `\Gamma`    |  $$\Lambda$$  |  `\Lambda`  |  $$\Sigma$$   |  `\Sigma`   |   $$\Psi$$   |   `\Psi`   |
|   $$\Delta$$    |   `\Delta`    |    $$\Xi$$    |    `\Xi`    | $$\Upsilon$$  | `\Upsilon`  |  $$\Omega$$  |  `\Omega`  |
|   $$\Theta$$    |   `\Theta`    |    $$\Pi$$    |    `\Pi`    |   $$\Phi$$    |   `\Phi`    |              |            |

# 二元关系

可以在下列符号的相应命令之前加上`\not`命令，而得到其否定形式。如`$$A\in B$$`表示$$A \in B$$，`$$A \notin B$$`表示$$A \notin B$$。

参阅[更加完整的 Latex 符号](https://blog.csdn.net/zgj926503/article/details/52757631)。

| 小于等于 | 大于等于 |  属于   |  属于   | 远小于  | 远大于  |   约等于    |   相似   |
| :------: | :------: | :-----: | :-----: | :-----: | :-----: | :---------: | :------: |
|  `\leq`  |  `\geq`  |  `\in`  |  `\ni`  |  `\ll`  |  `\gg`  |  `\approx`  |  `\sim`  |
| $$\leq$$ | $$\geq$$ | $$\in$$ | $$\ni$$ | $$\ll$$ | $$\gg$$ | $$\approx$$ | $$\sim$$ |

# 二元运算符

|     乘     | 除       | 正负号  | 正负号 2 |   交集   |   并集   |    交    |    并     |   点乘    |
| :--------: | -------- | :-----: | :------: | :------: | :------: | :------: | :-------: | :-------: |
|  `\times`  | `\div`   |  `\mp`  |  `\pm`   |  `\cup`  |  `\cap`  |  `\vee`  |  `\land`  |  `\cdot`  |
| $$\times$$ | $$\div$$ | $$\mp$$ | $$\pm$$  | $$\cup$$ | $$\cap$$ | $$\vee$$ | $$\land$$ | $$\cdot$$ |

# 其他符号

|  `\nabla`  |  `\forall`  |  `\partial`  |  `\exists`  |
| :--------: | :---------: | :----------: | :---------: |
| $$\nabla$$ | $$\forall$$ | $$\partial$$ | $$\exists$$ |

# 求和、求积、取极限

| 求和     | 积分     | 双重积分  | 三重积分   | 环形积分  | 求积      | 极限     |
| -------- | -------- | --------- | ---------- | --------- | --------- | -------- |
| `\sum`   | `\int`   | `\iint`   | `iiint`    | `\oint`   | `\prod`   | `\lim`   |
| $$\sum$$ | $$\int$$ | $$\iint$$ | $$\iiint$$ | $$\oint$$ | $$\prod$$ | $$\lim$$ |

二重和三重环形积分的命令应该是`\oiint`、`\oiiint`，但是我的 Jekyll 主题上不能正常渲染（Typora 编辑器可以正常显示）。使用`\def`指令来自己定义一个：

```
%------LaTex源码------%
\def\ooint{ {\bigcirc}\kern-11.5pt{\int}\kern-6.5pt{\int}}
\def\oooint{ {\bigcirc}\kern-12.3pt{\int}\kern-7pt{\int}\kern-7pt{\int}}
\ooint, \oooint
```

$$
\def\ooint{ {\bigcirc}\kern-11.5pt{\int}\kern-6.5pt{\int}}
\def\oooint{ {\bigcirc}\kern-12.3pt{\int}\kern-7pt{\int}\kern-7pt{\int}}
\ooint,  \oooint$$

现在应该可以写一些简单的公式了：

| 代码                                                         | 结果                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| `$\Phi = { {\circ}\kern-5.5pt{\int}\kern-7.5pt{\int} }_{\Omega} Pdydz + Qdzdx + Rdxdy$` | $$\Phi = { {\circ}\kern-5.5pt{\int}\kern-7.5pt{\int} }_{\Omega} Pdydz + Qdzdx + Rdxdy$$ |
| `$\bar x = \frac{M_y}M = \frac{\sum^n_{i=1}m_ix_i}{\sum^n_{i=1}M_i}$` | $$\bar x = \frac{M_y}M = \frac{\sum^n_{i=1}m_ix_i}{\sum^n_{i=1}M_i}$$ |
| `$\frac{\partial z}{\partial x}\arrowvert_{\begin{align} x=x_0 \\ y=y_0\end{align}} = \lim_{\Delta x \to 0}\frac{\Delta z}{\Delta x} = \lim_{\Delta x \to 0}\frac{f(x_0 + \Delta x, y_0) - f(x_0,y_0)}{\Delta x}$` | $$\frac{\partial z}{\partial x}\arrowvert_{\begin{align} x=x_0 \\ y=y_0\end{align}} = \lim_{\Delta x \to 0}\frac{\Delta z}{\Delta x} = \lim_{\Delta x \to 0}\frac{f(x_0 + \Delta x, y_0) - f(x_0,y_0)}{\Delta x}$$ |





# 矩阵

矩阵可以用命令`\matrix`和`\pmatrix`表示，各类矩阵环境的区别于外面的括号不同。

|  环境   |                            代码                             |                            结果                             |
| :-----: | :---------------------------------------------------------: | :---------------------------------------------------------: |
| matrix  |  `$$\begin{matrix} 1&0&0\\ 0&1&0\\ 0&0&1\\ \end{matrix}$$`  |   $$\begin{matrix} 1&0&0\\ 0&1&0\\ 0&0&1\\ \end{matrix}$$   |
| bmatrix | `$$\begin{bmatrix} 1&0&0\\ 0&1&0\\ 0&0&1\\ \end{bmatrix}$$` | $$\begin{bmatrix} 1&0&0 \\ 0&1&0 \\ 0&0&1\\ \end{bmatrix}$$ |
| vmatris | `$$\begin{vmatrix} 1&0&0\\ 0&1&0\\ 0&0&1\\ \end{vmatrix}$$` |  $$\begin{vmatrix} 1&0&0\\ 0&1&0\\ 0&0&1\\ \end{vmatrix}$$  |
| pmatrix | `$$\begin{pmatrix} 1&0&0\\ 0&1&0\\ 0&0&1\\ \end{pmatrix}$$` |  $$\begin{pmatrix} 1&0&0\\ 0&1&0\\ 0&0&1\\ \end{pmatrix}$$  |
| Bmatrix | `$$\begin{Bmatrix} 1&0&0\\ 0&1&0\\ 0&0&1\\ \end{Bmatrix}$$` |  $$\begin{Bmatrix} 1&0&0\\ 0&1&0\\ 0&0&1\\ \end{Bmatrix}$$  |
| Vmatrix | `$$\begin{Vmatrix} 1&0&0\\ 0&1&0\\ 0&0&1\\ \end{Vmatrix}$$` |  $$\begin{Vmatrix} 1&0&0\\ 0&1&0\\ 0&0&1\\ \end{Vmatrix}$$  |

书写矩阵时，不同的列使用`&`分隔，行用`\\`分隔。如：

```
$$

A_1 & A_2 & A_3 \\
B_1 & B_2 & B_3 \\
C_1 & C_2 & C_3 \\
\end{Vmatrix}\\\\\\\\\\$\$

```

$$\begin{Vmatrix}
A_1 & A_2 & A_3 \\
B_1 & B_2 & B_3 \\
C_1 & C_2 & C_3 \\
\end{Vmatrix}$$

在矩阵中经常使用各种省略号即`\dots`、`\vdots`、`\ddots`、`\iddots`，amsmath还提供了可以跨多列的省略号`\hdotsfor{<列数>}`。

如：

```

$$
1& \dots& 0\\
\vdots& \ddots& \vdots\\
0& \dots& 1\\
\end{bmatrix}$$
```
$$

1& \dots& 0\\
\vdots& \ddots& \vdots\\
0& \dots& 0\\
\end{bmatrix}\\\\\\\\\\$\$

`smallmatrix`可以生成行内的小矩阵，如`$$\begin{smallmatrix} a&b \\ c&d \\ \end{smallmatrix}$$`将生成矩阵$$\begin{smallmatrix} a&b \\ c&d \\ \end{smallmatrix}$$

$$
# 公式组

不需要对齐的公式用`gather`，`align`将会使公式组对齐。

|                           代码                           |                          结果                          |
| :------------------------------------------------------: | :----------------------------------------------------: |
| `$$\begin{gather} a = b+c+d \\ x = x + y \end{gather}$$` | $$\begin{gather} a = b+c+d \\ x = x + y \end{gather}$$ |
| `$$\begin{align} &a = b+c+d \\ &x = x + y \end{align}$$` | $$\begin{align} &a = b+c+d \\ &x = x + y \end{align}$$ |
|  `$$\begin{align} a = b+c+d \\ x = x + y \end{align}$$`  | $$\begin{align} a = b+c+d \\  x = x + y \end{align}$$  |



# 方程组/分段函数

使用`cases`环境来书写方程式。如：

```
$$

-x, \quad x\leq0 \\
x, \quad x>0
\end{cases}\\\\\\\\\$\$

```

$$y = \begin{cases}
-x, \quad x\leq0 \\
x, \quad x>0
\end{cases}$$



<script src="https://cdn.bootcss.com/mathjax/2.7.1/latest.js?config=TeX-AMS-MML_HTMLorMML"></script>
$$
```
