---
date:
    created: 2024-11-14
    updated: 2024-11-18
readtime: 45
categories:
    - Tools
tags:
    - Markdown
---

# Markdown常见公式

Markdown常见的公式以及符号汇总摘录。
<!-- more -->

!!! warning "注意"
    这里是对来自CSDN的[史上最全Markdown公式、符号总结！！！](https://blog.csdn.net/weixin_42782150/article/details/104878759)的摘录与修改，这篇文章非常好，基本涵盖了所有的Mk数学公式和符号，侵权联系我删除。

一般公式分为两种形式，行内公式和行间公式。行内公式是在公式代码块的前后均添加一个`$` ；行间公式则是在公式代码块的前后均添加两个`$$` 。

```test
$ \Gamma(z) = \int_0^\infty t^{z-1}e^{-t}dt\,. $
$$\Gamma(z) = \int_0^\infty t^{z-1}e^{-t}dt\,.$$
```

***

公式排列：一般使用`\binom{a}{b}`或者`{a \choose b}`实现对 $a$ , $b$ 两个公式的排列。

```test
\binom{n+1}{2k} {n+1 \choose 2k}
```

$$
\binom{n+1}{2k} {n+1 \choose 2k}
$$

***

## 向量公式

向量表示：使用`\mathbf{x}`来表示向量$\mathbf{x}$。

```test
f(\mathbf{x})=\mathbf{w}^T\mathbf{x}
```

$$
f(\mathbf{x})=\mathbf{w}^T\mathbf{x}
$$

## 分段函数

定义函数的时候经常需要分情况给出表达式，使用 `{…`。其中：

（1）使用`\`来分隔分组；

（2）使用`&`来指示需要对齐的位置；

（3）使用`\ + 空格`来表示空格；

（4）如果要使分类之间的垂直间隔变大，可以使用`\[2ex]`代替`\`来分隔不同的情况。（`3ex`,`4ex` 也可以用，`1ex` 相当于原始距离）。

```test
y=
\begin{cases}
-x,\quad x\leq 0\\
x, \quad x>0
\end{cases}
\tag{1}
```

$$
y=
\begin{cases}
-x,\quad x\leq 0\\
x, \quad x>0
\end{cases}
\tag{1}
$$

使用`\[2ex]`代替`\`使分组的垂直间隔增大：

```test
y=
\begin{cases}
-x,\quad x\leq 0 \\[2ex]
x, \quad x>0
\end{cases}
\tag{1}
```

$$
y=
\begin{cases}
-x,\quad x\leq 0 \\[2ex]
x, \quad x>0
\end{cases}
\tag{1}
$$

## 方程组

```test
\left\{ 
\begin{array}{c}
    a_1x+b_1y+c_1z=d_1 \\ 
    a_2x+b_2y+c_2z=d_2 \\ 
    a_3x+b_3y+c_3z=d_3
\end{array}
\right.
```

$$
\left\{
\begin{array}{c}
    a_1x+b_1y+c_1z=d_1 \\
    a_2x+b_2y+c_2z=d_2 \\
    a_3x+b_3y+c_3z=d_3
\end{array}
\right.
$$

## 均方误差

```test
J(\theta) = \frac{1}{2m}\sum_{i = 0} ^m(y^i - h_\theta (x^i))^2
```

$$
J(\theta) = \frac{1}{2m}\sum_{i = 0} ^m(y^i - h_\theta (x^i))^2
$$

## 批量梯度下降

```test
\frac{\partial J(\theta)}{\partial\theta_j} = -\frac1m\sum_{i=0}^m(y^i-h_\theta(x^i))x^i_j
```

$$
\frac{\partial J(\theta)}{\partial\theta_j} = -\frac1m\sum_{i=0}^m(y^i-h_\theta(x^i))x^i_j
$$

## case环境的使用

```test
a = 
\begin{cases}
\int x\,\mathrm{d} x\\
b^2
\end{cases}
```

$$
a =
\begin{cases}
\int x\,\mathrm{d} x\\
b^2
\end{cases}
$$

## 带方框的等式

```test
\begin{aligned}
\boxed{x^2+y^2=z^2}
\end{aligned}
```

$$
\begin{aligned}
\boxed{x^2+y^2=z^2}
\end{aligned}
$$

## 最大（最小）操作符

```test
\begin{gathered}
\operatorname{arg\,max}_a f(a) 
 = \operatorname*{arg\,max}_b f(b) \\
 \operatorname{arg\,min}_c f(c) 
 = \operatorname*{arg\,min}_d f(d)
\end{gathered}
```

$$
\begin{gathered}
\operatorname{arg\,max}_a f(a)
 = \operatorname*{arg\,max}_b f(b) \\
 \operatorname{arg\,min}_c f(c)
 = \operatorname*{arg\,min}_d f(d)
\end{gathered}
$$

## 求极限

```test
\begin{aligned}
  \lim_{a\to \infty} \tfrac{1}{a}
\end{aligned}

\begin{aligned}
   \lim\nolimits_{a\to \infty} \tfrac{1}{a}
\end{aligned}
```

$$
\begin{aligned}
  \lim_{a\to \infty} \tfrac{1}{a}
\end{aligned}
$$

$$
\begin{aligned}
   \lim\nolimits_{a\to \infty} \tfrac{1}{a}
\end{aligned}
$$

## 求积分

```test
\begin{aligned}
   \int_a^b x^2  \mathrm{d} x
\end{aligned}

\begin{aligned}
   \int\limits_a^b x^2  \mathrm{d} x
\end{aligned}
```

$$
\begin{aligned}
   \int_a^b x^2  \mathrm{d} x
\end{aligned}
$$

$$
\begin{aligned}
   \int\limits_a^b x^2  \mathrm{d} x
\end{aligned}
$$

## 多行表达式

有时候需要将一行公式多行进行显示，其中`\begin{aligned}`表示开始方程，`\end{equation}`表示方程结束

使用`\\`表示公式换行。`\begin{gather}`表示环境设置，`&`表示对齐的位置。

```test
\begin{aligned}
J(\mathbf{w})&=\frac{1}{2m}\sum_{i=1}^m(f(\mathbf{x_i})-y_i)^2\\
&=\frac{1}{2m}\sum_{i=1}^m [f(\mathbf{x_i})]^2-2f(\mathbf{x_i)}y_i+y_i^2
\end{aligned}
```

$$
\begin{aligned}
J(\mathbf{w})&=\frac{1}{2m}\sum_{i=1}^m(f(\mathbf{x_i})-y_i)^2\\
&=\frac{1}{2m}\sum_{i=1}^m [f(\mathbf{x_i})]^2-2f(\mathbf{x_i)}y_i+y_i^2
\end{aligned}
$$

常见公式环境

|  环境名称  |       释义       |
| :--------: | :--------------: |
|  `align`   | 最基本的对齐环境 |
| `multline` |    非对齐环境    |
|  `gather`  | 无对齐的连续方程 |

> gathered 允许多行（多组）方程式在彼此之下设置并分配单个方程式编号
>
> split 与 align * 类似，但在另一个显示的数学环境中使用
>
> aligned 与 align 类似，可以在其他数学环境中使用
>
> alignedat 与 alignat 类似，同样需要一个额外的参数来指定要设置的方程列数
>
> 如果各个方程需要在某个字符处对齐（如等号对齐），只需在所有要对齐的字符前加上`&`符号

```test
\begin{aligned}
 \left.\begin{aligned}
        B'&=-\partial \times E,\\
        E'&=\partial \times B - 4\pi j,
       \end{aligned}
 \right\}
 \qquad \text{Maxwell's equations}
\end{aligned}
```

$$
\begin{aligned}
 \left.\begin{aligned}
        B'&=-\partial \times E,\\
        E'&=\partial \times B - 4\pi j,
       \end{aligned}
 \right\}
 \qquad \text{Maxwell's equations}
\end{aligned}
$$

```test
\begin{aligned}
 \sigma_1 &= x + y  &\quad \sigma_2 &= \frac{x}{y} \\
 \sigma_1' &= \frac{\partial x + y}{\partial x} & \sigma_2' 
    &= \frac{\partial \frac{x}{y}}{\partial x}
\end{aligned}
```

$$
\begin{aligned}
 \sigma_1 &= x + y  &\quad \sigma_2 &= \frac{x}{y} \\
 \sigma_1' &= \frac{\partial x + y}{\partial x} & \sigma_2'
    &= \frac{\partial \frac{x}{y}}{\partial x}
\end{aligned}
$$

```test
\begin{aligned}
a_n&=\frac{1}{\pi}\int\limits_{-\pi}^{\pi}f(x)\cos nx\,\mathrm{d}x\\
&=\frac{1}{\pi}\int\limits_{-\pi}^{\pi}x^2\cos nx\,\mathrm{d}x\\[6pt]
\end{aligned}
```

$$
\begin{aligned}
a_n&=\frac{1}{\pi}\int\limits_{-\pi}^{\pi}f(x)\cos nx\,\mathrm{d}x\\
&=\frac{1}{\pi}\int\limits_{-\pi}^{\pi}x^2\cos nx\,\mathrm{d}x\\[6pt]
\end{aligned}
$$

## 公式编辑的编号设置

|     符号     |                         功能                         |
| :----------: | :--------------------------------------------------: |
| `tag{标号}`  | 公式宏包序号设置命令，可用于带星号公式环境中的公式行 |
| `tag*{标号}` |        作用与tag相同，只是标号两侧没有圆括号         |

```test
x^2+y^2=z^2 \tag{1$'$}
```

$$
x^2+y^2=z^2 \tag{1$'$}
$$

```test
x^4+y^4=z^4 \tag{*}
```

$$
x^4+y^4=z^4 \tag{*}
$$

```test
x^5+y^5=z^5 \tag*{*}
```

$$
x^5+y^5=z^5 \tag*{*}
$$

```test
x^6+y^6=z^6 \tag{1-1}
```

$$
x^6+y^6=z^6 \tag{1-1}
$$

## 矩阵

```test
\begin{pmatrix}1 & 2 \\ 3 &4\\ \end{pmatrix}
```

$$
\begin{pmatrix}1 & 2 \\ 3 &4\\ \end{pmatrix}
$$

```test
\begin{bmatrix}1 & 2 \\ 3 & 4\\ \end{bmatrix}
```

$$
\begin{bmatrix}1 & 2 \\ 3 & 4\\ \end{bmatrix}
$$

```test
\begin{Bmatrix}1 &2 \\ 3 & 4\\ \end{Bmatrix}
```

$$
\begin{Bmatrix}1 &2 \\ 3 & 4\\ \end{Bmatrix}
$$

```test
\begin{vmatrix}1 &2 \\ 3 &4\\ \end{vmatrix}
```

$$
\begin{vmatrix}1 &2 \\ 3 &4\\ \end{vmatrix}
$$

```test
\begin{Vmatrix}1 &  2 \\ 3 &  4\\ \end{Vmatrix}
```

$$
\begin{Vmatrix}1 &  2 \\ 3 &  4\\ \end{Vmatrix}
$$

**元素省略**可以使用`\cdots`表示⋯，`\ddots`表示⋱，`\vdots`表示⋮，从而省略矩阵中的元素，如：

```test
\begin{pmatrix}
1&a_1&a_1^2&\cdots&a_1^n\\
1&a_2&a_2^2&\cdots&a_2^n\\
\vdots&\vdots&\vdots&\ddots&\vdots\\
1&a_m&a_m^2&\cdots&a_m^n\\
\end{pmatrix}
```

$$
\begin{pmatrix}
1&a_1&a_1^2&\cdots&a_1^n\\
1&a_2&a_2^2&\cdots&a_2^n\\
\vdots&\vdots&\vdots&\ddots&\vdots\\
1&a_m&a_m^2&\cdots&a_m^n\\
\end{pmatrix}
$$

1、不带括号的矩阵

```test
\begin{matrix}
1 & 2 & 3\\
4 & 5 & 6 \\
7 & 8 & 9
\end{matrix}
\tag{1}
```

$$
\begin{matrix}
1 & 2 & 3\\
4 & 5 & 6 \\
7 & 8 & 9
\end{matrix}
\tag{1}
$$

2、带小括号的矩阵

```test
\left(
\begin{matrix}
1 & 2 & 3\\
4 & 5 & 6 \\
7 & 8 & 9
\end{matrix}
\right)
\tag{2}
```

$$
\left(
\begin{matrix}
1 & 2 & 3\\
4 & 5 & 6 \\
7 & 8 & 9
\end{matrix}
\right)
\tag{2}
$$

3、带中括号的矩阵

```test
\left[
\begin{matrix}
1 & 2 & 3\\
4 & 5 & 6 \\
7 & 8 & 9
\end{matrix}
\right]
\tag{3}
```

$$
\left[
\begin{matrix}
1 & 2 & 3\\
4 & 5 & 6 \\
7 & 8 & 9
\end{matrix}
\right]
\tag{3}
$$

4、带大括号的矩阵

```test
\left\{
\begin{matrix}
1 & 2 & 3\\
4 & 5 & 6 \\
7 & 8 & 9
\end{matrix}
\right\}
\tag{4}
```

$$
\left\{
\begin{matrix}
1 & 2 & 3\\
4 & 5 & 6 \\
7 & 8 & 9
\end{matrix}
\right\}
\tag{4}
$$

5、带省略号的矩阵

```test
\left[
\begin{matrix}
a & b & \cdots & a\\
b & b & \cdots & b\\
\vdots & \vdots & \ddots & \vdots\\
c & c & \cdots & c
\end{matrix}
\right]
\tag{5}
```

$$
\left[
\begin{matrix}
a & b & \cdots & a\\
b & b & \cdots & b\\
\vdots & \vdots & \ddots & \vdots\\
c & c & \cdots & c
\end{matrix}
\right]
\tag{5}
$$

6、带横线/竖线分割的矩阵

```test
\left[
    \begin{array}{c|cc}
    1 & 2 & 3 \\ \hline
    4 & 5 & 6 \\
    7 & 8 & 9
    \end{array}
\right]
\tag{7}
```

$$
\left[
    \begin{array}{c|cc}
    1 & 2 & 3 \\ \hline
    4 & 5 & 6 \\
    7 & 8 & 9
    \end{array}
\right]
\tag{7}
$$

## 上下标符号

默认情况下，上、下标符号仅仅对下一个组起作用。一个组即单个字符或者使用`{...}`包裹起来的内容。

|                       数学算式                       |                    Markdown公式                    |     核心语法     |
| :--------------------------------------------------: | :------------------------------------------------: | :--------------: |
|                    $a_i,a_{pre}$                     |                   a_i , a_{pre}                    |   下标使用`_`    |
|                   $a^i , a^{pre}$                    |                   a^i , a^{pre}                    |   上标使用`^`    |
|                      $\bar{a}$                       |                      \bar{a}                       |                  |
|                     $\acute{a}$                      |                     \acute{a}                      |                  |
|                     $\breve{a}$                      |                     \breve{a}                      |                  |
|                     $\grave{a}$                      |                     \grave{a}                      |                  |
|                      $\dot{a}$                       |                      \dot{a}                       |                  |
|                      $\ddot{a}$                      |                      \ddot{a}                      |                  |
|                   $\dot {\dot x}$                    |                   \dot {\dot x}                    |                  |
|                      $\hat{a}$                       |                      \hat{a}                       |                  |
|                    $\widehat{xy}$                    |                    \widehat{xy}                    |  多字符可以使用  |
|                     $\check{a}$                      |                     \check{a}                      |                  |
|                     $\breve{a}$                      |                     \breve{a}                      |                  |
|                     $\tilde{a}$                      |                     \tilde{a}                      |                  |
|                      $\vec{a}$                       |                      \vec{a}                       |                  |
|                $\overrightarrow {xy}$                |                \overrightarrow {xy}                | 矢量使用`\vec{}` |
|              $\overline{a + b + c + d}$              |              \overline{a + b + c + d}              |       向量       |
|             $\underline{a + b + c + d}$              |             \underline{a + b + c + d}              |                  |
|             $\overbrace{a + b + c + d}$              |             \overbrace{a + b + c + d}              |                  |
|             $\underbrace{a + b + c + d}$             |             \underbrace{a + b + c + d}             |                  |
| $\overbrace{a + \underbrace{b + c}_{1.0} + d}^{2.0}$ | \overbrace{a + \underbrace{b + c}_{1.0} + d}^{2.0} |                  |

## 括号

小括号与方括号

（1）使用原始的`()` ， `[]`得到的括号大小是固定的，如`( 2 + 3 ) [ 4 + 4 ] ( 2 + 3 ) [ 4 + 4 ] ( 2 + 3 ) [ 4 + 4 ]`
（2）使用`\left`(或`\right`)可使括号大小与邻近的公式相适应（该语句适用于所有括号类型），如$( x y ) \left(\frac{x}{y}\right)$

|      数学算式      |           Markdown公式           | 核心语法 |
| :----------------: | :------------------------------: | :------: |
|      $( , )$       |              ( , )               |          |
|      $[ , ]$       |              [ , ]               |          |
|  $\lang, \rang $   | \lang, \rang 或 \langle, \rangle |          |
|  $\lvert, \rvert$  |          \lvert, \rvert          |          |
|  $\lVert, \rVert$  |          \lVert, \rVert          |          |
| $\lbrace, \rbrace$ |     \lbrace, \rbrace 或 {, }     |          |

增大括号的方法

|                           数学算式                           |                         Markdown公式                         | 核心语法 |
| :----------------------------------------------------------: | :----------------------------------------------------------: | :------: |
|                            $(x)$                             |                             (x)                              |          |
|                       $\big( x \big)$                        |                        \big( x \big)                         |          |
|                       $\Big( x \Big)$                        |                        \Big( x \Big)                         |          |
|                      $\bigg( x \bigg)$                       |                       \bigg( x \bigg)                        |          |
|                      $\Bigg( x \Bigg)$                       |                       \Bigg( x \Bigg)                        |          |
|      $\Bigg(\bigg(\Big(\big((x)\big)\Big)\bigg)\Bigg)$       |       \Bigg(\bigg(\Big(\big((x)\big)\Big)\bigg)\Bigg)        |          |
| $\Bigg \langle \bigg \langle \Big \langle\big\langle\langle x \rangle \big \rangle\Big\rangle\bigg\rangle\Bigg\rangle$ | \Bigg \langle \bigg \langle \Big \langle\big\langle\langle x \rangle \big \rangle\Big\rangle\bigg\rangle\Bigg\rangle |          |

## 分式与根式

分式的表达方法：

- 使用`\frac{a}{b}`表示分式，比如$\frac{a+c+1}{b+c+1}$
- 使用`\over`来分隔一个组的前后两部分，如${a+b}\over{b+1}$
- 连分数，使用`\cfrac`代替`\frac`或者`\over`，两个效果对比如下：

`\frac`表示连分式：

数学算式：

```test
x=a_0 + \frac{1^2}{a_ 1+\frac{2^2}{a_2+\frac{3^2}{a_3+ \frac{4^2}{a_4+...}}}}
```

$$
x=a_0 + \frac{1^2}{a_ 1+\frac{2^2}{a_2+\frac{3^2}{a_3+ \frac{4^2}{a_4+...}}}}
$$

`\cfrac`表示连分式：

数学算式：

```test
x=a_0 + \cfrac{1^2}{a_ 1+\cfrac{2^2}{a_2+\cfrac{3^2}{a_3+ \cfrac{4^2}{a_4+...}}}}
```

$$
x=a_0 + \cfrac{1^2}{a_ 1+\cfrac{2^2}{a_2+\cfrac{3^2}{a_3+ \cfrac{4^2}{a_4+...}}}}
$$

|    数学算式     | Markdown公式  |          核心语法           |
| :-------------: | :-----------: | :-------------------------: |
|  $\frac{a}{b}$  |  \frac{a}{b}  | 分数使用`\frac{分子}{分母}` |
| $a^i , a^{pre}$ | a^i , a^{pre} |         上标使用`^`         |

## 开放

|     数学算式      |  Markdown公式   |        核心语法         |
| :---------------: | :-------------: | :---------------------: |
|  $\sqrt{a + b}$   |  \sqrt{a + b}   |    开方使用`\sqrt{}`    |
| $\sqrt[n]{a + b}$ | \sqrt[n]{a + b} | 开n次方使用`\sqrt[n]{}` |

## 累加/累乘

|            数学算式            |         Markdown公式         |           核心语法            |
| :----------------------------: | :--------------------------: | :---------------------------: |
|     $\sum_{i = 0}^{n} x^2$     |     \sum_{i = 0}^{n} x^2     | 累加使用`\sum_{下标}^{上标}`  |
| $\prod_{i = 0}^{n}\frac{1}{x}$ | \prod_{i = 0}^{n}\frac{1}{x} | 累乘使用`\prod_{下标}^{上标}` |

## 三角函数

|  数学算式  | Markdown公式 | 核心语法 |
| :--------: | :----------: | :------: |
|   $\sin$   |     \sin     |   正弦   |
|  $\\cos$   |     \cos     |   余弦   |
|   $\tan$   |     \tan     |   正切   |
|   $\cot$   |     \cot     |   余切   |
|   $\sec$   |     \sec     |  反正弦  |
|   $\csc$   |     \csc     |  反余弦  |
|   $\bot$   |     \bot     |   垂直   |
|  $\angle$  |    \angle    |   夹角   |
| $40^\circ$ |   40^\circ   |   度数   |

## 对数函数

|    数学算式    | Markdown公式 |           核心语法            |
| :------------: | :----------: | :---------------------------: |
|  $\ln{a + b}$  |  \ln{a + b}  | 以e为底，对数函数使用`\ln{}`  |
| $\log_{a}^{b}$ | \log_{a}^{b} |  对数函数使用`\log_{a}^{b}`   |
|  $\lg{a + b}$  |  \lg{a + b}  | 以10为底，对数函数使用`\ln{}` |

## 二元运算符

|      数学算式      |   Markdown公式   |  核心语法  |
| :----------------: | :--------------: | :--------: |
|       $\pm$        |       \pm        |   正负号   |
|       $\mp$        |       \mp        |   负正号   |
|      $\times$      |      \times      |    乘号    |
|       $\div$       |       \div       |    除号    |
|       $\ast$       |       \ast       |    星号    |
|      $\star$       |      \star       |            |
|       $\mid$       |       \mid       |    竖线    |
|      $\nmid$       |      \nmid       |            |
|      $\circ$       |      \circ       |    圆圈    |
|     $\bullet$      |     \bullet      |            |
|      $\cdot$       |      \cdot       |   **点**   |
|       $\wr$        |       \wr        |            |
|     $\diamond$     |     \diamond     |            |
|     $\Diamond$     |     \Diamond     |            |
|    $\triangle$     |    \triangle     |            |
|  $\bigtriangleup$  |  \bigtriangleup  |            |
| $\bigtriangledown$ | \bigtriangledown |            |
|  $\triangleleft$   |  \triangleleft   |            |
|  $\triangleright$  |  \triangleright  |            |
|       $\lhd$       |       \lhd       |            |
|       $\rhd$       |       \rhd       |            |
|      $\unlhd$      |      \unlhd      |            |
|      $\unrhd$      |      \unrhd      |            |
|      $\circ$       |      \circ       |            |
|     $\bigcirc$     |     \bigcirc     |            |
|      $\odot$       |      \odot       |            |
|     $\bigodot$     |     \bigodot     |    点积    |
|     $\oslash$      |     \oslash      |            |
|     $\ominus$      |     \ominus      |            |
|     $\otimes$      |     \otimes      |            |
|    $\bigotimes$    |    \bigotimes    | 克罗内克积 |
|      $\oplus$      |      \oplus      |            |
|    $\bigoplus$     |    \bigoplus     |    异或    |
|     $\dagger$      |     \dagger      |            |
|     $\ddagger$     |     \ddagger     |            |
|      $\amalg$      |      \amalg      |            |

## 关系符号

|  数学算式   | Markdown公式 | 核心语法 |
| :---------: | :----------: | :------: |
|   $\leq$    |     \leq     |          |
|   $\geq$    |     \geq     |          |
|  $\equiv$   |    \equiv    |          |
|  $\models$  |   \models    |          |
|   $\prec$   |    \prec     |          |
|   $\succ$   |    \succ     |          |
|   $\sim$    |     \sim     |          |
|   $\perp$   |    \perp     |          |
|  $\preceq$  |   \preceq    |          |
|  $\succeq$  |   \succeq    |          |
|  $\simeq$   |    \simeq    |          |
|   $\mid$    |     \mid     |          |
|    $\ll$    |     \ll      |          |
|    $\gg$    |     \gg      |          |
|  $\asymp$   |    \asymp    |          |
| $\parallel$ |  \parallel   |          |
|  $\approx$  |   \approx    |          |
|   $\cong$   |    \cong     |          |
|   $\neq$    |     \neq     |  不等于  |
|  $\doteq$   |    \doteq    |          |
|  $\propto$  |   \propto    |          |
|  $\bowtie$  |   \bowtie    |          |
|   $\Join$   |    \Join     |          |
|  $\smile$   |    \smile    |          |
|  $\frown$   |    \frown    |          |
|  $\vdash$   |    \vdash    |          |
|  $\dashv$   |    \dashv    |          |

## 极限

|           数学算式            |        Markdown公式         |        核心语法         |
| :---------------------------: | :-------------------------: | :---------------------: |
|            $\lim$             |            \lim             |     极限使用`\lim`      |
|         $\rightarrow$         |         \rightarrow         | 趋向于使用`\rightarrow` |
|           $\infty$            |           \infty            |    无穷使用`\infty`     |
| $\lim_{n\rightarrow+\infty}n$ | \lim_{n\rightarrow+\infty}n |                         |

## 向量

|    数学算式     | Markdown公式  |       核心语法       |
| :-------------: | :-----------: | :------------------: |
|    $\vec{a}$    |    \vec{a}    |  向量使用`\vec{a}`   |
| $J(\mathbf{w})$ | J(\mathbf{w}) | 向量使用`\mathbf{w}` |

## 模运算

模运算使用`\pmod`来表示。示例如下：

```test
$a \equiv b \pmod n$
```

$$
a \equiv b \pmod n
$$

## 箭头

|       数学算式        |    Markdown公式     |
| :-------------------: | :-----------------: |
|      $\uparrow$       |      \uparrow       |
|     $\downarrow$      |     \downarrow      |
|    $\updownarrow$     |    \updownarrow     |
|      $\Uparrow$       |      \Uparrow       |
|     $\Downarrow$      |     \Downarrow      |
|    $\Updownarrow$     |    \Updownarrow     |
|     $\rightarrow$     |     \rightarrow     |
|     $\leftarrow$      |     \leftarrow      |
|   $\leftrightarrow$   |   \leftrightarrow   |
|     $\Rightarrow$     |     \Rightarrow     |
|     $\Leftarrow$      |     \Leftarrow      |
|   $\Leftrightarrow$   |   \Leftrightarrow   |
|   $\longrightarrow$   |   \longrightarrow   |
|   $\longleftarrow$    |   \longleftarrow    |
| $\longleftrightarrow$ | \longleftrightarrow |
|   $\Longrightarrow$   |   \Longrightarrow   |
|   $\Longleftarrow$    |   \Longleftarrow    |
|       $\mapsto$       |       \mapsto       |
|     $\longmapsto$     |     \longmapsto     |
|   $\hookleftarrow$    |   \hookleftarrow    |
|   $\hookrightarrow$   |   \hookrightarrow   |
|   $\rightharpoonup$   |   \rightharpoonup   |
|  $\leftharpoondown$   |  \leftharpoondown   |
| $\rightleftharpoons$  | \rightleftharpoons  |
|   $\leftharpoonup$    |   \leftharpoonup    |
|  $\rightharpoondown$  |  \rightharpoondown  |
|      $\leadsto$       |      \leadsto       |
|      $\nearrow$       |      \nearrow       |
|      $\searrow$       |      \searrow       |
|      $\swarrow$       |      \swarrow       |
|      $\nwarrow$       |      \nwarrow       |

## 集合

|   数学算式    | Markdown公式 | 核心语法 |
| :-----------: | :----------: | :------: |
|  $\emptyset$  |  \emptyset   |   空集   |
| $\varnothing$ | \varnothing  |    空    |
|     $\in$     |     \in      |   属于   |
|     $\ni$     |     \ni      |          |
|   $\notin$    |    \notin    |  不属于  |
|   $\subset$   |   \subset    |   子集   |
|   $\supset$   |   \supset    |   父集   |
| $\not\subset$ | \not\subset  |  非子集  |
|  $\subseteq$  |  \subseteq   |  真子集  |
| $\subsetneq$  |  \subsetneq  |  非子集  |
|  $\supseteq$  |  \supseteq   |          |
|    $\cup$     |     \cup     |   并集   |
|   $\bigcup$   |   \bigcup    |   并集   |
|    $\cap$     |     \cap     |   交集   |
|   $\bigcap$   |   \bigcap    |   交集   |
|   $\uplus$    |    \uplus    |  多重集  |
|  $\biguplus$  |  \biguplus   |  多重集  |
|  $\sqsubset$  |  \sqsubset   |          |
|  $\sqsupset$  |  \sqsupset   |          |
|   $\sqcap$    |    \sqcap    |          |
| $\sqsubseteq$ | \sqsubseteq  |          |
| $\sqsupseteq$ | \sqsupseteq  |          |
|    $\vee$     |     \vee     |          |
|   $\wedge$    |    \wedge    |          |
|  $\setminus$  |  \setminus   |   差集   |

## 微积分

|     数学算式      |  Markdown公式   |      核心语法      |
| :---------------: | :-------------: | :----------------: |
|     $\prime$      |     \prime      |      一阶导数      |
|      $\int$       |      \int       |      一重积分      |
|      $\iint$      |      \iint      |      双重积分      |
|      $\oint$      |      \oint      |      曲线积分      |
|     $\nabla$      |     \nabla      |        梯度        |
| $\int_0^2 x^2 dx$ | \int_0^2 x^2 dx | 其他的积分符号类似 |

## 逻辑运算

|   数学算式   | Markdown公式 | 核心语法 |
| :----------: | :----------: | :------: |
|  $\because$  |   \because   |   因为   |
| $\therefore$ |  \therefore  |   所以   |
|  $\forall$   |   \forall    |   任意   |
|   \(\exist\)   |    \exist    |   存在   |
|    $\vee$    |     \vee     |  逻辑与  |
|   $\wedge$   |    \wedge    |  逻辑或  |
|  $\bigvee$   |   \bigvee    |  逻辑与  |
| $\bigwedge$  |  \bigwedge   |  逻辑或  |

## 希腊字母

|    大写    | Markdown公式 |     小写      | Markdown公式 |
| :--------: | :----------: | :-----------: | :----------: |
|  $\Alpha$  |    \Alpha    |   $\alpha$    |    \alpha    |
|  $\Beta$   |    \Beta     |    $\beta$    |    \beta     |
|  $\Gamma$  |    \Gamma    |   $\gamma$    |    \gamma    |
|  $\Delta$  |    \Delta    |   $\delta$    |    \delta    |
| $\Epsilon$ |   \Epsilon   |  $\epsilon$   |   \epsilon   |
|            |              | $\varepsilon$ | \varepsilon  |
|  $\Zeta$   |    \Zeta     |    $\zeta$    |    \zeta     |
|   $\Eta$   |     \Eta     |    $\eta$     |     \eta     |
|  $\Theta$  |    \Theta    |   $\theta$    |    \theta    |
|  $\Iota$   |    \Iota     |    $\iota$    |    \iota     |
|  $\Kappa$  |    \Kappa    |   $\kappa$    |    \kappa    |
| $\Lambda$  |   \Lambda    |   $\lambda$   |   \lambda    |
|   $\Mu$    |     \Mu      |     $\mu$     |     \mu      |
|   $\Nu$    |     \Nu      |     $\nu$     |     \nu      |
|   $\Xi$    |     \Xi      |     $\xi$     |     \xi      |
| $\Omicron$ |   \Omicron   |  $\omicron$   |   \omicron   |
|   $\Pi$    |     \Pi      |     $\pi$     |     \pi      |
|   $\Rho$   |     \Rho     |    $\rho$     |     \rho     |
|  $\Sigma$  |    \Sigma    |   $\sigma$    |    \sigma    |
|   $\Tau$   |     \Tau     |    $\tau$     |     \tau     |
| $\Upsilon$ |   \Upsilon   |  $\upsilon$   |   \upsilon   |
|   $\Phi$   |     \Phi     |    $\phi$     |     \phi     |
|            |              |   $\varphi$   |   \varphi    |
|   $\Chi$   |     \Chi     |    $\chi$     |     \chi     |
|   $\Psi$   |     \Psi     |    $\psi$     |     \psi     |
|  $\Omega$  |    \Omega    |   $\omega$    |    \omega    |

## 省略号

不同省略号的区别是点的位置不同，`\ldots`位置稍低，`\cdots`位置居中。

| 数学算式 | Markdown公式 |       核心语法       |
| :------: | :----------: | :------------------: |
| $\dots$  |    \dots     | 一般用于有下标的序列 |
| $\ldots$ |    \ldots    |                      |
| $\cdots$ |    \cdots    | 纵向位置比\dots稍高  |
| $\vdots$ |    \vdots    |         竖向         |
| $\ddots$ |    \ddots    |                      |

## 空格

|    数学算式    | Markdown公式 |      核心语法      |
| :------------: | :----------: | :----------------: |
|   $123\!123$   |   123\!123   | 空格距离：-3/18 em |
|   $123\,123$   |   123\,123   | 空格距离：3/18 em  |
|   $123\:123$   |   123\:123   | 空格距离：4/18 em  |
|   $123\;123$   |   123\;123   | 空格距离：5/18 em  |
| $123\quad123$  | 123\quad123  |   空格距离：1 em   |
| $123\qquad123$ | 123\qquad123 |   空格距离：2 em   |

而上面中的em是指当前文本中文本的字体尺寸。

## 表格格式

一般使用`|--|--|`，这样的形式来创建表格。

- 列样式可以是`c, l, r`分别表示居中，左，右对齐
- 使用`|`表示一条竖线
- 表格中各行使用`\`分隔，各列使用`&`分隔
- 使用`\hline`在本行前加入一条直线
