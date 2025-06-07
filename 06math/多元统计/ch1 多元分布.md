# 1.0 预备知识

## 1.0.1 随机变量$X$

随机变量$X$期望、矩、方差：

 
| 期望     | $E(X)=\begin{cases}\int^{\infty}_{-\infty}tf(t)dt,\quad &若X连续;\\\sum_ix_iP\{X=x_i\},\quad &若X离散;\end{cases}$           |
| ------ | ---------------------------------------------------------------------------------------------------------------------- |
| **矩**  | **$E(X^k)=\begin{cases}\int^{\infty}_{-\infty}t^kf(t)dt,\quad &若X连续;\\\sum_ix_i^kP\{X=x_i\},\quad &若X离散;\end{cases}$** |
| **方差** | **$Var(X)=E\left[(X-E(X))^2\right]=E(X^2)-(E(X))^2$**                                                                  |

## 1.0.2 随机向量$X=(X_1,X_2,\dots,X_p)'$

令$x=(x_1,x_2,\dots,x_p)'$，$X_1,X_2,\dots,X_p$相互独立，当且仅当$F(x_1,x_2,\dots,x_p)=\prod^p_{i=1}F_i(x_i),\forall x\in \mathbb{R}^p$，其中$F_i(x_i)$是$X_i$的边缘**分布**函数。

 
| **联合分布函数**       | $\begin{align}F(x_1,x_2\dots,x_p)&=P\{X_1\le x_1,X_2\le x_2,\dots,X_p\le x_p\}\\&=P(X\le x)\end{align}$                                                                                           |
| ---------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **联合概率密度函数(非负)** | 存在$f(t_1,t_2,\dots,t_p)$满足下式：$F(x_1,x_2\dots,x_p)=\int^{x_1}_{-\infty}\int^{x_2}_{-\infty}\dots\int^{x_p}_{-\infty}f(t_1,t_2,\dots,t_p)dt_1dt_2\dots d_p$                                         |
| **边缘分布**         | (也就是选取随机向量中的部分、构成的分布)。$X$的$q$个分量($q<p$)$X^{(1)}=(X_1,X_2,\dots,X_q)'$的分布称为边缘分布。$P\{X^{(1)}\le u\}=P\{X_1\le u_1,\dots,X_q\le u_q\}=F(u_1,\dots,u_q,+\infty,\dots +\infty)$                        |
| **边缘概率密度函数**     | 对$X^{(1)}$: $g(u)=\int_{\mathbb{R}^{p-q}}f(u,v)dv$                                                                                                                                                |
| **条件密度**         | 令$X=(X^{(1)}{'},X^{(2)}{'})'$, $f(x)=f(x^{(1)},x^{(2)})$。$X^{(2)}$在给定$X^{(1)}=x^{(1)}$的条件密度为：$f(x^{(2)}\|X^{(1)}=x^{(1)})=\frac{f(x^{(1)},x^{(2)})}{g(x^{(1)})}$，$g(x^{(1)})$是$X^{(1)}$的边缘概率密度函数。 |

## 1.0.3 多元随机变量(随机向量)

 
| 期望$E(X)$          | $E(X)=(E(X_1),E(X_2),\dots,E(X_p))'$             |
| ----------------- | ------------------------------------------------ |
| **协方差$Cov(X)$**   | **$Cov(X)=E\left[(X-E(X))(X-E(X))'\right]$**   |
| **协方差$Cov(X,Y)$** | **$Cov(X,Y)=E\left[(X-E(X))(Y-E(Y))'\right]$** |

## 1.0.4 矩阵知识

一些运算：

+   $E(tr(AXB))=tr(AE(X)B)$：期望和trace的计算等级相同。
+   $Cov(AX)=ACov(X)A'$
    > $$ \begin{align} Cov(AX)&=E\left[(AX-E(AX))(AX-E(AX))'\right]\\ &=E\left[A(X-E(X))(X-E(X))'A'\right]\\ &=AE\left[(X-E(X))(X-E(X))'\right]A'\\ &=ACov(X)A' \end{align} $$
+   $Cov(AX,BY)=ACov(X,Y)B'$
+   $E(X'AX)=(E(X))'A(E(X))+tr(ACov(X))$：二次型，此公式将期望值分解为常数项（期望向量的二次型）和随机项（协方差矩阵与 A 的迹）。
    > $$ \begin{align} E(X'AX)&=E(\sum_{i,j}X_iA_{ij}X_j)\\ &=\sum_{i,j}A_{ij}E(X_iX_j)\\ &=\sum_{i,j}A_{ij}(E(X_i)E(X_j)+Cov(X_i,X_j)\\ &=(E(X))'A(E(X))+tr(ACov(X)) \end{align} $$

分块矩阵：$A=\begin{pmatrix}A_{11}&A_{12}\\A_{21}&A_{22}\end{pmatrix}$，其中$A_{11}$是非退化的方阵(可逆，满秩)。

记$A_{2|1}=A_{22}-A_{21}A_{11}^{-1}A_{12}$，则有$|A|=|A_{11}|·|A_{2|1}|$。 $$ A^{-1}=\begin{pmatrix} I&A_{11}^{-1}A_{12}\\ 0& I \end{pmatrix}\begin{pmatrix} A_{11}^{-1}&0\\ 0&A_{2|1}^{-1} \end{pmatrix}\begin{pmatrix} I&0\\ -A_{21}A_{11}^{-1}&I \end{pmatrix} $$

记$A^{-1}=\begin{pmatrix}B_{11}&B_{12}\\B_{21}&B_{22}\end{pmatrix}$, 则有：

+   $B_{11}=(A_{11}-A_{12}A_{22}^{-1}A_{21})^{-1}$
+   $B_{22}=(A_{22}-A_{21}A_{11}^{-1}A_{12})^{-1}$
+   $B_{12}=-A_{11}^{-1}A_{12}(A_{22}-A_{21}A_{11}^{-1}A_{12})^{-1}$
+   $B_{21}=-(A_{22}-A_{21}A_{11}^{-1}A_{12})^{-1}A_{21}A_{11}^{-1}$

![image-20241128173119356](https://cdn.jsdelivr.net/gh/SchwertLin/Pic/img/image-20241128173119356.png)

## 1.0.5 多元特征函数

(**特征函数与概率分布函数一一对应**)随机向量$X=(X_1,\dots,X_p)'$的特征函数为： $$ \phi(t)=\phi(t_1,\dots,t_p)=E[e^{i(t_1X_1+\dots+t_pX_p)}]=E[e^{it'X}] $$ 其中, $t=(t_1,\dots,t_p)'\in\mathbb{R}^p$, $i$是虚数单位($i^2=-1$)

性质：

1.  对正整数$k_1,\dots,k_p$, 如果$E(X_1^{k_1}\dots X_p^{k_p})$存在, 则
2.  对$0<k<p$, 分量$X^{(1)}=(X_1,\dots,X_k)'$的特征函数是$\phi(t_1,\dots,t_k,0,\dots,0)$.
3.  记$X_1,\dots,X_p$的边缘特征函数分别为$\phi_1(t_1),\dots,\phi_p(t_p)$, 记$X=(X_1,\dots,X_p)'$的特征函数是$\phi(t_1,\dots,t_p)$, 则$X_1,\dots,X_p$相互独立的充分必要条件是：$\phi(t_1,\dots,t_p)=\phi_1(t_1)\dots\phi_p(t_p)$.
4.  设$p$维随机向量$Y_1,\dots,Y_m$的特征函数分别为$\phi^{(1)}(t),\dots,\phi^{(m)}(t)$, 如果$Y_1,\dots,Y_m$相互独立, 则随机向量和 $Y_1+\dots+Y_m$的特征函数为: $\phi(y)=\phi^{(1)}(t)\dots\phi^{(m)}(t)$.

> Q:**我个人感觉这个地方是不是写错了？Y怎么会是p维向量？那角标不应该是p吗？**
> 
> A: 在这里，$Y_1, \dots, Y_m$ 是独立的随机向量，每个 $Y_i$ 依然是 $p$ 维的，所以 $Y_1, \dots, Y_m$ 是多个 $p$ 维向量

# 1.1 一元正态分布

【分布密度】若随机变量$X$的概率密度函数为： $$ p(x)=\frac{1}{\sqrt{2\pi}\sigma}\exp\left\{-\frac{(x-\mu)^2}{2\sigma^2}\right\} $$ 其中$-\infty<x,\mu<\infty,\sigma^2>0$，则称随机变量X服从正态分布。记为$X\overset{d}{\sim}N(\mu,\sigma^2)$, 其中$\mu$是均值, $\sigma^2$是方差。

# 1.2 多元正态分布

【分布密度】若$p$元随机向量$X$服从参数为$\mu,\Sigma$的多元正态分布，其概率密度函数为： $$ p(x)=(2\pi)^{-\frac p 2}|\Sigma|^{-\frac 1 2}\exp\left\{-\frac 1 2 (x-\mu)'\Sigma^{-1}(x-\mu)\right\} $$ 其中$\mu\in\mathbb{R}^p$，$\Sigma$为p阶正定矩阵，记为$X\overset{d}{\sim}N_p(\mu,\Sigma)$。

> d 代表服从分布(distribution)，$\Sigma$是多元正态分布的**方差**。

**p元标准正态分布：**$X\overset{d}{\sim}N_p(0,I_p)$

**定理1：**设p元随机向量$X=\mu+AY$, 其中$\mu\in\mathbb{R}^k, A$为$k\times p$的行满秩矩阵，$k\le p$, 随机向量$Y\overset{d}{\sim}N_p(0,I_p)$, 则$X\overset{d}{\sim}N_k(\mu,\Sigma)$, 其中$\Sigma=AA'>0$.

> **证明**：随机向量 $X$的特征函数定义为： $$ \phi_X(t) = \mathbb{E} \left[ e^{i t^T X} \right] $$ 其中，$t \in\mathbb{R}^k$是与 $X $同维度的向量。
> 
> 代入 $X = \mu + AY$到特征函数的定义中，得到： $$ \phi_X(t) = \mathbb{E} \left[ e^{i t^T (\mu + A Y)} \right]= e^{i t^T \mu} \mathbb{E} \left[ e^{i t^T A Y} \right] $$ 由于 $Y $是 $p$维标准正态随机向量，$Y N_p(0, I_p) $，其特征函数为： $$ \phi_Y(t) = \mathbb{E} \left[ e^{i t^T Y} \right] = e^{-\frac{1}{2} t^T t} $$ 这里 $t\in \mathbb{R}^p$是与 $Y $同维度的向量。
> 
> $$ \phi_X(t) = e^{i t^T \mu}\mathbb{E} \left[ e^{i t^T A Y} \right]= e^{i t^T \mu}e^{-\frac{1}{2} (A^T t)^T (A^T t)}\\ =e^{i t^T \mu}e^{-\frac{1}{2} t^T A A^T t} $$ 我们知道，一个 $k$维正态分布 $N_k(,) $的特征函数为： $$ \phi(t) = e^{i t^T \mu} e^{-\frac{1}{2} t^T \Sigma t}=e^{i t^T \mu}e^{-\frac{1}{2} t^T A A^T t} $$
> 
> 因此，$X $服从 $N_k(\mu, \Sigma)$分布，即： $$ X \overset{d}{\sim} N_k(\mu, \Sigma) $$
> 
> 如何产生$N_p(\mu,\Sigma)$的(伪)随机数？--==Cholesky 分解==
> 
> 生成的标准正态分布随机向量 $Z\overset{d}{\sim}N_p(0,I_p)$可以通过下列变换得到目标分布$X = \mu + L Z, \Sigma=LL'$, L 是 Cholesky 分解得到的下三角矩阵，Z是标准正态随机向量。

## 1.2.2 性质

 
| 性质         | 说明: $X\overset{d}{\sim}N(\mu,\Sigma)$                                                                                                                                                                                                                                                                                                                                                                                                                                   |
| ---------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1.密度函数     | $p(x)=(2\pi)^{-\frac p 2}\|\Sigma\|^{-\frac 1 2}\exp\left\{-\frac 1 2 (x-\mu)'\Sigma^{-1}(x-\mu)\right\}$                                                                                                                                                                                                                                                                                                                                                               |
| 2.特征函数     | $E(\exp(it'X))=\exp\{it'\mu-\frac{t'\Sigma t}2\}$                                                                                                                                                                                                                                                                                                                                                                                                                       |
| 3.期望方差     | $E(X)=\mu,Cov(X)=\Sigma$                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| 4.线性变换     | $Y=\eta+AX,\eta\in\mathbb{R}^k,A_{k\times p}, Y\overset{d}{\sim}N_k(\eta+A\mu,A\Sigma A')$                                                                                                                                                                                                                                                                                                                                                                              |
| 5.相互独立     | 设$X_1,\dots,X_k$相互独立，$X_i\overset{d}{\sim}N_p(\mu_i,\Sigma_i),1\le i\le k$, 则$\sum^k_{i=1}\alpha_iX_i\overset{d}{\sim}N_p(\sum^k_{i=1}\alpha_i\mu_i,\sum^k_{i=1}\alpha^2_i\Sigma_i)$                                                                                                                                                                                                                                                                                    |
| 6.卡方分布     | **$\Sigma>0$**, 则$(X-\mu)'\Sigma^{-1}(X-\mu)\overset{d}{\sim}\chi^2_p$, 其中$\chi^2_p$是自由度为p的卡方分布。                                                                                                                                                                                                                                                                                                                                                                        |
| 7.矩阵分解     | $X=\begin{pmatrix}X_1^{(q)}\\X_2^{(p-q)}\end{pmatrix},\mu=\begin{pmatrix}\mu_1\\\mu_2\end{pmatrix},\Sigma=\begin{pmatrix}\Sigma_{11}&\Sigma_{12}\\\Sigma_{21}&\Sigma_{22}\end{pmatrix}$,则$X_1^{(q)}\overset{d}{\sim}N_q(\mu_1,\Sigma_{11}),X_2^{(p-q)}overset{d}{\sim}N_{p-q}(\mu_2,\Sigma_{22})$                                                                                                                                                                       |
| 8.分量独立性    | $X=\begin{pmatrix} X_1^{(q_1)}\\\vdots\\X_k^{(q_k)}\end{pmatrix},\Sigma=\begin{pmatrix}\Sigma_{11}&\ldots&\Sigma_{1k}\\\vdots&\ddots&\vdots\\ \Sigma_{k1}&\ldots&\Sigma_{kk}\end{pmatrix}$,则$X_i^{(q_i)},X_j^{(q_j)}(1\le i<j\le k)$相互独立的**充要条件**是$Cov(X_i^{q_i},X_j^{(q_j)})=\Sigma_{ij}=0$.                                                                                                                                                                           |
| 9.条件分布     | $(X_1\|X_2=x_2)\overset{d}{\sim}N_q(\mu_{1\|2},\Sigma_{1\|2})$,其中$\mu_{1\|2}=E(X_1\|X_2=x_2)=\mu_1+\Sigma_{12}\Sigma_{22}^{-1}(x_2-\mu_2)$,$\Sigma_{1\|2}=Cov(X_1\|X_2=x_2)=\Sigma_{11}-\Sigma_{12}\Sigma_{22}^{-1}\Sigma_{21}$.$(\Sigma_{1\|2}\le\Sigma_{11})$                                                                                                                                                                                                         |
| 10.变量的独立分解 | 令$Y_1=X_1,Y_2=X_2-\Sigma_{21}\Sigma_{11}^{-1}X_1$;$Z_2=X_2,Z_1=X_1-\Sigma_{12}\Sigma_{22}^{-1}X_2$;则$Y_1$与$Y_2$相互独立，$Z_1$与$Z_2$相互独立，且$Y_1\overset{d}{\sim}N_q(\mu_1,\Sigma_{11}),Y_2\overset{d}{\sim}N_{p-q}(\mu_2-\Sigma_{21}\Sigma_{11}^{-1}\mu_1,\Sigma_{2\|1})$, $Z_2\overset{d}{\sim}N_{p-q}(\mu_2,\Sigma_{22}),Z_1\overset{d}{\sim}N_q(\mu_1-\Sigma_{12}\Sigma_{22}^{-1}\mu_2,\Sigma_{1\|2}$,$(\Sigma_{2\|1}=\Sigma_{22}-\Sigma_{21}\Sigma_{11}^{-1}\Sigma_{12})$ |

# 1.3 相关系数

 
| 定义                         | 说明                                                                                                                                                                                                                                                                                                                                                                                                                      |
| -------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 相关系数$p_{ij}$               | $X_i$与$X_j$：$p_{ij}=\frac{Cov(X_i,X_j)}{\sqrt{Var(X_i)}\sqrt{Var(X_j)}}=\frac{\sigma_{ij}}{\sqrt{\sigma_{ii}}\sqrt{\sigma_{jj}}}$                                                                                                                                                                                                                                                                                       |
| 相关矩阵R                      | $R=\begin{pmatrix}\rho_{11}&\ldots&\rho_{1p}\\\vdots &&\vdots\\ \rho_{p1}&\ldots&\rho_{pp}\end{pmatrix}=diag(\sigma_{11}^{-\frac 1 2},\dots,\sigma_{pp}^{-\frac 1 2})\begin{pmatrix}\sigma_{11}&\ldots&\sigma_{1p}\\\vdots &&\vdots\\ \sigma_{p1}&\ldots&\sigma_{pp}\end{pmatrix}diag(\sigma_{11}^{-\frac 1 2},\dots,\sigma_{pp}^{-\frac 1 2})$                                                                         |
| 偏相关系数                      | $X=\begin{pmatrix}X_1^{(q)}\\X_2^{(p-q)}\end{pmatrix},\mu=\begin{pmatrix}\mu_1\\\mu_2\end{pmatrix},\Sigma=\begin{pmatrix}\Sigma_{11}&\Sigma_{12}\\\Sigma_{21}&\Sigma_{22}\end{pmatrix}$, 则$(X_1^{(q)}\|X_2^{(p-q)})\overset{d}{\sim}N_q(\mu_{1\|2},\Sigma_{1\|2})$. 在给定$X_2^{(p-q)}$的条件下，$X_i$与$X_j$的条件相关系数$\rho_{(ij)\|(1\|2)}=\frac{\sigma_{(ij)\|(1\|2)}}{\sqrt{\sigma_{(ii)\|(1\|2)}}\sqrt{\sigma_{(jj)\|(1\|2)}}}$ |
| 精度矩阵$(k_{ij})_{p\times p}$ | 设随机向量$X$，有$Cov(X)=\Sigma>0$, 那么称$K=\Sigma^{-1}$为$X$的精度矩阵。                                                                                                                                                                                                                                                                                                                                                               |

> 偏相关系数是图模型和因果推断中的重要统计量，可以由特征函数+期望+方差，可以通过**偏相关系数判别多元正态随机向量分量之间的条件独立性**。

**精度矩阵的性质：**

1.  若$X=(X_1,\dots,X_p)'\overset{d}{\sim}N_p(\mu,\Sigma),\Sigma>0,K=\Sigma^{-1}=(k_{ij})_{p\times p}$, 则$k_{ii}=(Var(X_i|X_{(-i)}))^{-1},1\le i\le p$, 其中$X_{(-i)}=(X_1,\dots,X_{i-1},X_{(i+1)},\dots,X_p)',1\le i\le p$, 设$X\overset{d}{\sim}N_p(\mu,\Sigma),\Sigma>0$, 有如下分解：
    
    $X\begin{pmatrix}X_1^{(p_1)}\\X_2^{(p_2)}\\X_3^{(p_3)}\end{pmatrix},\Sigma=\begin{pmatrix}\Sigma_{11}&\Sigma_{12}&\Sigma_{13}\\\Sigma_{21}&\Sigma_{22}&\Sigma_{23}\\\Sigma_{31}&\Sigma_{32}&\Sigma_{33}\end{pmatrix},K=\begin{pmatrix}K_{11}&K_{12}&K_{13}\\K_{21}&K_{22}&K_{23}\\K_{31}&K_{32}&K_{33}\end{pmatrix}$
    
2.  在$X_3$给定的条件下，$X_1$与$X_2$相互条件独立的充要条件是$K_{12}=0$($K_{12}$是精度矩阵 $K$ 中的元素，表示在给定其他所有变量的条件下，$X_1$ 和$X_2$ 的关系的强度。)
    
    > 证明： $$ \begin{align} \Sigma_{12|3}&\overset{\text{定义}}{=}Cov((X_1,X_2)|X_3)\\ &\overset{\text{性质9}}{=}\begin{pmatrix}\Sigma_{11}& \Sigma_{12}\\\Sigma_{21}&\Sigma_{22}\end{pmatrix}-\begin{pmatrix}\Sigma_{13}\\\Sigma_{23}\end{pmatrix}\Sigma_{33}^{-1}\begin{pmatrix}\Sigma_{31}& \Sigma_{32}\end{pmatrix}\\ &\overset{\text{矩阵运算}}{=}\begin{pmatrix}\Sigma_{11}-\Sigma_{13}\Sigma_{33}^{-1}\Sigma_{31}&\Sigma_{12}-\Sigma_{13}\Sigma_{33}^{-1}\Sigma_{32}\\\Sigma_{21}-\Sigma_{23}\Sigma_{33}^{-1}\Sigma_{31}&\Sigma_{22}-\Sigma_{23}\Sigma_{33}^{-1}\Sigma_{32}\end{pmatrix}\\ &\overset{\text{分块矩阵运算}}{=}\begin{pmatrix}K_{11}&K_{12}\\K_{21}&K_{22}\end{pmatrix}^{-1} \end{align} $$ 由(分量独立性)：$X=\begin{pmatrix} X_1^{(q_1)}\\\vdots\\X_k^{(q_k)}\end{pmatrix},\Sigma=\begin{pmatrix}\Sigma_{11}&\ldots&\Sigma_{1k}\\\vdots&\ddots&\vdots\\ \Sigma_{k1}&\ldots&\Sigma_{kk}\end{pmatrix}$, 则$X_i^{(q_i)},X_j^{(q_j)}(1\le i<j\le k)$相互独立的**充要条件**是$Cov(X_i^{q_i},X_j^{(q_j)})=\Sigma_{ij}=0$.
    > 
    > 则$X_1$与$X_2$条件独立的充要条件为$\Sigma_{12}-\Sigma_{13}\Sigma_{33}^{-1}\Sigma_{32}=0$,$K_{12}=0$;则推广有$K_{13}=0,K_{23}=0$.
    > 
    > 无量纲：**因为精度矩阵的数值与变量的量纲有关**，所以进行标准化处理。令$C=\begin{pmatrix}c_{11}&\ldots&c_{1p}\\\vdots &\ddots&\vdots\\ c_{p1}&\ldots&c_{pp}\end{pmatrix}\overset{\Delta}{=}diag(k_{11}^{-\frac 1 2},\dots,k_{pp}^{-\frac 1 2})\begin{pmatrix}k_{11}&\ldots&k_{1p}\\\vdots &\ddots&\vdots\\ k_{p1}&\ldots&k_{pp}\end{pmatrix}diag(k_{11}^{-\frac 1 2},\dots,k_{pp}^{-\frac 1 2})$
    > 
    > $C=\begin{pmatrix}C_{11}&C_{12}&C_{13}\\C_{21}&C_{22}&C_{23}\\ C_{31}&C_{32}&C_{33}\end{pmatrix}$,(将得到的C根据$X_1,X_2,X_3$分块)。
    > 
    > 在给定$X_3$的条件下，$X_1$与$X_2$条件独立的充要条件$C_{12}=0$.
    

## 1.3.1 练习

![image-20241201094117103](https://cdn.jsdelivr.net/gh/SchwertLin/Pic/img/image-20241201094117103.png)

![image-20241201094132212](https://cdn.jsdelivr.net/gh/SchwertLin/Pic/img/image-20241201094132212.png)

对于$\hat{E}(Y|X_1,X_2,X_3,X_4)=\mu_Y+\Sigma_{YX}\Sigma_{XX}^{-1}(X-\mu_X)$： $$ \begin{align} \hat{E}(Y|X)&=\mu_Y+\Sigma_{YX}\Sigma_{XX}^{-1}(X-\mu_X)\\ &=95.423+\begin{pmatrix}56.689&176.381&-47.556&-190.9\end{pmatrix}\begin{pmatrix}31.941& 19.314& -28.663&-22.308\\ 19.314& 223.515& -12.811&-233.923\\ -28.663& -12.811& 37.87&2.923\\ -22.308& -233.923& 2.923& 258.615\end{pmatrix}^{-1}\begin{pmatrix}X_1-7.462\\X_2-48.154\\X_3-11.769\\X_4-30\end{pmatrix}\\ &=95.423+\begin{pmatrix}-2.06871& -2.83557 &-3.51512& -3.44172\end{pmatrix}\begin{pmatrix}X_1-7.462\\X_2-48.154\\X_3-11.769\\X_4-30\end{pmatrix}\\ &=95.423-2.069(X_1-7.462)-2.836(X_2-48.154)-3.515(X_3-11.769)-3.442(X_4-30) \end{align} $$ ![image-20241201095141147](https://cdn.jsdelivr.net/gh/SchwertLin/Pic/img/image-20241201095141147.png)

预测：计算y关于$(x_1,x_2)$的条件期望，从而用$(x_1,x_2)$预测$y$:

![image-20241201101835469](https://cdn.jsdelivr.net/gh/SchwertLin/Pic/img/image-20241201101835469.png)

# 1.4 矩阵多元正态分布

## 1.4.0 矩阵拉直和Kronecker积

**矩阵拉直**：记$X=(x_1,\dots,x_p)是$$n\times p$的矩阵。矩阵拉直运算，是将矩阵按**列**拉直为向量$vec(X)=\begin{pmatrix}x_1\\\vdots\\x_p\end{pmatrix}_{np\times 1}$

**Kronecker积**：令$A=(a_{ij})_{n\times p},B_{m\times q}$，A和B的Kronecker积记为：$A\otimes B=(a_{ij}B)_{nm\times pq}$

> 令$X=\begin{pmatrix} 1 & 2 \\ 3 & 4 \\ 5 & 6 \end{pmatrix},vec(X)=\begin{pmatrix} 1 \\ 3 \\ 5 \\ 2 \\ 4 \\ 6 \end{pmatrix}$
> 
> 令$A = \begin{pmatrix} 1 & 2 \\ 3 & 4 \end{pmatrix}, \quad B = \begin{pmatrix} 0 & 5 \\ 6 & 7 \end{pmatrix}$
> 
> $A \otimes B$ 的计算步骤如下：
> 
> $ A B = $$\begin{pmatrix} 0 & 5 & \vert & 0 & 10 \\ 6 & 7 & \vert & 12 & 14 \\ \hline 0 & 15 & \vert & 0 & 20 \\ 18 & 21 & \vert & 24 & 28 \end{pmatrix}$$
> 
> $

**拉直运算和Kronecker积的性质**

 
| 性质 | 说明 |
| --- | --- |
| 1 | 对任意实数$\lambda$，有$(\lambda A)\otimes B = A\otimes(\lambda B)=\lambda(A\otimes B)$ |
| 2 | $A\otimes(B + C)=A\otimes B+A\otimes C$，$(B + C)\otimes A = B\otimes A+C\otimes A$ |
| 3 | $(A\otimes B)\otimes C = A\otimes(B\otimes C)$ |
| 4 | $(A\otimes B)'=A'\otimes B'$ |
| 5 | $(A\otimes B)(C\otimes D)=(AC)\otimes(BD)$ |
| 6 | 若$A$和$B$都是非奇异的方阵，则$(A\otimes B)^{-1}=A^{-1}\otimes B^{-1}$ |
| 7 | $\text{tr}(A\otimes B)=\text{tr}(A)\cdot\text{tr}(B)$，$\text{tr}(C'D)=({vec}(C))'({vec}(D))$ |
| 8 | 若$A$和$B$分别是$n$和$m$阶方阵，则$\vert A\otimes B\vert=\vert A\vert^{n}\cdot\vert B\vert^{m}$ |
| 9 | 若$A$、$Y$和$B$分别是$n\times p$、$p\times q$和$q\times m$的矩阵，则${vec}(AYB)=(B'\otimes A){vec}(Y)$。(如果我们对矩阵 $Y$ 进行线性变换 $AYB$，那么其 **“拉直”** 形式（即按列展开）将受到 Kronecker积的影响。) |

## 1.4.1 矩阵分布

设 $X_1, \cdots, X_n$ i.i.d.(独立同分布, independent and identically distributed)，$X_i = (x_{i1}, \cdots, x_{ip})' \stackrel{d}{=} N_p(\mu, \Sigma)$，即 $X_1, \cdots, X_n$ 是来自 $p$ 元正态总体 $N_p(\mu, \Sigma)$ 的独立样本。

记 $X=(X_1, \cdots, X_n)$，则 $X$ 是一个 $p\times n$ 的随机矩阵。

随机矩阵的期望：$E(X)=(\mu, \cdots, \mu)=\mu\cdot 1_n'$， 其中 $1_n=(1, \cdots, 1)'$。

矩阵的拉直运算：$\text{vec}(X)=\text{vec}((X_1, \cdots, X_n)) = \begin{pmatrix} X_1\\ \vdots\\ X_n \end{pmatrix}_{(np)\times 1}$

随机矩阵的协方差阵：$Cov(X)=Cov(vec(X))$

**随机矩阵的分布：随机矩阵拉直后的随机向量的分布。**

矩阵$X$的运算 由于$X=(X_1,\cdots,X_n)$，有 $$ E(\text{vec}(X)) = \begin{pmatrix} \mu\\ \vdots\\ \mu \end{pmatrix}, \quad \text{Cov}(\text{vec}(X)) = \begin{pmatrix} \Sigma & 0 & \cdots & 0\\ 0 & \Sigma & \cdots & 0\\ \vdots & \vdots & \ddots & \vdots\\ 0 & 0 & \cdots & \Sigma \end{pmatrix} $$ 即$E(\text{vec}(X)) = 1_n \otimes \mu$，$\text{Cov}(\text{vec}(X)) = I_n \otimes \Sigma$，其中$I_n$是$n$阶单位阵。

> 是因为$X_1, \cdots, X_n$ 独立同分布，所以它们的$\mu,\Sigma$都是一样的。

## 随机矩阵拉直运算的性质(转置)

性质1：对 $n\times m$ 的随机矩阵 $Y$，若有 $$ E(\text{vec}(Y))=\alpha\otimes\beta, \text{Cov}(\text{vec}(Y)) = A\otimes B $$ 其中，$\alpha,\beta$ 分别是 $m$ 和 $n$ 维列向量，$A$ 和 $B$ 分别是 $m$ 和 $n$ 阶方阵，则 $$ E(\text{vec}(Y'))=\beta\otimes\alpha, \text{Cov}(\text{vec}(Y')) = B\otimes A $$

由性质1，对上述随机矩阵 $X$ 有 $$ E(\text{vec}(X'))=\mu\otimes 1_n, \text{Cov}(\text{vec}(X'))=\Sigma\otimes I_n $$ 因此，对由 $n$ 个 $p$ 维正态总体的独立样本组成的随机矩阵 $X$， $\text{vec}(X)\stackrel{d}{\sim}N_{np}(1_n\otimes\mu, I_n\otimes\Sigma)$， $\text{vec}(X')\stackrel{d}{\sim}N_{np}(\mu\otimes 1_n,\Sigma\otimes I_n)$。

## 1.4.3 矩阵正态分布

> 矩阵正态分布是指矩阵的每一列或每一行都服从正态分布，且这些列或行之间可能具有某种协方差结构。
> 
> **矩阵正态分布的一个重要特性是它的“拉直”形式也是正态分布。**

假设矩阵 $X$ 是一个 $n \times p$ 的矩阵，它的“拉直”（vectorization）形式 $\text{vec}(X)$ 也就是把矩阵按列展开成一个向量。如果这个向量服从正态分布，我们就说矩阵 $X$ 服从 **矩阵正态分布**。更具体地：

+   如果 $\text{vec}(X)\stackrel{d}{\sim}N_{np}(1_n\otimes\mu, I_n\otimes\Sigma)$，我们说矩阵 $X$ 服从矩阵正态分布，记为：$X\stackrel{d}{\sim}N_{p\times n}(\mu\cdot 1_n',I_n\otimes\Sigma)$。

一般地，记 $n\times p$ 的正态随机矩阵为 $X\stackrel{d}{\sim}N_{n\times p}(B,\Sigma\otimes V)$，其中 $$ \begin{cases} B= E(X)=\mu\cdot 1_n'\\ \Sigma\otimes V=\text{Cov}(\text{vec}(X))=I_n\otimes\Sigma \end{cases} $$ $\Sigma$ 和 $V$ 分别是 $p$ 和 $n$ 阶方阵(正定阵)，分别控制着$X$的行列之间的协方差结构。

从这个分布，可以得到$X$的拉直形式$vec(X)$服从以下正态分布： $$ \text{vec}(X)\stackrel{d}{\sim}N_{np}(\text{vec}(B),\Sigma\otimes V) $$

## 密度函数

矩阵正态分布的密度函数表示了矩阵 $X$ 出现某种特定值的概率。

若 $X\stackrel{d}{\sim}N_{p\times n}(B, V\otimes\Sigma)$，其密度函数如下： $$ \frac{1}{(2\pi)^{(np)/2}|V\otimes\Sigma|^{1/2}}\exp\left\{-\frac{1}{2}(\text{vec}(X - B))'(V\otimes\Sigma)^{-1}(\text{vec}(X - B))\right\} $$ 上式等价于（用**迹的性质**进行简化）： $$ \frac{1}{(2\pi)^{(np)/2}|V|^{n/2}|\Sigma|^{p/2}}\exp\left\{-\frac{1}{2}\text{tr}[(X - B)'\Sigma^{-1}(X - B)V^{-1}]\right\} $$ **证明：**(即证$(\text{vec}(X) - \text{vec}(B))' (V \otimes \Sigma)^{-1} (\text{vec}(X) - \text{vec}(B)) = \text{tr} \left[ (X - B)' \Sigma^{-1} (X - B) V^{-1} \right]$)

> 利用Kronecker积的一个重要性质：$\text{vec}(AXB)=(B'\otimes A)\text{vec}(X)$ 其中 $A$、$X$ 和 $B$ 分别是 $n\times p$、$p\times q$ 和 $q\times m$ 的矩阵。 $$ \begin{align} 右式&=\text{tr} \left[ (X - B)' \Sigma^{-1} (X - B) V^{-1} \right]\\ &\overset{性质7}{=}\left(vec(X-B)\right)'\left(vec(\Sigma^{-1} (X - B) V^{-1})\right)\\ &\overset{性质9}{=}\left(vec(X-B)\right)'(\Sigma^{-1}\otimes V^{-1})vec(X-B)\\ &\overset{性质6}{=}\left(vec(X-B)\right)'(\Sigma\otimes V)^{-1}vec(X-B)\\ &=左式 \end{align} $$

## 线性变换

> 如果矩阵服从正态分布，经过线性变换后，结果仍然服从矩阵正态分布，只是均值和协方差矩阵发生了变化。

性质2：设 $p\times n$ 的矩阵 $X$ 服从矩阵正态分布 $X\stackrel{d}{\sim}N_{p\times n}(B, V\otimes\Sigma),(\Sigma_{p\times p}\geq0, V_{n\times n}\geq0)$。

对其进行线性变换$ Y = C + AX,$ 其中 $C_{q\times m}, A_{q\times p}$ 和 $\Gamma_{n\times m}$ 是常数矩阵。

则矩阵$Y$的分布将是： $$ Y\stackrel{d}{\sim}N_{q\times m}((C + AB\Gamma), (\Gamma'V\Gamma)\otimes (A\Sigma A')) $$ $C+AB\Gamma$：这是矩阵 $Y$ 的均值矩阵，表示了经过线性变换后的期望。

$(\Gamma' V \Gamma) \otimes (A \Sigma A')$：这是矩阵 $Y$ 的协方差矩阵，表示了变换后的行列协方差结构。

【挑战20天学完多元统计分析，让我们说：DDL是最佳生产力！】

> 非常好矩阵分析，使我大脑旋转——
