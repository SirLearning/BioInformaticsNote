
# 2.0 由一元正态分布导出的分布

应用： 1) 构造参数的置信区间； 2) 假设检验

## 2.0.1 卡方分布(对应Wishart分布)

设$X=(x_1,\cdots,x_n)$，其中$x_1,\cdots,x_n$ **i.i.d.**(独立同分布)，$x_i\stackrel{d}{\sim}N_1(0,1)$，$1\leq i\leq n$。

则称随机变量$Y = XX'=\sum_{i = 1}^{n}x_i^2$为服从自由度为$n$的卡方分布，记为 ： $$ Y=\sum_{i = 1}^{n}x_i^2\stackrel{d}{\sim}\chi^2(n) $$

密度函数为： $$ g_n(x)=\begin{cases}\frac{x^{\frac{n-2}{2}}e^{-\frac{x}{2}}}{2^{\frac n 2}\Gamma(\frac n 2)}, &\quad x>0\\ 0, &\quad x\le0 \end{cases} $$ 期望方差： $$ X\sim\chi^2(n)\\E(X)=n,Cov(X)=2n $$

## 2.0.2 t分布(对应$T^2$分布)

假设随机变量$X$和$Y$**相互独立**，且$X\stackrel{d}{\sim}N_1(0,1)$，$Y\stackrel{d}{\sim}\chi^2(n)$， 则称随机变量$t = \frac{X}{\sqrt{Y/n}}$为服从自由度为$n$的$t$分布，记为： $$ t = \frac{X}{\sqrt{\frac Y n}}\stackrel{d}{\sim}t(n) $$

密度函数： $$ t_n(x)=\frac{\Gamma\left(\frac{n + 1}{2}\right)}{\Gamma\left(\frac{n}{2}\right)\sqrt{n\pi}}\left(1+\frac{x^2}{n}\right)^{-\frac{n + 1}{2}}, \quad -\infty<x<\infty $$

## 2.0.3 F分布(对应Wilks分布)

假设随机变量$X$和$Y$**相互独立**，且$X\stackrel{d}{\sim}\chi^2(n)$，$Y\stackrel{d}{\sim}\chi^2(m)$， 则称随机变量$F=\frac{X/n}{Y/m}$为服从自由度为$n$和$m$的$F$分布，记为: $$ F = \frac{\frac X n}{\frac Y m}\stackrel{d}{\sim}F(n,m). $$

密度函数： $$ f_{m,n}(x) = \begin{cases} \frac{\Gamma(\frac{m + n}{2})}{\Gamma(\frac{m}{2})\Gamma(\frac{n}{2})} m^{\frac{m}{2}} n^{\frac{n}{2}} x^{\frac{m}{2}-1}(n + mx)^{-\frac{m + n}{2}}, x > 0 \\ 0, \text{其它} \end{cases} $$

## 2.0.4 $\Gamma$函数

> 此处主要是对$\Gamma$函数的解释，下文还有在Wilks分布--Beta分布中提及。

Gamma 函数的定义为： $$ \Gamma(x) = \int_0^\infty t^{x-1} e^{-t} \, dt, \quad \text{对于} \ x > 0 $$ 与阶乘函数关系:

+   对于正整数 $n$，有：$\Gamma(n) = (n-1)!$
+   对于非整数的 $x$: $\Gamma\left( \frac{1}{2} \right) = \sqrt{\pi}$

性质:

 
| 性质 | 说明 |
| --- | --- |
| 递推 | $\Gamma(x+1) = x \Gamma(x), \quad \text{对于} \ x > 0$, 这个关系与阶乘的递推性质相似，因为 $n! = n \times (n-1)!$。 |
| 阶乘 | $\Gamma(n) = (n-1)! \quad \text{对于正整数} \ n$ |
| 对称性 | $\Gamma$函数的反射公式：$\Gamma(x) \Gamma(1-x) = \frac{\pi}{\sin(\pi x)}, \quad 0 < x < 1$ |
| 特殊值 | $\Gamma\left( \frac{1}{2} \right) = \sqrt{\pi}$ |

# 2.1 Wishart分布

## 2.1.1 定义

设随机向量$X=(X_1,\cdots,X_n)$，其中$X_1,\cdots,X_n$ i.i.d.(独立同分布)，每个$X_i$都遵循一个多维正态分布 $X_i\stackrel{d}{\sim}N_p(0,\Sigma)$，$1\leq i\leq n$。

**$p$阶Wishart分布**：称$p$阶随机矩阵$W = XX'=\sum_{i = 1}^{n}X_iX_i'$的分布为$p$阶Wishart分布，记为 $ WW_p(n,)$, 其中$n$称为其**自由度**。

> 【矩阵正态分布与Wishart分布】**Wishart分布实际上是矩阵正态分布的一个特殊情况。**
> 
> 当你通过独立的正态随机向量生成矩阵$X$后，矩阵 $W = X X'$ 就是 Wishart分布的实例。
> 
> **Wishart分布**: $W = X X' \sim W_p(n, \Sigma)$ 是矩阵$X$与其转置 $X'$ 的乘积，意味着$X$ 和 $X'$ 都是**矩阵正态分布**, $X\stackrel{d}{\sim}N_{p\times n}(0,I_n\otimes\Sigma), X' \sim N_{n \times p}(0, \Sigma \otimes I_n)$

## 2.1.2 密度函数

当**$\Sigma>0$，$n\geq p$**时，$p$阶Wishart分布有密度函数: $$ f_p(W)=\frac{|W|^{\frac{(n - p - 1)}2}\exp\left\{-\frac{1}{2}\text{tr}(\Sigma^{-1}W)\right\}}{2^{\frac{np}2}|\Sigma|^{\frac n 2}\pi^{\frac{p(p - 1)}{4}}\prod_{i = 1}^{p}\Gamma\left(\frac{n - i + 1}{2}\right)}, \quad W>0 $$ 若记$\Gamma_p(x)=\pi^{p(p - 1)/4}\prod_{i = 1}^{p}\Gamma\left(x-\frac{i - 1}{2}\right)$，并称之为$p$维$\Gamma$函数，则有 $$ f_p(W)=\frac{|W|^{\frac{(n - p - 1)}2}\exp\left\{-\frac{1}{2}\text{tr}(\Sigma^{-1}W)\right\}}{2^{\frac{np}2}\Gamma_p\left(\frac{n}{2}\right)|\Sigma|^{\frac n2}}, \quad W>0. $$ 当$p = 1$时，**Wishart分布退化成$\chi^2$分布**（一元正态分布导出）。

$ f_1(w)=2^{-n 2}^{-1}(n 2){-n}w{2}{-}, w>0. $ 即$W = X'X\stackrel{d}{\sim}\sigma^2\chi^2(n)$。

> **将Wishart分布转化为随机向量的分布**：
> 
> $W=XX'=(w_{ij})_{p\times p}$对称 ($(XX')'=XX', w_{ij}=w_{ji}$)，因此可以把W的分布展开成一个由$\frac{p(p+1)}2$的元素组成的随机向量$(w_{11},\dots,w_{1p},w_{22},\dots,w_{2p},\dots,w_{pp})'$的分布。(按每行的向量拉直) $$ W=\begin{pmatrix} w_{11}&w_{12}&\ldots&w_{1p}\\ w_{21}&w_{22}&\ldots&w_{2p}\\ \vdots&\vdots&\ddots&\vdots\\ w_{p1}&w_{p2}&\ldots&w_{pp}\\ \end{pmatrix}=\begin{pmatrix} w_{1}\\w_{2}\\\vdots\\w_{p} \end{pmatrix}\overset{d}\sim\begin{pmatrix} w_{1}'\\w_{2}'\\\vdots\\w_{p}' \end{pmatrix} $$

对前提条件的说明：要求自由度$n\ge p$是为确保$W>0$(W正定)必成立。$rank(W)=\min(n,p)=p$

+   当自由度 $n\lt p$时，矩阵 $X$ 的列数不足以提供足够的信息来使得 $W$ 为正定矩阵。外积矩阵 $W$ 可能会退化（奇异），导致它不是正定的（即存在零特征值）
+   当 $n \geq p$（自由度 $n$ 至少为矩阵维度 $p$）矩阵 $X$ 具有足够的列，才能确保矩阵 $W$ 是 **正定矩阵**。

> **Q: 为什么W一定要是正定的？**
> 
> A: $W=XX'$的形式确保了$W$是对称的, 但是对称与正定并不等价。正定要需要其主对角元素是大于0的。
> 
> 因为$X$的列(n个)是独立同分布的，$XX'$一定满秩：$rank(W)=p$
> 
> Ps: 联想到Cholesky分解：LU+对称=正定. A symmetric matrix A possessing an LU factorization in which each pivot is positive is said to be positive definite. $A=LU=LDL^T=LD^{\frac 1 2}D^{\frac 1 2}L^T=BB^T$
> 
> 何时矩阵$A$存在LU分解？
> 
> +   将A通过基本初等变换转化为上三角矩阵U的过程中不能出现主元=0的情况。
> +   每个主子矩阵$A_k$都是非奇异的。

## 2.1.3 分布性质

 
| 简要说明          | 性质                                                                                                                                                                                                                                                                                                      |
| ------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1.分布期望        | 若 $W \stackrel{d}{\sim} W_p(n,\Sigma)$，则 $E(W) = n\Sigma$                                                                                                                                                                                                                                               |
| 2.线性变换        | 若 $W \stackrel{d}{\sim} W_p(n,\Sigma)$，$C$ 是 $k\times p$ 阶矩阵，则 $CWC' \stackrel{d}{\sim} W_k(n,C\Sigma C')$                                                                                                                                                                                              |
| 3.特征函数        | 若 $W \stackrel{d}{\sim} W_p(n,\Sigma)$，则 $W$ 特征函数为 $$E(e^{itr(TW)}) = \|I_p - 2i\Sigma T\|^{-n/2}$$ , 其中 $T$ 为 $p$ 阶实对称阵                                                                                                                                                                                |
| 4.可加性         | 若 $W_1,\cdots,W_k$ 相互独立，$W_i \stackrel{d}{\sim} W_p(n_i,\Sigma)$，$1\leq i\leq k$，则 $$\sum_{i = 1}^{k} W_i \stackrel{d}{\sim} W_p(\sum_{i = 1}^{k} n_i,\Sigma)$$                                                                                                                                         |
| 5.矩阵二次型       | 【详细见下】若 $A$ 为幂等矩阵，则矩阵二次型 $Q = XAX' \stackrel{d}{\sim} W_p(m,\Sigma)$， 其中，$m = \text{Rank}(A) = R(A) = \text{tr}(A)$。                                                                                                                                                                                    |
| 6.独立分解        | 【详细见下】 设 $W \stackrel{d}{\sim} W_p(n,\Sigma)$，$\Sigma>0$，$n\geq p$。 将 $W$ 和 $\Sigma$ 作如下相同的 $q$ 阶和 $(p - q)$ 阶矩阵分块: $W = \begin{pmatrix} W_{11} & W_{12} \\ W_{21} & W_{22} \end{pmatrix}, \quad \Sigma = \begin{pmatrix} \Sigma_{11} & \Sigma_{12} \\ \Sigma_{21} & \Sigma_{22} \end{pmatrix}.$        |
| 7.行列式         | 设 $W \stackrel{d}{\sim} W_p(n,\Sigma)$，$\Sigma>0$，$n\geq p$。则 $$\|W\|\stackrel{d}{=}\|\Sigma\|\prod_{i = 1}^{p} \gamma_i,$$ 其中，$\gamma_1,\cdots,\gamma_p$ 相互独立，$\gamma_i \stackrel{d}{\sim} \chi^2(n - i + 1)$，$1\leq i\leq p$                                                                          |
| 8.逆矩阵期望       | 若 $W \stackrel{d}{\sim} W_p(n,\Sigma)$，$\Sigma>0$，$n>(p + 1)$，则 $E(W^{-1})=\frac{1}{n - p - 1}\Sigma^{-1}$                                                                                                                                                                                              |
| 9.逆矩阵分布       | 设 $W \stackrel{d}{\sim} W_p(n,\Sigma)$，$\Sigma>0$，$n\geq p$， 则对任意非零的 $p$ 维向量 $a$，都有 $\frac{a'\Sigma^{-1}a}{a'W^{-1}a} \stackrel{d}{\sim} \chi^2(n - p + 1)$                                                                                                                                             |
| 10.Bartlett分解 | 设 $W \stackrel{d}{\sim} W_p(n, I_p)$，$n\geq p$。将 $W$ 作分解 $W = TT'$，$T$ 是对角元为正的下三角矩阵。 令 $T=(t_{ij})_{p\times p}$，则 $t_{11}, t_{21}, t_{22}, \cdots, t_{p1}, t_{p2}, \cdots, t_{pp}$ 相互独立，且 $t_{ii}^2 \stackrel{d}{\sim} \chi^2(n - p + 1)$,$t_{ij} \stackrel{d}{\sim} N(0, 1)$ 对 $1\leq j < i\leq p$ 成立。 |

> Bartlett 分解: 将$W$分解成$TT'$, 这个下三角矩阵 $T$ 的对角线元素的平方服从卡方分布，非对角线元素服从标准正态分布，并且这些元素是相互独立的。
> 
> **Q: Bartlett分解和Cholesky分解有什么关系？**
> 
> A: 形式上相似，用处不同。
> 
> +   相似：两者都涉及将矩阵分解为下三角矩阵与其转置的乘积。
> 
> 在 Bartlett 分解和 Cholesky 分解中，都有一个下三角矩阵 $T$ 或 $L$，并且分解形式是 $W = TT'$ 或 $A = LL^T$。
> 
> +   不同：
>     
>     +   **应用背景不同**：Cholesky 分解用于**任意对称正定矩阵**，而 Bartlett 分解用于威尔奇分布（Wishart 分布）矩阵，特别是当协方差矩阵是单位矩阵时。Bartlett 分解涉及威尔奇分布的统计性质，如卡方分布和正态分布的关系。
>     +   **元素的分布不同**：在 Bartlett 分解中，$T$ 的元素有特定的概率分布（如 $t_{ii}^2 \sim \chi^2(n - p + 1)$ 和 $t_{ij} \sim N(0, 1)$），这些元素是相互独立的，而在 Cholesky 分解中，$L$ 的元素是通过递归计算的，并没有类似的概率分布性质。
>     +   **独立性**：Bartlett 分解中的 $T$ 的元素是相互独立的，而 Cholesky 分解中 $L$的元素之间是有依赖关系的。

## 性质5：矩阵二次型

> 首先介绍一下 二次型、矩阵二次型是个什么，我们再谈Wishart分布与矩阵二次型之间的关联。
> 
> **二次型**：
> 
> ![image-20241202163338879](https://cdn.jsdelivr.net/gh/SchwertLin/Pic/img/image-20241202163338879.png)
> 
> 因为二次型是一个数值，所以转置就等于自身。 $$ f(x)=\frac{f(X)+f(X)^T}2=\frac{X^TA^TX+X^TA^TX}2=X^T(\frac{A^T+A}{2})X=X^TAX\\ \frac{A^T+A}{2}=A $$ 上式说明**$A$必是对称的**。
> 
> **矩阵二次型**：若随机矩阵 $X \stackrel{d}{\sim} N_{p\times n}(0, I_n \otimes \Sigma)$，或 $X' \stackrel{d}{\sim} N_{n\times p}(0, \Sigma \otimes I_n)$，则称 $Q = XAX'$ 为矩阵二次型，其中 $A$ 是 $n$ 阶对称方阵，$A \geq 0$(表示$A$是半正定的)。
> 
> 若 $X=(X_1,\cdots,X_n)$，其中 $X_1,\cdots,X_n$ i.i.d.，$X_i \stackrel{d}{\sim} N_p(0,\Sigma)$，$1 \leq i \leq n$， $A=(a_{ij})_{n\times n}$，则 $$ Q = XAX'=\sum_{i = 1}^{n} \sum_{j = 1}^{n} a_{ij}X_iX_j' $$ 特别地，当 $A = I_n$ 时，$Q = XX' \stackrel{d}{\sim} W_p(n,\Sigma)$。

随机矩阵 $X \stackrel{d}{\sim} N_{p\times n}(0, I_n \otimes \Sigma)$，矩阵二次型$Q=XAX', A_{n}$.

1.  若 $A$ 为幂等矩阵(投影)，则矩阵二次型 $Q = XAX' \stackrel{d}{\sim} W_p(m,\Sigma)$， 其中，$m = \text{Rank}(A) =dim\ R(A) = \text{tr}(A)$
    
    > (5.9.13) Projectors and Idempotents
    > 
    > A linear operator P on V is a projector if and only if $P^2 = P$.
    > 
    > 证明： 对称+幂等=正交投影,通过构造$Y=XU$来证明$Q$这个二次型服从自由度为n的Wishart分布。
    > 
    > ![image-20241202161549153](https://cdn.jsdelivr.net/gh/SchwertLin/Pic/img/image-20241202161549153.png)
    > 
    > ![image-20241202162418298](https://cdn.jsdelivr.net/gh/SchwertLin/Pic/img/image-20241202162418298.png)
    > 
    > 由 $A$ 幂等+对称，所以$A$是正交投影算子。
    > 
    > (5.13.5)存在正交阵 $U$，使得 $A = U\begin{pmatrix} I_m & 0 \\ 0 & 0 \end{pmatrix}U'$，其中 $m = Rank(A)$. 下面考虑矩阵正态分布的正交变换 $Y = XU$ 的分布。
    > 
    > 矩阵拉直的性质9：对矩阵 $C_{n\times p}, Z_{p\times q}, D_{q\times m}$，有 $$\text{vec}(CZD)=(D'\otimes C)\text{vec}(Z).$$
    > 
    > 期望：U是标准正交阵、不改变X的长度，只改变方向: $E(Y)=E(XU)=E(X) = 0$
    > 
    > 方差：$Cov(AX)=ACov(X)A', (A\otimes B)'=A'\otimes B',(A\otimes B)(C\otimes D)=(AC\otimes BD)$ $$ \begin{align} \text{Cov}[\text{vec}(Y)]&=\text{Cov}[\text{vec}(XU)]=\text{Cov}[\text{vec}(I_pXU)]\\ &=\text{Cov}[(U'\otimes I_p)\text{vec}(X)]\\ &=(U'\otimes I_p)\text{Cov}[\text{vec}(X)](U\otimes I_p)\\ &=(U'\otimes I_p)(I_n\otimes\Sigma)(U\otimes I_p)\\ &=(U'I_nU)\otimes(I_p\Sigma I_p)\\ &=I_n\otimes\Sigma. \end{align} $$ 因此有 $Y \stackrel{d}{\sim} N_{p\times n}(0, I_n \otimes \Sigma)$。 令 $Y=(Y_1,\cdots,Y_n)$，可知 $Y_1,\cdots,Y_n$ 是独立同分布的 $p$ 维正态随机向量，均值为0，协方差为 $\Sigma$。
    > 
    > 进而有， $$ Q = XAX' = XU\begin{pmatrix} I_m & 0 \\ 0 & 0 \end{pmatrix}U'X' = Y\begin{pmatrix} I_m & 0 \\ 0 & 0 \end{pmatrix}Y'=\sum_{i = 1}^{m} Y_iY_i' \\ Q\stackrel{d}{\sim} W_p(m,\Sigma) $$ 得证。
    
2.  设 $Q = XAX'$，$Q_1 = XBX'$，$A$ 和 $B$ 都是幂等矩阵。 若 $Q_2 = Q - Q_1 \geq 0$，则 $Q_2 \stackrel{d}{\sim} W_p(m - r,\Sigma)$， 其中，$m = Rank(A)$，$r = Rank(B)$，且 $Q_1$ 与 $Q_2$ 相互独立。
    
3.  设 $Q = XAX'$，$A$ 为幂等矩阵。 则 $P'X'$ 与 $Q$ 独立的充要条件为 $AP = 0$，其中 $P$ 是 $n\times p$ 的矩阵。
    
    > 证明：(个人推导，可能有误)
    > 
    > $AP=0$表示矩阵 $P$ 中的列向量必须全部位于 $A$ 的零空间中，也就是说，矩阵 $P$ 中的所有列向量与 $A$ 所投影的子空间是正交的。 $$ \begin{align} \text{Cov}(P'X', X A X') &=\text{Cov}(P'X', Q) \\ &= \mathbb{E}[(P'X' - \mathbb{E}[P'X'])(XAX' - \mathbb{E}[XAX'])]\\ &=E[P' X' X A X']-E[P'X']E[XAX']\\ &=0 \end{align} $$ 因为$X \stackrel{d}{\sim} N_{p\times n}(0, I_n \otimes \Sigma), E(X)=E(X')=0，E(P'X')=P'E(X')=0$ $$ \begin{align} E[P' X' X A X']&=0\\ &=E[P'X']E[XAX']\\ &=P'E[X']E[X]AE[X']\\ P'A&=0 \end{align} $$ 因为$P'A=0$, $A$是对称的，所以可以得到$AP=0$.
    > 
    > 绷，感觉是个死循环，没法推。
    

## 性质6: 独立分解

设 $W \stackrel{d}{\sim} W_p(n,\Sigma)$，$\Sigma>0$，$n\geq p$。 将 $W$ 和 $\Sigma$ 作如下相同的 $q$ 阶和 $(p - q)$ 阶矩阵分块 $W = \begin{pmatrix} W_{11} & W_{12} \\ W_{21} & W_{22} \end{pmatrix}, \quad \Sigma = \begin{pmatrix} \Sigma_{11} & \Sigma_{12} \\ \Sigma_{21} & \Sigma_{22} \end{pmatrix}.$ $$ W = \begin{pmatrix} W_{11} & W_{12} \\ W_{21} & W_{22} \end{pmatrix}=\begin{pmatrix} I&0\\W_{21}W_{11}^{-1}&I \end{pmatrix}\begin{pmatrix} W_{11}&W_{12}\\ 0&W_{22}-W_{21}W_{11}^{-1}W_{12} \end{pmatrix} $$ 上方是我从矩阵分析中找出的分块矩阵的分解，感觉和下面的性质比较相关。则有：

+   (独立性)$W_{22}-W_{21}W_{11}^{-1}W_{12}$ 与 $(W_{11}, W_{21})$ 相互独立；
+   (条件分布)$W_{22}-W_{21}W_{11}^{-1}W_{12} \stackrel{d}{\sim} W_{p - q}((n - q),\Sigma_{2|1}),\Sigma_{2|1}=\Sigma_{22}-\Sigma_{21}\Sigma_{11}^{-1}\Sigma_{12}$；
+   (矩阵分布)$W_{11} \stackrel{d}{\sim} W_q(n,\Sigma_{11})$；
+   (条件下的分布)在 $W_{11}$ 给定的条件下， $$W_{21}W_{11}^{-\frac 12} \stackrel{d}{\sim} N_{(p - q)\times q}(\Sigma_{21}\Sigma_{11}^{-\frac 12}W_{11}^{\frac 12}, I_q \otimes \Sigma_{2|1}).$$

特别地，当 $\Sigma_{21}=0$ 时，有 ：

+   $W_{22}-W_{21}W_{11}^{-1}W_{12}$，$W_{11}$ 与 $W_{21}W_{11}^{-\frac 12}$ 相互独立；
+   $W_{22}-W_{21}W_{11}^{-1}W_{12} \stackrel{d}{\sim} W_{p - q}((n - q),\Sigma_{22})$；
+   $W_{11} \stackrel{d}{\sim} W_q(n,\Sigma_{11})$；
+   $W_{21}W_{11}^{-\frac 12} \stackrel{d}{\sim} N_{(p - q)\times q}(0, I_q \otimes \Sigma_{22})$。

# 2.2 Hotelling $T^2$分布

> Hotelling $T^2$ 统计量是一个“无量纲”统计量，在进行假设检验时不需要显式地估计协方差矩阵 $\Sigma$，因为它已经被标准化为与 $\Sigma$ 无关的形式。

## 2.2.1 定义

Hotelling $T^2$分布：设$X\overset{d}{\sim}N_p(0,\Sigma),W\overset{d}{\sim}W_p(n,\Sigma)$，且$X$和$W$相互独立。记为$T^2=nX'W^{-1}X$.

特别地，当$p=1,\Sigma=1$时，Hotelling $T^2$分布退化为一维正态分布情况中的$t$分布的平方：$t^2=nX'WX=\frac{X^2}{\frac W n}\overset{d}{\sim}F(1,n)$(**$t$分布的变量的平方服从第一自由度为1，第二自由度为n的F分布**) $$ 1D:t = \frac{X}{\sqrt{\frac Y n}}\stackrel{d}{\sim}t(n) $$ 假设$\Sigma>0$: (将$X$用$\Sigma^{-\frac 1 2}X$替换、$W$用$\Sigma^{-\frac 1 2}W\Sigma^{-\frac 1 2}$替换) $$ \begin{align} T^2&=nX'W^{-1}X\\ &=n(\Sigma^{-\frac 1 2}X)'(\Sigma^{-\frac 1 2}W\Sigma^{-\frac 1 2})^{-1}(\Sigma^{-\frac 1 2}X) \end{align} $$ 通过标准化变换，发现$\Sigma^{-\frac 1 2}X\stackrel{d}{\sim}N_p(0,I_p), \Sigma^{-\frac 1 2}W\Sigma^{-\frac 1 2}\stackrel{d}{\sim}W_p(n,I_p)$。

所以Hotelling $T^2$分布与协方差矩阵$\Sigma$无关，仅依赖于样本数量n和维度p，记为$T_p^2(n)$.

## 2.2.2 分布性质

 
| 性质 | 说明 |
| --- | --- |
| 1.相互独立 | $\frac{X'W^{-1}X}{\chi^2(n - p + 1)} \stackrel{d}{=} \frac{\chi^2(p)}{\chi^2(n - p + 1)}$,其中分子分母相互独立 |
| 2.$T^2$与F分布 | $\frac{n - p + 1}{np}T_p^2(n) \stackrel{d}{=} \frac{\chi^2(p)/p}{\chi^2(n - p + 1)/(n - p + 1)} \stackrel{d}{\sim} F(p,(n - p + 1))$ |
| 3.密度函数 | $T_p^2(n)$的密度函数为$p(t)=\frac{\Gamma((n + 1)/2)}{\Gamma(p/2)\Gamma((n - p + 1)/2)} \cdot \frac{(t/n)^{(p - 2)/2}}{(1 + t/n)^{(n + 1)/2}}$ |

## 2.2.3 非中心的Hotelling $T^2$分布

> **Q：自由度是什么？**
> 
> A：自由度通常代表可以自由选择或独立变化的数值的数量。假设你有一个样本数据集 $X_1, X_2, \dots, X_n$。
> 
> 如果你知 $n-1$ 个数据点，并且要求样本的均值为某一特定值（比如 0），那么最后一个数据点是由其他 $n-1$个数据点决定的。因此，这样的数据集的自由度是$n-1$，因为只有 $n-1$个数据点可以自由变化。
> 
> **Q：两个自由度？**
> 
> A：对于一些非中心分布，比如$T^2$、$F$分布，通常有两个参数（注意不是自由度）。
> 
> +   **第一个自由度**：与 **数据的维度** 或 **分子部分的卡方分布** 相关，反映了数据的变化度、模型拟合的效果或者均值的偏离。
> +   **第二个自由度**：与 **误差的自由度** 或 **分母部分的卡方分布** 相关，通常与样本大小、样本误差和模型的复杂度有关。（如果是基于样本方差的估计，需要-1：在计算样本的方差时，样本的均值是一个参数，因此计算样本方差时，只有$n-1$ 个数据点是自由变化的。）
> +   **非中心参数**：不是自由度，而是参数，反映了样本均值的偏离程度，即数据的“非中心性”。

定义：设$X\stackrel{d}{\sim}N_{p}(\mu,\Sigma)$，$W\stackrel{d}{\sim}W_{p}(n,\Sigma)$，且$X$和$W$相互独立。

则$T^{2}=nX'W^{-1}X$的分布为非中心的Hotelling$T^{2}$分布，记为$T_{p}^{2}(n,a)$，其中$a = \mu'\Sigma^{-1}\mu$是非中心参数。

**性质：**

1.  $X'W^{-1}X\stackrel{d}{=}\frac{\chi^{2}(p,a)}{\chi^{2}(n - p + 1)}$
2.  $\frac{n - p + 1}{np}T_{p}^{2}(n,a)\stackrel{d}{=}\frac{\chi^{2}(p,a)/p}{\chi^{2}(n - p + 1)/(n - p + 1)}\stackrel{d}{\sim}F(p,(n - p + 1),a)$

# 2.3 Wilks分布

## 2.3.1 定义

定义：假设$W_1 \stackrel{d}{\sim} W_p(n,\Sigma)$，$W_2 \stackrel{d}{\sim} W_p(m,\Sigma)$，$\Sigma>0$，$n\geq p$，$W_1$和$W_2$相互独立。记 $ =, $ 则称$\Lambda$的分布为Wilks分布，记为$\Lambda_{p,n,m}$。

> 由于: $$ \Lambda=\frac{|\Sigma^{-1/2}W_1\Sigma^{-1/2}|}{|\Sigma^{-1/2}W_1\Sigma^{-1/2}+\Sigma^{-1/2}W_2\Sigma^{-1/2}|},\\\begin{cases} \Sigma^{-1/2}W_1\Sigma^{-1/2} \stackrel{d}{\sim} W_p(n, I_p) \\ \Sigma^{-1/2}W_2\Sigma^{-1/2} \stackrel{d}{\sim} W_p(m, I_p)\end{cases} $$ 故Wilks分布$\Lambda_{p,n,m}$与$\Sigma$无关。

**F分布与Beta分布的关系**：

> **Q: Beta分布？**
> 
> A: 二项分布$X\sim B(n,p)$可以看做是多次重复进行伯努利实验所得到的分布。在多次重复进行二项分布的实验中，我们想要知道p的所有可能取值的概率，这就是一个**Beta分布**。
> 
> +   $B(\alpha, \beta)$ 的概率密度函数（PDF）为：
> 
> $$ f(x;\alpha, \beta) = \frac{x^{\alpha-1} (1-x)^{\beta-1}}{B(\alpha, \beta)}, \quad 0 \leq x \leq 1 $$
> 
> 其中，$B(\alpha, \beta)$ 是 Beta 函数，是一个归一化常数，确保积分为 1。 $$ \Gamma(x)=\int^{+\infty}_0 t^{x-1}e^{-t}dt\\ B(\alpha,\beta)=\frac{\Gamma(\alpha)\Gamma(\beta)}{\Gamma(\alpha+\beta)}=\int^1_0 t^{\alpha-1}(1-t)^{\beta-1}dt $$ Beta分布由两个参数 $\alpha$ 和$\beta$ 控制，这两个参数通常被称为 **形状参数**。Beta 分布广泛应用于统计学中，尤其是在贝叶斯统计和比例数据建模中。
> 
> +   当 $\alpha = \beta = 1$ 时，Beta 分布就是均匀分布。
> +   当 $\alpha > \beta$ 时，分布倾向于 1（右偏）。
> +   当 $\alpha < \beta$ 时，分布倾向于 0（左偏）。

给定随机变量$F\stackrel{d}{\sim}F(n,m)$，服从F分布(其中n, m 分别是分子的自由度和坟墓的自由度)。F 分布的性质之一是，它可以与 Beta 分布建立联系。

1.  $$\frac{\frac{n}{m}F(n,m)}{1+\frac{n}{m}F(n,m)}\stackrel{d}{=}B\left(\frac{n}{2},\frac{m}{2}\right),$$ 其中$B\left(\frac{n}{2},\frac{m}{2}\right)$是自由度为$\left(\frac{n}{2},\frac{m}{2}\right)$的$Beta$分布。
2.  $$\frac{1 - B\left(\frac{m}{2},\frac{n}{2}\right)}{B\left(\frac{m}{2},\frac{n}{2}\right)}\cdot\frac{m}{n}\stackrel{d}{=}F(n,m).$$

## 2.3.2 分布性质

 
| 性质 | 说明 |
| --- | --- |
| 1 | $\Lambda_{p,n,m} \stackrel{d}{=} B_1B_2\cdots B_p$，其中，$B_1, B_2,\cdots, B_p$ 相互独立， $ B_i B(,), 1ip. $ 因此它是$p = 1$时$Beta$分布的推广，而不是$F$分布的直接推广 |
| 2 | $\Lambda_{p,n,m} \stackrel{d}{=} \Lambda_{m,(n + m - p),p}$ |
| 3与F分布的关系 | $\begin{align}1.&\frac{n}{m} \cdot \frac{1 - \Lambda_{1,n,m}}{\Lambda_{1,n,m}} \stackrel{d}{\sim} F(m,n)\\2.&\frac{n + 1 - p}{p} \cdot \frac{1 - \Lambda_{p,n,1}}{\Lambda_{p,n,1}} \stackrel{d}{\sim} F(p,(n + 1 - p))\\3.&\frac{n - 1}{m} \cdot \frac{1 - \sqrt{\Lambda_{2,n,m}}}{\sqrt{\Lambda_{2,n,m}}} \stackrel{d}{\sim} F(2m,2(n - 1))\\4.&\frac{n+1-p}{p}·\frac{1-\sqrt{\Lambda_{p,n,2}}}{\Lambda_{p,n,2}} \stackrel{d}{\sim} F(2n,2(n+1-p))\end{align}$ |

# 2.4 总结

   
|  | Wishart分布 | Hotelling $T^2$分布 | Wilks分布 |
| --- | --- | --- | --- |
| 1维下 | $\chi ^2$分布 | t分布**平方** | Beta分布 |
| 2 | 正态随机向量特殊二次型的分布 | 常用于检验统计量的分布 | 常用于似然比检验统计量的分布 |
| 3 | 样本离差阵是最常见的服从Wishart分布的随机矩阵 | 计算需转化为F分布 | 计算在很多情况下可以转化为F分布 |

> **Q: 样本离差阵是什么**？
> 
> A: 样本离差阵$A$后续会介绍。
> 
> 设$X$为$n\times p$的数据矩阵，$E(X)=E(E(X_1),E(X_2),\ldots,E(X_p))$ $$ \bar{X}=\frac 1 nX'1_n\\ A=X'X-n\bar X\bar X'=X'(I_n-\frac 1 n 1_n1_n')X $$ 注意是$1_n$.

## 2.4.1 作业

若 $W \stackrel{d}{\sim} W_{p}(n,\Sigma)$，$\Sigma > 0$。$A$ 是 $p$ 阶常数方阵，试求 $E(|AW|)$。 $$ E(|AW|)=|A|E(|W|) $$

根据性质7：设 $W \stackrel{d}{\sim} W_p(n,\Sigma)$，$\Sigma>0$，$n\geq p$。则 $$|W|\stackrel{d}{=} |\Sigma|\prod_{i = 1}^{p} \gamma_i,$$ 其中，$\gamma_1,\cdots,\gamma_p$ 相互独立，$\gamma_i \stackrel{d}{\sim} \chi^2(n - i + 1)$，$1\leq i\leq p$ $$ |A|E(|W|)=|A|E(|\Sigma|\prod_{i = 1}^{p} \gamma_i)\\ =|A||\Sigma|\prod_{i = 1}^{p}E(\gamma_i) $$

对于$\gamma_i\sim\chi^2(n-i+1)$,其期望是$E(\gamma_i)=n-i+1$

所以期望式子可以写成： $$ |A||\Sigma|\prod_{i=1}^{p}E(\gamma_i)\\ =|A||\Sigma|\prod_{i=1}^{p}(n-i+1) $$

> 找另外一个同学对了对答案，我这么写没什么问题，但是gpt每次都给我不同的答案，逆天。

【挑战20天学完多元统计分析，让我们说：DDL是最佳生产力！】

> 急，只剩下10天了。。。
