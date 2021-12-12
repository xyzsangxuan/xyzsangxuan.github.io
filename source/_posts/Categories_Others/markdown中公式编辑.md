---
title: markdown中公式编辑教程
date: 2020-07-03 03:17:37
tags: 
    - math
categories: 
    - 杂项
cover: /img/cover1.png
top_img: /img/cover1.png
mathjax: true
description: 学习markdown编辑公式的文档和教程
keywords: markdown&math
---
# 数学公式和符号
## 行内公式和行间公式
&ensp;&ensp;&ensp;&ensp;行内公式是在公式代码块的基础上前面加上$ ，后面加上$ 组成的，行间公式则是在公式代码块前后使用$$ 和$$ 。
* 行内公式：$\Gamma(z) = \int_0^\infty t^{z-1}e^{-t}dt\,.$
* 行间公式：
$$\Gamma(z) = \int_0^\infty t^{z-1}e^{-t}dt\,.$$
代码块：
```
* 行内公式：$\Gamma(z) = \int_0^\infty t^{z-1}e^{-t}dt\,.$
* 行间公式：
$$\Gamma(z) = \int_0^\infty t^{z-1}e^{-t}dt\,.$$
```
## 希腊字母
| 名称 | 大写 | code | 小写 | code |
| ---- | ---- | ---- | ---- | ---- |
| alpha  | A | A | α | \alpha | 
| beta | B  | B  | β  | \beta |
| gamma | Γ | \Gamma | γ | \gamma |
| delta | Δ | \Delta | δ | \delta |
| epsilon | E | E | ϵ | \epsilon |
| zeta | Z | Z | ζ | \zeta |
| eta | H | H | η | \eta |
| theta | Θ | \Theta | θ | \theta |
| iota | I | I | ι | \iota |
| kappa | K | K | κ | \kappa |
| lambda | Λ | \Lambda | λ | \lambda |
| mu | M | M | μ | \mu |
| nu | N | N | ν | \nu |
| xi | Ξ | \Xi | ξ | \xi |
| omicron | O | O | ο | \omicron |
| pi | Π | \Pi | π | \pi |
| rho | P | P | ρ | \rho |
| sigma | Σ | \Sigma | σ | \sigma |
| tau | T | T | τ | \tau |
| upsilon | Υ  | Y | υ | \upsilon |
| phi | Φ | \Phi | ϕ | \phi |
| chi | X | X | χ | \chi |
| psi | Ψ | \Psi | ψ | \psi |
| omega | Ω | \Omega | ω | \omega |
## 上标与下标
&ensp;&ensp;&ensp;&ensp;上标和下标分别使用^ 与_ ，例如```$x_i^2$```表示的是：$x_i^2$。

&ensp;&ensp;&ensp;&ensp;默认情况下，上、下标符号仅仅对下一个组起作用。一个组即单个字符或者使用```{..}``` 包裹起来的内容。如果使用```$10^10$``` 表示的是$10^10$，而```$10^{10}$``` 才是$10^{10}$。同时，大括号还能消除二义性，如```x^5^6``` 将得到一个错误，必须使用大括号来界定^的结合性，如``` ${x^5}^6$ ```：${x^5}^6$或者```$x^{5^6}$ ```：$x^{5^6}$。
## 括号
### 小括号与方括号
&ensp;&ensp;&ensp;&ensp;使用原始的```( )``` ，```[ ]``` 即可，如```$(2+3)[4+4]$``` ： $(2+3)[4+4]$

&ensp;&ensp;&ensp;&ensp;使用\left(或\right)使符号大小与邻近的公式相适应（该语句适用于所有括号类型），如```$\left(\frac{x}{y}\right)$``` ：$\left(\frac{x}{y}\right)$
### 大括号
&ensp;&ensp;&ensp;&ensp;由于大括号```{}``` 被用于分组，因此需要使用```\{```和```\}```表示大括号，也可以使用```\lbrace``` 和```\rbrace```来表示。如```$\{a\*b\}:a\∗b$``` 或```$\lbrace a\*b\rbrace :a\*b$ ```表示$\{a\*b\}:a\∗b$。
### 尖括号
&ensp;&ensp;&ensp;&ensp;区分于小于号和大于号，使用```\langle 和\rangle``` 表示左尖括号和右尖括号。如```$\langle x \rangle$ ```表示：$\langle x \rangle$。
### 上取整
&ensp;&ensp;&ensp;&ensp;使用\lceil 和 \rceil 表示。 如，```$\lceil x \rceil$```：$\lceil x \rceil$。
### 下取整
&ensp;&ensp;&ensp;&ensp;使用\lfloor 和 \rfloor 表示。如，```$\lfloor x \rfloor$```：$\lfloor x \rfloor$。
## 求和与积分
### 求和
&ensp;&ensp;&ensp;&ensp;```\sum``` 用来表示求和符号，其下标表示求和下限，上标表示上限。如:

&ensp;&ensp;&ensp;&ensp;```$\sum_{r=1}^n$```表示：$\sum_{r=1}^n$。

&ensp;&ensp;&ensp;&ensp;```$$\sum_{r=1}^n$$```表示：$$\sum_{r=1}^n$$
### 积分
&ensp;&ensp;&ensp;&ensp;\int 用来表示积分符号，同样地，其上下标表示积分的上下限。如，```$\int_{r=1}^\infty$```：$\int_{r=1}^\infty$。
  多重积分同样使用 int ，通过 i 的数量表示积分导数：
 ``` $\iint$``` ： $\iint$
  ```$\iiint$``` ：$\iiint$
  ```$\iiiint$``` ： $\iiiint$
### 连乘
&ensp;&ensp;&ensp;&ensp;```$\prod {a+b}$```，输出：$\prod {a+b}$。

&ensp;&ensp;&ensp;&ensp;```$\prod_{i=1}^{K}$```，输出：$\prod_{i=1}^{K}$。

&ensp;&ensp;&ensp;&ensp;```$$\prod_{i=1}^{K}$$```，输出：$$\prod_{i=1}^{K}$$。
### 其他
与此类似的符号还有，

&ensp;&ensp;&ensp;&ensp;```$\prod$``` ：$\prod$ 

&ensp;&ensp;&ensp;&ensp;```$\bigcup$``` ：$\bigcup$ 

&ensp;&ensp;&ensp;&ensp;```$\bigcap$``` ：$\bigcap$

&ensp;&ensp;&ensp;&ensp;```$arg\,\max_{c_k}$```：$arg\,\max_{c_k}$

&ensp;&ensp;&ensp;&ensp;```$arg\,\min_{c_k}$```：$arg\,\min_{c_k}$

&ensp;&ensp;&ensp;&ensp;```$\mathop {argmin}_{c_k}$```：$\mathop {argmin}_{c_k}$

&ensp;&ensp;&ensp;&ensp; ```$\mathop {argmax}_{c_k}$```：$\mathop {argmax}_{c_k}$

&ensp;&ensp;&ensp;&ensp;```$\max_{c_k}$```： $\max_{c_k}$

&ensp;&ensp;&ensp;&ensp;```$\min_{c_k}$```： $\min_{c_k}$

## 分式与根式
### 分式
* 第一种，使用```\frac ab```，```\frac```作用于其后的两个组```a``` ，```b``` ，结果为$\frac ab$。如果你的分子或分母不是单个字符，请使用{..}来分组，比如```$\frac {a+c+1}{b+c+2}$```表示$\frac {a+c+1}{b+c+2}$。
* 第二种，使用\over来分隔一个组的前后两部分，如```${a+1\over b+1}$```：${a+1\over b+1}$
### 连分数
&ensp;&ensp;&ensp;&ensp;
### 根式
&ensp;&ensp;&ensp;&ensp;
## 多行表达式
&ensp;&ensp;&ensp;&ensp;
### 分类表达式
&ensp;&ensp;&ensp;&ensp;
### 多行表达式
&ensp;&ensp;&ensp;&ensp;
### 方程组
&ensp;&ensp;&ensp;&ensp;
## 特殊函数与符号
&ensp;&ensp;&ensp;&ensp;
### 三角函数
&ensp;&ensp;&ensp;&ensp;
### 比较函数
&ensp;&ensp;&ensp;&ensp;
### 集合关系与运算
&ensp;&ensp;&ensp;&ensp;
### 排列
&ensp;&ensp;&ensp;&ensp;
### 箭头
&ensp;&ensp;&ensp;&ensp;
### 逻辑运算符
&ensp;&ensp;&ensp;&ensp;
### 操作符
&ensp;&ensp;&ensp;&ensp;
### 等于
&ensp;&ensp;&ensp;&ensp;
### 范围
&ensp;&ensp;&ensp;&ensp;
### 模运算
&ensp;&ensp;&ensp;&ensp;
### 点
&ensp;&ensp;&ensp;&ensp;
## 顶部符号
&ensp;&ensp;&ensp;&ensp;对于单字符，\hat x ：$\hat x$

&ensp;&ensp;&ensp;&ensp;多字符可以使用\widehat {xy} ：$\widehat {xy}$

&ensp;&ensp;&ensp;&ensp;(\overline x ): $\overline x$

&ensp;&ensp;&ensp;&ensp;矢量(\vec x): $\vec x$

&ensp;&ensp;&ensp;&ensp;向量(\overrightarrow {xy} ):$\overrightarrow {xy}$

&ensp;&ensp;&ensp;&ensp;(\dot x ): $\dot x$

&ensp;&ensp;&ensp;&ensp;(\ddot x ):$\ddot x$

&ensp;&ensp;&ensp;&ensp;(\dot {\dot x} ):$\dot{\dot x}$

## 表格
&ensp;&ensp;&ensp;&ensp;
## 矩阵
&ensp;&ensp;&ensp;&ensp;
### 基本内容
&ensp;&ensp;&ensp;&ensp;
### 括号
&ensp;&ensp;&ensp;&ensp;
### 元素省略
&ensp;&ensp;&ensp;&ensp;
### 增广矩阵
&ensp;&ensp;&ensp;&ensp;
## 公式标记与引用
&ensp;&ensp;&ensp;&ensp;
## 字体
&ensp;&ensp;&ensp;&ensp;