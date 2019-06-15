---
layout: post
title: "行列式"
excerpt: 你就不能领略下数学的美么?
cover: /img/head/liner-algebra1.jpg
categories:
  - linear-Algebra
tags:
  - 线性代数
---



# 二、三阶行列式

二阶行列式$$\begin{vmatrix}a_{11}&a_{12}\\a_{21} & a_{22}\end{vmatrix} = a_{11}a_{22} - a_{12}a_{21}$$.

即**主对角线元素** - **次对角线元素**.

三阶行列式$$\begin{vmatrix}
a_{11} & a_{12} &a_{13} \\
a_{21} & a_{22} & a_{23} \\
a_{31} & a_{32} & a_{33}
\end{vmatrix}= a_{11}a_{22}a_{33} + a_{12}a_{23}a_{31} + a_{13}a_{21}a_{32} - a_{22}a_{23}a_{32} - a_{12}a_{21}a_{33} - a_{13}a_{22}a_{31} = a_{11}\begin{vmatrix}a_{22} & a_{23} \\ a_{32} & a_{33}\end{vmatrix} - a_{12}\begin{vmatrix}a_{21} & a_{23}\\a_{31} & a_{33}\end{vmatrix} + a_{13}\begin{vmatrix}a_{21}&a_{22}\\a_{31}&a_{32}\end{vmatrix}$$



# 一般行列式

## n阶行列式

由$$n^2$$个数$$a_{ij}(i=1,2,3\dots,n; j=1,2,3,\dots,n)$$组成的$$n$$行$$n$$列$$\begin{vmatrix}a_{11}&a_{12}&\dots&a_{1n} \\ a_{21}&a_{22}&\dots&a_{2n} \\ \vdots & \vdots & & \vdots\\a_{n1}&a_{n2}&\dots&a_{nn}\end{vmatrix}$$的式子。

$$D = \begin{vmatrix}a_{11}&a_{12}&\dots&a_{1n}\\a_{21}&a_{22}&\dots&a_{2n}\\ \vdots&\vdots&&\vdots\\a_{n1}&a_{n2}&\dots&a_{nn}\end{vmatrix} = a_{11}A_{11} + a_{12}A_{12} + \dots + a_{1n}A_{1n}$$

其中，

$$a_{ij}$$为行列式中第$$i$$行第$$j$$列的元素.

$$A_{ij}= (-1)^{1+j}M_{ij}$$。

$$M_{ij}$$为$$D$$中划掉第一行和第$$j$$列之后，按原来顺序排成的$$n-1$$阶行列式

$$M_{ij} = \begin{vmatrix}a_{21}&\dots&a_{2,j-1}&a_{2,j+1}&\dots&a_{2n}\\a_{31}&\dots&a_{3,j-1}&a_{3,j+1}&\dots&a_{3n}\\\vdots&&\vdots&\vdots&&\vdots\\a_{n1}&\dots&a_{n.j-1}&a_{n, j+1}&\dots&a_{nn}\end{vmatrix}$$

**称$$Aij$$为元素$$a_{ij}$$的代数余子式​**.

**称$$Mij$$为元素$$a_{ij}$$的余子式**.



## 常见行列式的值

1. 对角行列式 $$D_n = \begin{vmatrix}a_1&&&\\&a_2&&\\&&\ddots&\\&&&a_n\end{vmatrix} = a_1a_2\dots a_n$$
2. 下三角行列式$$D_n = \begin{vmatrix}a_{11}&&&\\a_{21}&a_{22}&&\\\vdots&\vdots&\ddots&\\a_{n1}&a_{n2}&\dots&a_{nn}\end{vmatrix} = a_{11}a_{22}\dots a_{nn}$$
3. $$D_n = \begin{vmatrix}&&&b_n\\&&b_{n-1}&\\&\dots&\\b_1&&&\end{vmatrix} = (-1)^{\frac{n(n-1)}2}b_1b_2\dots b_n $$



# 行列式性质

## 转置行列式 $D^T$

$$D = \begin{vmatrix}a_{11}&a_{12}&\dots&a_{1n}\\ a_{21}&a_{22}&\dots&a_{2n}\\ \vdots&\vdots&\ddots&\vdots\\ a_{n1}&a_{n2}&\dots&a_{nn}\end{vmatrix}, D^T = \begin{vmatrix}a_{11}&a_{21}&\dots&a_{n1}\\ a_{12}&a_{22}&\dots&a_{n2}\\ \vdots&\vdots&\ddots&\vdots\\ a_{1n}&a_{2n}&\dots&a_{nn}\end{vmatrix}$$

## 性质1:   $D = D^T$

因此,上三角行列式$$\begin{vmatrix}a_{11}&a_{12}&\dots&a_{1, n-1}&a_{1n}\\ &a_{22}&\dots&a_{2, n-1}&a_{2n}\\ &&\ddots&\vdots&\vdots\\ &&&a_{n-1, n-1}&a_{n-1, n}\\ &&&&a_{nn}\end{vmatrix} = \begin{vmatrix}a_{11}&&&&\\ a_{12}&a_{22}&&&\\ \vdots&\vdots&\ddots&\\ a_{1, n-1}&a_{2,n-1}&\dots&a_{n-1,n-1}&\\ a_{1n}&a_{2n}&\dots&a_{n-1,n}&a_{nn}\end{vmatrix} = a_{11}a_{22}\dots a_{n-1,n-1}a_{nn}$$



>  **因为$$D^T = D$$，因此，下列性质对行列式的列也成立。**



## 性质2: 行列式无论按那一行展开,值都相等,为行列式的值

$$D = \begin{vmatrix}a_{11}&a_{12}&\dots&a_{1n}\\ a_{21}&a_{22}&\dots&a_{2n}\\ \vdots&\vdots&&\vdots\\ a_{n1}&a_{n2}&\dots&a_{nn}\end{vmatrix} = a_{i1}A_{i1} + a_{i2}A_{i2} + \dots + a_{in}A_{in}$$

## 性质3:行列式可以按行提取公因子

$$\begin{vmatrix}a_{11}&a_{12}&\dots&a_{1n}\\ \vdots&\vdots&&\vdots\\ ka_{i1}&ka_{i2}&\dots&ka_{in}\\ \vdots&\vdots&&\vdots\\ a_{n1}&a_{n2}&\dots&a_{nn}\end{vmatrix} = k\begin{vmatrix}a_{11}&a_{12}&\dots&a_{1n}\\ \vdots&\vdots&&\vdots\\ a_{i1}&a_{i2}&\dots&a_{in}\\ \vdots&\vdots&&\vdots\\ a_{n1}&a_{n2}&\dots&a_{nn}\end{vmatrix}$$

### 推论 行列式中,一行全为0时行列式为0

## 性质4: 拆行可加性

$$\underrightarrow{第i行} \begin{vmatrix}a_{11}&a_{12}&\dots&a_{1n}\\ \vdots&\vdots&&\vdots&\\ b_1+c_1&b_2+c_2&\dots&b_n+c_n\\ \vdots&\vdots&&\vdots&\\ a_{n1}&a_{n2}&\dots&a_{nn}\end{vmatrix} =  \begin{vmatrix}a_{11}&a_{12}&\dots&a_{1n}\\ \vdots&\vdots&&\vdots&\\ b_1&b_2&\dots&b_n\\ \vdots&\vdots&&\vdots&\\ a_{n1}&a_{n2}&\dots&a_{nn}\end{vmatrix} +  \begin{vmatrix}a_{11}&a_{12}&\dots&a_{1n}\\ \vdots&\vdots&&\vdots&\\ c_1&c_2&\dots&c_n\\ \vdots&\vdots&&\vdots&\\ a_{n1}&a_{n2}&\dots&a_{nn}\end{vmatrix}$$

## 性质5 两行对应元素相等(或成比例),行列式为0

### 推论

$$D = |a_{ij}|_n, \begin{cases}\sum^n_{k=1}a_{ik}A_{jk} = D \cdot \delta_{ij}\\ \sum^n_{k=1}a_{ki}A_{kj} = D\cdot\delta_{ij}\end{cases}, \delta_{ij} = \begin{cases}1, i=j\\ 0, i\neq j\end{cases}$$
$$\delta_{ij}$$被称为**克罗内克符号**.

## 性质6: 某行元素的若干倍添加到另一行,所得的行列式值不变

$$\begin{vmatrix}
a_{11}& a_{12}& \dots& a_{1n}\\
\vdots& \vdots& & \vdots\\
a_{i1}& a_{i2}& \dots& a_{in}\\
\vdots& \vdots& & \vdots\\
a_{j1}& a_{j2}& \dots& a_{jn}\\
\vdots& \vdots& & \vdots\\
a_{n1}& a_{n2}& \dots& a_{nn}\\
\end{vmatrix} = \begin{vmatrix}
a_{11}& a_{12}& \dots& a_{1n}\\
\vdots& \vdots& & \vdots\\
a_{i1}& a_{i2}& \dots& a_{in}\\
\vdots& \vdots& & \vdots\\
ka_{i1}+a_{j1}& ka_{i2}+a_{j2}& \dots& ka_{in}+a_{jn}\\
\vdots& \vdots& & \vdots\\
a_{n1}& a_{n2}& \dots& a_{nn}\\
\end{vmatrix}$$

## 性质7: 行列式两行互换,改变符号

$$\begin{vmatrix}
a_{11}& a_{12}& \dots& a_{1n}\\
\vdots& \vdots& & \vdots\\
a_{i1}& a_{i2}& \dots& a_{in}\\
\vdots& \vdots& & \vdots\\
a_{j1}& a_{j2}& \dots& a_{jn}\\
\vdots& \vdots& & \vdots\\
a_{n1}& a_{n2}& \dots& a_{nn}\\
\end{vmatrix} = -\begin{vmatrix}
a_{11}& a_{12}& \dots& a_{1n}\\
\vdots& \vdots& & \vdots\\
a_{j1}& a_{j2}& \dots& a_{jn}\\
\vdots& \vdots& & \vdots\\
a_{i1}& a_{i2}& \dots& a_{in}\\
\vdots& \vdots& & \vdots\\
a_{n1}& a_{n2}& \dots& a_{nn}\\
\end{vmatrix}$$

## 性质8 [拉普拉斯]展开定理

在$$D_n$$中选取$$k$$个行, $$D_n = \sum k个行产生的所有k阶子式 \times 子式对应的代数余子式$$



# 行列式的计算

> 将一般行列式转换成三角行行列式
>
> 将高阶行列式转换成低阶行列式

#### DEMO 1 

计算 $$D = \begin{vmatrix} a&b&\dots&b\\ b&a&\dots&b \\ \vdots&\vdots&&\vdots \\ b&b&\dots&a \end{vmatrix}$$

行列式的特点：*主对角线上的元素都相等，主对角线之外的元素也相等*。

从第二列起，每一列加到第一列。（性质1.6）$$D = \begin{vmatrix} a+(n-1)b&b&\dots&b\\ a+(n-1)b&a&\dots&b \\ \vdots&\vdots&&\vdots \\ a+(n-1)b&b&\dots&a  \end{vmatrix}$$

再将第一行的$$(-1)$$倍添加到其他行（性质1.6）$$D = \begin{vmatrix} a+(n-1)b&b&\dots&b\\ 0&a-b&\dots&0 \\ \vdots&\vdots&&\vdots \\ 0&0&\dots&a-b \end{vmatrix} = [a+(n-1)b](a-b)^{n-1}$$

#### DEMO2

计算行列式 $$D = \begin{vmatrix} 2&1\\ 1&2&1\\ & 1&\ddots&\ddots\\ &&\ddots&2&1 \\ &&&1&2 \end{vmatrix}$$

按第一行展开，有$$D = 2M_{11} - M_{12}$$。而$$M_{11} = D_{n-1}, M_{12} = D_{n-2}$$，因此$$D_n = 2D_{n-1} - D_{n-2}$$，移下项，

$$D_n - D_{n-1} = D_{n-1} - D_{n-2}$$

数列$$\{Dn\}$$是一个等差数列，公差是$$D_2 - D_1 = 1$$，首项是$$D_1 = 2$$，$$D_n = D_1 + (n-1) = n+1$$



# Cramer法则

假设有一个n元线性方程组

$$\begin{cases} a_{11}x_1 + a_{12}x_2 + \dots + a_{1n}x_n = b_{1} \\ a_{21}x_1 + a_{22}x_2 + \dots + a_{2n}x_n = b_{2}\\    \dots\\ a_{n1}x_1 + a_{n2}x_2 + \dots + a_{nn}x_n = b_{n}\end{cases}$$ 

将所有系数提出来构成一个行列式

$$D = \begin{vmatrix} a_{11}&a_{12}&\dots&a_{1n}\\ a_{21}&a_{22}&\dots&a_{2n}\\ \vdots&\vdots&&\vdots\\  a_{n1}&a_{n2}&\dots&a_{nn}\\  \end{vmatrix}$$

将$$D$$中的第$$i$$列替换成常数项$$b_1,b_2,\dots,b_n$$

$$D_1 =  \begin{vmatrix} b_1&a_{12}&\dots&a_{1n}\\ b_1&a_{22}&\dots&a_{2n}\\ \vdots&\vdots&&\vdots\\  b_1&a_{n2}&\dots&a_{nn}\\  \end{vmatrix}, D_2 =  \begin{vmatrix} a_{11}&b_1&\dots&a_{1n}\\ a_{21}&b_{2}&\dots&a_{2n}\\ \vdots&\vdots&&\vdots\\  a_{n1}&b_{2}&\dots&a_{nn}\\  \end{vmatrix}, \dots, D_n =  \begin{vmatrix} a_{11}&a_{12}&\dots&b_{1}\\ a_{21}&a_{22}&\dots&b_{2}\\ \vdots&\vdots&&\vdots\\  a_{n1}&a_{n2}&\dots&b_n\\  \end{vmatrix}$$

线性方程的解

$$x_i = D_i/D, (i = 1,2,\dots,n)$$

<script src="https://cdn.bootcss.com/mathjax/2.7.1/latest.js?config=TeX-AMS-MML_HTMLorMML"></script>