# Markdown数学公式

***
始于2024.7.2晚
[整理来源：CSDN](https://blog.csdn.net/m0_37769093/article/details/107732606)
[补充内容网址：Markdown 数学公式指导手册](https://freeopen.github.io/mathjax/#ba-yi-xie-te-shu-de-zhu-yi-shi-xiang)
***

Markdown的行内公式表示为`$公式$`，行间公式表示为`$$公式$$`

***

## 常用符号标注

### 上下标

数学符号|实际效果|语法
---|---|---
向量                   |$\vec{a}$|`\vec{a}`\
平均值                 |$\overline{a}$|`\overline{a}`
估计值                 |$\widehat{a}$|`\widehat{a}`
颚化符号 等价无穷小     |$widetilde{a}$|`\widetilde{a}`
一阶导数               |$\dot{a}$|`\dot{a}`
二阶导数               |$\ddot{a}$|`\ddot{a}`
-|$\check{a}$|`\check{a}`
-|$\breve{a}$|`\breve{a}`
-|$\grave{a}$|`\grave{a}`
-|$\acute{a}$|`\acute{a}`
-|$\stackrel{x}{y}$|`\stackrel{x}{y}`
-|$\overset{z}{y}$|`\overset{z}{y}`
-|$\underset{x}{y}$|`\underset{x}{y}`
上标|$x^y$|`x^y`
下标|$x_y$|`x_y`
复杂上下标|${^1_2}\bigotimes{^3_4}$|`{^1_2}\bigotimes{^3_4}`

### 分式

实际效果|语法
---|---
1/2|`1/2`
$\frac{1}{2}$|`\frac{1}{2}`

### 省略号

`\cdots`，即$\cdots$

## 复杂数学符号

形式|实际效果|语法
---|---|---
1.求和|$y = \sum_{i=1}^{n}{x_i}$|`y = \sum_{i=1}^{n}{x_i}`
-|$y=\sum^{x \to \infty}_{y \to 0}{\frac{x}{y}}$|`y=\sum^{x \to \infty}_{y \to 0}{\frac{x}{y}}`
2.极限|$\lim^{x \to \infty}_{y \to 0}{\frac{x}{y}}$|`\lim^{x \to \infty}_{y \to 0}{\frac{x}{y}}`
-|$\lim^{x \to \infty}_{y \to 0}{\frac{x}{y}}$|`\lim^{x \to \infty}_{y \to 0}{\frac{x}{y}}`
3.开方|$\sqrt x$|`sqrt x`
-|$\sqrt[3]{x+y}$|`\sqrt[3]{x+y}` 
4.微积分|$\int^{\infty}_{0}{xdx}$|`\int^{\infty}_{0}{xdx}`
-|$\iint$|`\iint`
-|$\iiint$|`\iiint`
-|$\oint$|`\oint`
-|$\dfrac{\partial f}{\partial x}$|`\dfrac{\partial f}{\partial x}`
-|$\frac{\partial x^2}{\partial y^2}$|`\frac{\partial x^2}{\partial y^2}`
-|$\frac{\partial f(x,y)}{\partial x} \vert _{x=0}$|`\frac{\partial f(x,y)}{\partial x} \vert _{x=0}`
-|$y{\prime}x$|`y{\prime}x`
-|$\nabla$|`\nabla`
-|$\infty$|`\infty`
5.向量|$\overrightarrow{xy}$|`\overrightarrow{xy}`
矢量|$\vec x$|`\vec x`
-|$\overline{xyz}$|`\overline{xyz}`
-|$\overline{x\overline{yz}}$|`overline{x\overline{yz}}`
-|$\underline{xyz}$|`\underline{xyz}`
6.累乘|$\prod_{n=1}^{99}{x_n}$|`\prod_{n=1}^{99}{x_n}`
-|$\prod_{n=1}^{99}{x_n}$|`\prod_{n=1}^{99}{x_n}`
7.箭头|$a \leftarrow b \rightarrow c \leftrightarrow d \Leftrightarrow e \rightleftharpoons f$|`a \leftarrow b \rightarrow c \leftrightarrow d \Leftrightarrow e \rightleftharpoons f`
-|$\longleftarrow b \longrightarrow c \Longleftrightarrow da⟵b⟶c⟺d	a \longleftarrow b \longrightarrow c \Longleftrightarrow d$|`\longleftarrow b \longrightarrow c \Longleftrightarrow da⟵b⟶c⟺d	a \longleftarrow b \longrightarrow c \Longleftrightarrow d`
-|$a \nearrow b \searrow c \nwarrow d \searrow e$|`a \nearrow b \searrow c \nwarrow d \searrow e`
-|$a \uparrow b \downarrow c \Uparrow d \Downarrow e$|`a \uparrow b \downarrow c \Uparrow d \Downarrow e`
-|$a \rightharpoonup b \rightharpoondown c \leftharpoonup d \leftharpoondown e$|`a \rightharpoonup b \rightharpoondown c \leftharpoonup d \leftharpoondown e`
8.逻辑运算符|$\forall a \exists b$|`\forall a \exists b`
-|$\lnot a \bigvee b \bigwedge$|`\lnot a \bigvee b \bigwedge`
-|$\because a \therefore b$|`\because a \therefore b`
9.集合符号|$X\cup Y \bigcup Z\cap W$|`X\cup Y \bigcup Z\cap W`
-|$X \subset Y \not\subset Z \subseteq W \not\subseteq UX⊂Y $|`X \subset Y \not\subset Z \subseteq W \not\subseteq UX⊂Y `
-|$\in d \notin e$|`\in d \notin e`
-|$\emptyset$|`\emptyset`
-|$\varnothing$|`\varnothing`
10.取整|$\lceil \frac{x}{2} \rceil$|`\lceil \frac{x}{2} \rceil`
-|$\lfloor x \rfloor$|`\lfloor x \rfloor`
11.括号|$\tbinom{n}{k}$|`tbinom{n}{k}`
-|$\binom{n}{k}$|`\binom{n}{k}`
-|$\dbinom{n}{k}$|`\dbinom{n}{k}`
-|${n\brace k}$|`{n\brace k}`
-|${n\choose k}$|`{n\choose k}`
-|${n\brack k}$|`{n\brack k}`
-|$\overbrace{1+2+\cdots+100}$|`overbrace{1+2+\cdots+100}`
-|$\underbrace{1+2+\cdots+100}$|`\underbrace{1+2+\cdots+100}`
-|$5050 \; \overbrace {1+2+⋯+100}$|`5050 \overbrace {1+2+⋯+100}`
12.矩阵|$\begin{matrix} 0 & 1 \\ 3 & 4 \\ \end{matrix}​$|`\begin{matrix} 0 & 1 \\ 3 & 4 \\ \end{matrix}​`
-|$\begin{pmatrix} 0 & 1 \\ 3 & 4 \\ \end{pmatrix}$|`\begin{pmatrix} 0 & 1 \\ 3 & 4 \\ \end{pmatrix}`
-|$\begin{vmatrix} 0 & 1 \\ 3 & 4 \\ \end{vmatrix}$|`\begin{vmatrix} 0 & 1 \\ 3 & 4 \\ \end{vmatrix}`
-|$\begin{Vmatrix} 0 & 1 \\ 3 & 4 \\ \end{Vmatrix}$|`\begin{Vmatrix} 0 & 1 \\ 3 & 4 \\ \end{Vmatrix}`
-|$\begin{bmatrix} 0 & 1 \\ 3 & 4 \\ \end{bmatrix}$|`\begin{bmatrix} 0 & 1 \\ 3 & 4 \\ \end{bmatrix}`
-|$\begin{Bmatrix} 0 & 1 \\ 3 & 4 \\ \end{Bmatrix}$|`\begin{Bmatrix} 0 & 1 \\ 3 & 4 \\ \end{Bmatrix}`

## 关系运算符

实际效果|语法
---|---
$\neq$|`\neq`
$\leq$|`\leq`
$\geq$|`\geq`
$\approx$|`\approx`
$\not\lt$|`\not\lt`
$\gt$|`\gt`
$\gg$|`\gg`
$\lll$|`\lll`
$\pm$|`\pm`
$\times$|`\times`
$\div$|`\div`
$\mid$|`\mid`
$\ast$|`\ast`
$\angle$|`\angle`
$\bot$|`\bot`
$\odot and\bigodot$|`\odot and\bigodot`
$\otimes and \bigotimes$|`\otimes and \bigotimes`

## 三角函数

实际效果|表示
---|---
$\sin 30^\circ$|`\sin 30^\circ`
$\cos 30^\circ$|`\cos 30^\circ`
$\tan30^\circ$|`\tan30^\circ`

## 对数函数

实际效果|表示
---|---
$\ln 2$|`\ln 2`
$\log_2 8$|`\log_2 8`.
$\lg 10$|`\lg 10`

## 大型关系式

### 矩阵


    % 可将 [] 换成 () 或 ||...
    \left[   
    \begin{array}{ccc|c}
        \psi(x) & g(x)   & \cdots  & a_{1n} \\
        \hline
        a_{21}  & a_{22} & \dots   & a_{2n} \\
        \vdots  & \vdots & \ddots  & \vdots \\
        a_{n1}  & a_{n2} & ...     & a_{nn}
    \end{array}
    \right]

% 可将 [] 换成 () 或 ||...
$$
\left[   
\begin{array}{ccc|c}
    \psi(x) & g(x)   & \cdots  & a_{1n} \\
    \hline
    a_{21}  & a_{22} & \dots   & a_{2n} \\
    \vdots  & \vdots & \ddots  & \vdots \\
    a_{n1}  & a_{n2} & ...     & a_{nn}
\end{array}
\right]
$$

    $$
    \begin{bmatrix}
        1 & x_{0} &...      & x_{0}^{n} \\
        1 & x_{1} &...  	 & x_{1}^{n} \\
        &       & \cdots  & \\
        1 & x_{n} & \dots   & x_{n}^{n}
    \end{bmatrix}
    \begin{bmatrix}
        a_{0}\\ a_{1}\\ ...\\ a_{n}
    \end{bmatrix}=
    \begin{bmatrix}
        y_{0}\\ y_{1}\\ ...\\ y_{n}
    \end{bmatrix}
    $$

$$
\begin{bmatrix}
    1 & x_{0} &...      & x_{0}^{n} \\
    1 & x_{1} &...  	 & x_{1}^{n} \\
    &       & \cdots  & \\
    1 & x_{n} & \dots   & x_{n}^{n}
\end{bmatrix}
\begin{bmatrix}
    a_{0}\\ a_{1}\\ ...\\ a_{n}
\end{bmatrix}=
\begin{bmatrix}
    y_{0}\\ y_{1}\\ ...\\ y_{n}
\end{bmatrix}
$$

### 方程式

    $$
    \begin{cases}
        a_{0}+a_{1}x_{0}+...+a_{n}x_{0}^{n}=y_{0} \\
        a_{0}+a_{1}x_{1}+...+a_{n}x_{1}^{n}=y_{1} \\
        \cdots\\
        a_{0}+a_{1}x_{n}+...+a_{n}x_{n}^{n}=y_{n}
    \end{cases}
    $$

$$
\begin{cases}
    a_{0}+a_{1}x_{0}+...+a_{n}x_{0}^{n}=y_{0} \\
    a_{0}+a_{1}x_{1}+...+a_{n}x_{1}^{n}=y_{1} \\
    \cdots\\
    a_{0}+a_{1}x_{n}+...+a_{n}x_{n}^{n}=y_{n}
\end{cases}
$$

### 等式

使用 `\&` 使 `=` 左对齐

    $$
    \begin{aligned}
        (f,K^{'}_{x}y+K^{''}_{x}y)_{F}
        &=(f^{'}+f^{''},K^{'}_{x}y+K^{''}_{x}y)_{F}\\
        &=(f^{'},K^{'}_{x}y)_{F}+(f^{''},K^{''}_{x}y)_{F}+(f^{'},K^{''}_{x}y)_{F}+(f^{''},K^{'}_{x}y)_{F}\\
        &=(f^{'},K^{'}_{x}y)_{F}+(f^{''},K^{''}_{x}y)_{F}\\
        &=(f^{'}(x),y)_{Y}+(f^{''}(x),y)_{Y}\\
        &=(f^{'}(x)+f^{''}(x),y)_{Y}\\
        &=(f(x),y)_{Y}\\
        &=(f,K_{x}y)_{F}
    \end{aligned}
    $$

使用 `\&` 使 `=` 左对齐

$$
\begin{aligned}
    (f,K^{'}_{x}y+K^{''}_{x}y)_{F}
    &=(f^{'}+f^{''},K^{'}_{x}y+K^{''}_{x}y)_{F}\\
    &=(f^{'},K^{'}_{x}y)_{F}+(f^{''},K^{''}_{x}y)_{F}+(f^{'},K^{''}_{x}y)_{F}+(f^{''},K^{'}_{x}y)_{F}\\
    &=(f^{'},K^{'}_{x}y)_{F}+(f^{''},K^{''}_{x}y)_{F}\\
    &=(f^{'}(x),y)_{Y}+(f^{''}(x),y)_{Y}\\
    &=(f^{'}(x)+f^{''}(x),y)_{Y}\\
    &=(f(x),y)_{Y}\\
    &=(f,K_{x}y)_{F}
\end{aligned}
$$

## 希腊字母

用`\英文名`来表示，其中，英文名首字母大写表示字母大写

## 注意

### 字体变换

语法|说明|显示
---|---|---
\rm|罗马体|$S a m p l e \rm{Sample}Sample$
\it|意大利体|$S a m p l e \it{Sample}Sample$
\bf|粗体|$S a m p l e \bf{Sample}Sample$
\sf|等线体|$S a m p l e \sf{Sample}Sample$
\tt|打字机体|$S a m p l e \tt{Sample}Sample$
\frak|旧德式字体|$S a m p l e \frak{Sample}Sample$
\cal|花体|$Sample\mathcal{sample}Sample$
\Bbb|黑板粗体|$S A M P L E \Bbb{SAMPLE}SAMPLE$
\mit|数学斜体|
\scr|手写体|

### 在字符中添加空格

有四种宽度的空格

语法|显示
---|---
`\,`|$a \, b$
`\;`|$a \; b$
`\quad`|$a \quad b$
`\qquad`|$a \qquad b$

### 添加注释文字

即在欲添加文字的行的末尾加以`\text{文字}`

    $$
    f(n)= \begin{cases}
    n/2, & \text {if $n$ is even} \\
    3n+1, & \text{if $n$ is odd}
    \end{cases}
    $$

$$
f(n)= \begin{cases}
n/2, & \text {if $n$ is even} \\
3n+1, & \text{if $n$ is odd}
\end{cases}
$$

### 删除线

首先需要使用`require{cancel}`来允许删除线的显示
后使用`\cancel{字符}`、`\bcancel{字符}`、`\xcancel{字符}`、`\cancelto{字符}`添加删除线

    $$
    \require{cancel}\begin{array}{rl}
    \verb|y+\cancel{x}| & y+\cancel{x}\\
    \verb|\cancel{y+x}| & \cancel{y+x}\\
    \verb|y+\bcancel{x}| & y+\bcancel{x}\\
    \verb|y+\xcancel{x}| & y+\xcancel{x}\\
    \verb|y+\cancelto{0}{x}| & y+\cancelto{0}{x}\\
    \verb+\frac{1\cancel9}{\cancel95} = \frac15+& \frac{1\cancel9}{\cancel95} = \frac15 \\
    \end{array}
    $$

$$
\require{cancel}\begin{array}{rl}
\verb|y+\cancel{x}| & y+\cancel{x}\\
\verb|\cancel{y+x}| & \cancel{y+x}\\
\verb|y+\bcancel{x}| & y+\bcancel{x}\\
\verb|y+\xcancel{x}| & y+\xcancel{x}\\
\verb|y+\cancelto{0}{x}| & y+\cancelto{0}{x}\\
\verb+\frac{1\cancel9}{\cancel95} = \frac15+& \frac{1\cancel9}{\cancel95} = \frac15 \\
\end{array}
$$
以上错误未知解决方法
