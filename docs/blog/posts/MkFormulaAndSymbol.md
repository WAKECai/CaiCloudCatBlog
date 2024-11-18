---
date:
    created: 2024-11-14
    updated: 2024-11-18
categories:
    - Tools
---

# Markdown常见公式

Markdown常见的公式以及符号汇总摘录。
<!-- more -->

!!! warning "注意"
    这里是对来自CSDN的[史上最全Markdown公式、符号总结！！！](https://blog.csdn.net/weixin_42782150/article/details/104878759)的摘录与修改，这篇文章非常好，基本涵盖了所有的Mk数学公式和符号，侵权联系我删除。


一般公式分为两种形式，行内公式和行间公式。行内公式是在公式代码块的前后均添加一个`$` ；行间公式则是在公式代码块的前后均添加两个`$$` 。

```
$ \Gamma(z) = \int_0^\infty t^{z-1}e^{-t}dt\,. $
$$\Gamma(z) = \int_0^\infty t^{z-1}e^{-t}dt\,.$$
```

***

公式排列：一般使用`\binom{a}{b}`或者`{a \choose b}`实现对 $a$ , $b$ 两个公式的排列。

```
\binom{n+1}{2k} {n+1 \choose 2k}
```

$$
\binom{n+1}{2k} {n+1 \choose 2k}
$$

***



## 向量公式

向量表示：使用`\mathbf{x}`来表示向量$\mathbf{x}$。

```
f(\mathbf{x})=\mathbf{w}^T\mathbf{x}
```

$$
f(\mathbf{x})=\mathbf{w}^T\mathbf{x}
$$


## 分段函数

定义函数的时候经常需要分情况给出表达式，使用 `{…`。其中：

（1）使用`\ `来分隔分组；

（2）使用`& `来指示需要对齐的位置；

（3）使用`\ + 空格`来表示空格；

（4）如果要使分类之间的垂直间隔变大，可以使用`\[2ex] `代替`\ `来分隔不同的情况。(`3ex`,`4ex` 也可以用，`1ex` 相当于原始距离）。

```
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

```
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

```
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

```
J(\theta) = \frac{1}{2m}\sum_{i = 0} ^m(y^i - h_\theta (x^i))^2
```

$$
J(\theta) = \frac{1}{2m}\sum_{i = 0} ^m(y^i - h_\theta (x^i))^2
$$

## 批量梯度下降

```
\frac{\partial J(\theta)}{\partial\theta_j} = -\frac1m\sum_{i=0}^m(y^i-h_\theta(x^i))x^i_j
```

$$
\frac{\partial J(\theta)}{\partial\theta_j} = -\frac1m\sum_{i=0}^m(y^i-h_\theta(x^i))x^i_j
$$



## case环境的使用

```
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

```
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

```
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

```
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

```
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

```
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

```
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
\begin{aligned} \left.\begin{aligned}        B'&=-\partial \times E,\\        E'&=\partial \times B - 4\pi j,       \end{aligned} \right\} \qquad \text{Maxwell's equations}\end{aligned}
$$



```
\begin{aligned}
 \sigma_1 &= x + y  &\quad \sigma_2 &= \frac{x}{y} \\	
 \sigma_1' &= \frac{\partial x + y}{\partial x} & \sigma_2' 
    &= \frac{\partial \frac{x}{y}}{\partial x}
\end{aligned}
```

$$
\begin{aligned} \sigma_1 &= x + y  &\quad \sigma_2 &= \frac{x}{y} \\	 \sigma_1' &= \frac{\partial x + y}{\partial x} & \sigma_2'     &= \frac{\partial \frac{x}{y}}{\partial x}\end{aligned}
$$

```
\begin{aligned}
a_n&=\frac{1}{\pi}\int\limits_{-\pi}^{\pi}f(x)\cos nx\,\mathrm{d}x\\
&=\frac{1}{\pi}\int\limits_{-\pi}^{\pi}x^2\cos nx\,\mathrm{d}x\\[6pt]
\end{aligned}
```

$$
\begin{aligned}a_n&=\frac{1}{\pi}\int\limits_{-\pi}^{\pi}f(x)\cos nx\,\mathrm{d}x\\&=\frac{1}{\pi}\int\limits_{-\pi}^{\pi}x^2\cos nx\,\mathrm{d}x\\[6pt]\end{aligned}
$$



## 公式编辑的编号设置

|     符号     |                         功能                         |
| :----------: | :--------------------------------------------------: |
| `tag{标号}`  | 公式宏包序号设置命令，可用于带星号公式环境中的公式行 |
| `tag*{标号}` |        作用与tag相同，只是标号两侧没有圆括号         |

```
x^2+y^2=z^2 \tag{1$'$}
```

$$
x^2+y^2=z^2 \tag{1$'$}
$$

```
x^4+y^4=z^4 \tag{*}
```

$$
x^4+y^4=z^4 \tag{*}
$$

```
x^5+y^5=z^5 \tag*{*}
```

$$
x^5+y^5=z^5 \tag*{*}
$$

```
x^6+y^6=z^6 \tag{1-1}
```

$$
x^6+y^6=z^6 \tag{1-1}
$$



## 矩阵

```
\begin{pmatrix}1 & 2 \\ 3 &4\\ \end{pmatrix}
```

$$
\begin{pmatrix}1 & 2 \\ 3 &4\\ \end{pmatrix}
$$

```
\begin{bmatrix}1 & 2 \\ 3 & 4\\ \end{bmatrix}
```


$$
\begin{bmatrix}1 & 2 \\ 3 & 4\\ \end{bmatrix}
$$

```
\begin{Bmatrix}1 &2 \\ 3 & 4\\ \end{Bmatrix}
```


$$
\begin{Bmatrix}1 &2 \\ 3 & 4\\ \end{Bmatrix}
$$

```
\begin{vmatrix}1 &2 \\ 3 &4\\ \end{vmatrix}
```


$$
\begin{vmatrix}1 &2 \\ 3 &4\\ \end{vmatrix}
$$

```
\begin{Vmatrix}1 &  2 \\ 3 &  4\\ \end{Vmatrix}
```


$$
\begin{Vmatrix}1 &  2 \\ 3 &  4\\ \end{Vmatrix}
$$

**元素省略**可以使用`\cdots`表示⋯，`\ddots`表示⋱，`\vdots`表示⋮，从而省略矩阵中的元素，如：

```
\begin{pmatrix}
1&a_1&a_1^2&\cdots&a_1^n\\
1&a_2&a_2^2&\cdots&a_2^n\\
\vdots&\vdots&\vdots&\ddots&\vdots\\
1&a_m&a_m^2&\cdots&a_m^n\\
\end{pmatrix}
```


$$
\begin{pmatrix}1&a_1&a_1^2&\cdots&a_1^n\\1&a_2&a_2^2&\cdots&a_2^n\\\vdots&\vdots&\vdots&\ddots&\vdots\\1&a_m&a_m^2&\cdots&a_m^n\\\end{pmatrix}
$$

1、不带括号的矩阵

```
\begin{matrix}
1 & 2 & 3\\
4 & 5 & 6 \\
7 & 8 & 9
\end{matrix}
\tag{1}
```

$$
\begin{matrix}1 & 2 & 3\\4 & 5 & 6 \\7 & 8 & 9\end{matrix}\tag{1}
$$

2、带小括号的矩阵

```
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
\left(\begin{matrix}1 & 2 & 3\\4 & 5 & 6 \\7 & 8 & 9\end{matrix}\right)\tag{2}
$$
3、带中括号的矩阵

```
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
\left[\begin{matrix}1 & 2 & 3\\4 & 5 & 6 \\7 & 8 & 9\end{matrix}\right]\tag{3}
$$

4、带大括号的矩阵

```
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
\left\{\begin{matrix}1 & 2 & 3\\4 & 5 & 6 \\7 & 8 & 9\end{matrix}\right\}\tag{4}
$$

5、带省略号的矩阵

```
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
\left[\begin{matrix}a & b & \cdots & a\\b & b & \cdots & b\\\vdots & \vdots & \ddots & \vdots\\c & c & \cdots & c\end{matrix}\right]\tag{5}
$$

6、带横线/竖线分割的矩阵

```
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
\left[    \begin{array}{c|cc}    1 & 2 & 3 \\ \hline    4 & 5 & 6 \\    7 & 8 & 9    \end{array}\right]\tag{7}
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

```
x=a_0 + \frac{1^2}{a_ 1+\frac{2^2}{a_2+\frac{3^2}{a_3+ \frac{4^2}{a_4+...}}}}
```

$$
x=a_0 + \frac{1^2}{a_ 1+\frac{2^2}{a_2+\frac{3^2}{a_3+ \frac{4^2}{a_4+...}}}}
$$

`\cfrac`表示连分式：

数学算式：

```
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

```
$a \equiv b \pmod n$
```

$$
a \equiv b \pmod n
$$

