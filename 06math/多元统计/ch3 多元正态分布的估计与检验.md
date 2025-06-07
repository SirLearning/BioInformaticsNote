# 3.1 多元正态分布样本统计量

设$X_1,X_2,\cdots,X_n$为来自多元正态总体$N_p(\mu,\Sigma)$的独立样本，其中$\mu\in R^p$，$\Sigma>0$，$n>p$。记:

  
| metric | 公式 | 说明 |
| --- | --- | --- |
| 样本均值 | $\overline{X}=n^{-1}\sum_{i = 1}^{n}X_i$ | 无偏估计，即$E(\overline{X})=\mu$。 |
| 样本离差阵 | $V=\sum_{i = 1}^{n}(X_i-\overline{X})(X_i-\overline{X})'$ | 衡量了样本点相对于样本均值的离散程度。 |
| 样本协方差阵 | $S=\frac{1}{n-1}V$ | 对离差阵进行归一化 |

> 事实：$(\overline{X},V)$是$(\mu,\Sigma)$的完全充分统计量, 这意味着$\overline{X}$和$V$包含了样本中关于总体参数$\mu$和$\Sigma$的所有信息。

## 3.1.1 ($\bar{X}$, $V$) 的分布性质

1.  $\bar{X} \sim N_p(\mu, \Sigma / n)$；
2.  $V \sim W_p(n - 1, \Sigma)$；
3.  $\bar{X}$ 与 $V$ 相互独立。

> **证明：**
> 
> （1）记 $X = (X_1, \cdots, X_n)$，则有 $E(X) = \mu \mathbf{1}_n'$，$\text{Cov}(\text{vec}(X)) = I_n \otimes \Sigma$。
> 
> 令 $U = (U_1, U_2, \cdots, U_n)$ 为 $n$ 阶正交矩阵，其中: $$ U_1 = \left( \frac{1}{\sqrt{n}}, \frac{1}{\sqrt{n}}, \cdots, \frac{1}{\sqrt{n}} \right)' = \frac{1}{\sqrt{n}} \mathbf{1}_n\\ 1_n'U_j=\sqrt{n}(\frac 1 {\sqrt{n}}1_n)'U_j=\sqrt{n}U_iU_j=0 $$ $U$的第一列 $U_1$ 被特别选择为与样本均值方向相关的向量。令 $Y = XU$ 记为 $(Y_1, Y_2, \cdots, Y_n)$，则$Y_1$代表了样本均值方向上的信息, $Y_2, \cdots, Y_n$则代表了与样本均值正交的剩余信息。 $$ E(Y) = E(X)U = \mu \mathbf{1}_n'U = \mu \mathbf{1}_n'\left( \frac{1}{\sqrt{n}} \mathbf{1}_n, U_2, \cdots, U_n \right) = (\sqrt{n} \mu, 0, \cdots, 0)\\ \begin{align} \text{Cov}(\text{vec}(Y))&=\text{Cov}(\text{vec}(I_p XU))\\ &=\text{Cov}((U' \otimes I_p)\text{vec}(X))\\ &=(U' \otimes I_p)\text{Cov}(\text{vec}(X))(U \otimes I_p)\\ &=(U' \otimes I_p)(I_n \otimes \Sigma)(U \otimes I_p)\\ &=I_n \otimes \Sigma \end{align} $$ 从上面的$Cov(Y)=I_n\otimes \Sigma$可以得到：$Y_1, Y_2, \cdots, Y_n$相互独立，且$Y_1 = \sqrt{n}\bar{X} \sim N_p(\sqrt{n}\mu,\Sigma)$， $Y_2, \cdots, Y_n \sim N_p(0,\Sigma)$。 因而有$\bar{X} \sim N_p(\mu,\Sigma / n)$，即(1)成立。
> 
> （2）由于$YY'=(XU)(U'X') = XX'$，即$\sum_{i = 1}^{n}X_iX_i'=\sum_{i = 1}^{n}Y_iY_i'$，因而有 $$ \begin{align} V&=\sum_{i = 1}^{n}X_iX_i'-n\bar{X}\bar{X}'\\ &=\sum_{i = 1}^{n}X_iX_i'-Y_1Y_1'\\ &=\sum_{i = 1}^{n}Y_iY_i'-Y_1Y_1'\\ &=\sum_{i = 2}^{n}Y_iY_i'\sim W_p(n - 1,\Sigma)\end{align} $$ 所以(2)成立。 又由于$\sqrt{n}\bar{X}=Y_1$，$V=\sum_{i = 2}^{n}Y_iY_i'$，因此$\bar{X}$与$V$独立，即(3)成立。

# 3.2 多元正态分布的参数估计

## 3.2.1 极大似然估计

观测样本$X=(X_1,X_2,\cdots,X_n)$的联合密度： $$ f(X)=(2\pi)^{-\frac{n p}{2}}|\Sigma|^{-\frac{n}{2}}\exp\left\{-\frac{1}{2}\text{tr}\Sigma^{-1}(V + n(\bar{X}-\mu)(\bar{X}-\mu)')\right\} $$ 首先求$\mu$的极大似然估计: $$ \begin{align} f(X)&=(2\pi)^{-\frac{n p}{2}}|\Sigma|^{-\frac{n}{2}}\exp\left\{-\frac{1}{2}\text{tr}\Sigma^{-1}(V + n(\bar{X}-\mu)(\bar{X}-\mu)')\right\}\\ &=(2\pi)^{-\frac{n p}{2}}|\Sigma|^{-\frac{n}{2}}\exp\left\{-\frac{1}{2}\text{tr}\Sigma^{-1}V-\frac{n}{2}\text{tr}\Sigma^{-1}(\bar{X}-\mu)(\bar{X}-\mu)'\right\}\\ &=(2\pi)^{-\frac{n p}{2}}|\Sigma|^{-\frac{n}{2}}\exp\left\{-\frac{1}{2}\text{tr}\Sigma^{-1}V-\frac{n}{2}(\bar{X}-\mu)'\Sigma^{-1}(\bar{X}-\mu)\right\} \end{align} $$ 易知$\mu$的极大似然估计为$\max f(X)=(\bar{X}-\mu)'\Sigma^{-1}(\bar{X}-\mu)=0$：$\hat{\mu}=\bar{X}$。 即正态总体均值的极大似然估计是样本均值。

将$\mu=\bar{X}$代入似然函数并去掉与参数无关的项，有： $$ f(X)\propto|\Sigma|^{-n/2}\exp\left\{-\frac{1}{2}\text{tr}(\Sigma^{-1}V)\right\} $$ 考虑正交分解$\Sigma^{-1/2}V\Sigma^{-1/2}=UAU'$，其中$U$是正交矩阵， $\Lambda=\text{diag}(\lambda_1,\cdots,\lambda_p)$。那么有: $$ |\Sigma|^{-1}=|V|^{-1}\prod_{i = 1}^{p}\lambda_i,\\ \text{tr}(\Sigma^{-1}V)=\text{tr}(\Sigma^{-1/2}V\Sigma^{-1/2})=\text{tr}(UAU')=\text{tr}(AU'U)=\text{tr}(\Lambda)=\sum_{i = 1}^{p}\lambda_i. $$ 则上面的式子变为： $$ f(X)\propto|\Sigma|^{-n/2}\exp\left\{-\frac{1}{2}\text{tr}(\Sigma^{-1}V)\right\}\\ f(X)\propto|V|^{-n/2}\prod_{i = 1}^{p}\lambda_i^{n/2}\exp\left\{-\frac{\lambda_i}{2}\right\} $$ 上式在$\lambda_1=\cdots=\lambda_p=n$时取最大值，故$\Sigma$的极大似然估计$\hat{\Sigma}$满足： $$ \hat{\Sigma}^{-1/2}V\hat{\Sigma}^{-1/2}=nI_p\Rightarrow\hat{\Sigma}=V/n $$ 因此，正态总体参数$(\mu,\Sigma)$的极大似然估计为$(\hat{\mu},\hat{\Sigma})=(\bar{X},V/n)$。 记 :

| \--- | 公式 | 期望 |
| --- | --- | --- |
| 样本协方差阵 | $S = \frac{V}{n - 1}$ | $E(\bar{X})=\mu$ |
| 样本精度矩阵 | $K = S^{-1}$ | $E(S)=E(V)/(n - 1)=\Sigma$ |

因此，$(\bar{X},S)$是$(\mu,\Sigma)$的无偏估计(一致最小)。

## 3.2.2 样本相关系数

记$\Upsilon = (\rho_{ij})_{p\times p}$为正态总体的相关系数矩阵，并记$V=(v_{ij})_{p\times p}$，$S=(s_{ij})_{p\times p}$，则$\rho_{ij}$的极大似然估计为: $$ \hat{\rho}_{ij}=r_{ij}=\frac{v_{ij}}{\sqrt{v_{ii}v_{jj}}}=\frac{s_{ij}}{\sqrt{s_{ii}s_{jj}}}, \quad 1\leq i,j\leq p $$ 记$R=(r_{ij})_{p\times p}$为样本相关系数矩阵。

### A. 样本相关系数的精确分布

考虑二元正态分布的情形: 精确分布假设总体$X\sim N_p(\mu,\Sigma)$，由性质3.2.7（边际分布：$X^{(1)}\sim N_q(\mu^{(1)},\Sigma_{11}),X^{(2)}\sim N_{p-q}(\mu^{(2)},\Sigma_{22})$）可知：$(X_1,X_2)'$服从二元正态分布: $$ \ \begin{pmatrix}X_1\\X_2\end{pmatrix}\sim N_2\left(\begin{pmatrix}\mu_1\\\mu_2\end{pmatrix},\begin{pmatrix}\sigma^2_1&\rho\sigma_1\sigma_2\\\rho\sigma_1\sigma_2&\sigma^2_2\end{pmatrix}\right) \\ \rho=\frac{Cov(X_1,X_2)}{\sigma_1\sigma_2},\sigma_1=\sqrt{Var(X_1)},\sigma_2=\sqrt{Var(X_2)} $$ 假设下面的样本来自二元分布总体$(X_1,X_2)'$： $$ \begin{pmatrix} x_{11}\\x_{12} \end{pmatrix},\begin{pmatrix} x_{21}\\x_{22} \end{pmatrix},\dots,\begin{pmatrix} x_{n1}\\x_{n2} \end{pmatrix} $$ 由这些样本可以定义样本离差阵: $$ V=\begin{pmatrix} v_{11}&v_{12}\\ v_{21}&v_{22} \end{pmatrix}=\begin{pmatrix} \sum^n_{i=1}(x_{i1}-\bar x_1)^2 &\sum^n_{i=1}(x_{i1}-\bar x_1)(x_{i2}-\bar x_2) \\ \sum^n_{i=1}(x_{i1}-\bar x_1)(x_{i2}-\bar x_2) &\sum^n_{i=1}(x_{i2}-\bar x_2)^2 \end{pmatrix} $$ 其中样本均值为$\bar x_1=\frac1n\sum^n_{i=1}x_{i1},\bar x_2=\frac1n\sum^n_{i=1}x_{i2}$.

**根据相关系数$\rho_{ij}$的极大似然估计即为样本相关系数：** $$ \hat\rho_{ij}=\frac{\sum^n_{k=1}(x_{ki}-\bar x_i)(x_{kj}-\bar x_j)}{\sqrt{\sum^n_{k=1}(x_{ki}-\bar x_i)^2\sum^n_{k=1}(x_{kj}-\bar x_j)^2}}\equiv r_{ij}\\ r=\frac{\sum^n_{k=1}(x_{k1}-\bar x_1)(x_{k2}-\bar x_2)}{\sqrt{\sum^n_{k=1}(x_{k1}-\bar x_1)^2\sum^n_{k=1}(x_{k2}-\bar x_2)^2}}=\frac{v_{12}}{\sqrt{v_{11}v_{22}}} $$ **样本相关系数r与分布的参数$\mu_1,\mu_2,\sigma_1\sigma_2$无关。**令： $$ u_{i1}=\frac{x_{i1}-\mu_1}{\sigma_1},\mu_{i2}=\frac{x_{i2}-\mu_{2}}{\sigma_2},i=1,2,\dots,n $$ 则$\begin{pmatrix} u_{11}\\u_{12} \end{pmatrix},\begin{pmatrix} u_{21}\\u_{22} \end{pmatrix},\dots,\begin{pmatrix} u_{n1}\\u_{n2} \end{pmatrix}$i.i.d.,$\sim N_2\left(\begin{pmatrix}0\\0\end{pmatrix},\begin{pmatrix}1&\rho\\\rho&1\end{pmatrix}\right)$.

则$x_{i1}=\mu_1+\sigma_1u_{i1},x_{i2}=\mu_2+\sigma_2u_{i2}$ : $$ r=\frac{\sum^n_{k=1}(x_{k1}-\bar x_1)(x_{k2}-\bar x_2)}{\sqrt{\sum^n_{k=1}(x_{k1}-\bar x_1)^2\sum^n_{k=1}(x_{k2}-\bar x_2)^2}}=\frac{\sum^n_{k=1}(u_{k1}-\bar u_1)(u_{k2}-\bar u_2)}{\sqrt{\sum^n_{k=1}(u_{k1}-\bar u_1)^2\sum^n_{k=1}(u_{k2}-\bar u_2)^2}}= $$ 所以, r 的分布与分布的参数$\mu_1,\mu_2,\sigma_1\sigma_2$无关，**只与$\rho$有关。**

不妨假设$\mu_1=\mu_2=0,\sigma_1=\sigma_2=1$，因为样本离差阵$V \sim W_2((n - 1), \Sigma)$，其中 $\Sigma = \left(\begin{array}{cc} 1 & \rho \\ \rho & 1 \end{array}\right)$. $$ V=\sum^n_{i=2}Y_iY_i'，Y=[Y_1,Y_2,\dots,Y_n]\\ v_{ij}=\sum^n_{k=2}y_{ki}y_{jk} $$ （$i=2$是因为n-1,去除一个第一列相关量）

再由Wishart分布的定义知，随机向量$(v_{xx}, v_{xy}, v_{yy})$的密度函数为: $$ \frac{(v_{xx}v_{yy}-v_{xy}^2)^{(n - 4)/2}}{2^{n - 1}\pi^{1/2}\Gamma\left(\frac{n - 1}{2}\right)\Gamma\left(\frac{n - 2}{2}\right)(1 - \rho^2)^{(n - 1)/2}}\exp\left\{-\frac{v_{xx}+v_{yy}-2\rho v_{xy}}{2(1 - \rho^2)}\right\} $$ 其中，$v_{xx}>0$，$v_{yy}>0$，$v_{xx}v_{yy}-v_{xy}^2>0$。

由变换$(v_{xx}, v_{xy}, v_{yy})\to(v_{xx}, v_{yy}, r)$导出$(v_{xx}, v_{yy}, r)$的密度函数，再对$v_{xx}$和$v_{yy}$积分后，可得$r$的密度函数为: $$ f(r|\rho, n)=\frac{2^{n - 3}(1 - \rho^2)^{(n - 1)/2}(1 - r^2)^{(n - 4)/2}}{\pi(n - 3)!}\sum_{k = 0}^{\infty}\frac{(2\rho r)^k}{k!}\Gamma^2\left(\frac{n + k - 1}{2}\right), \quad |r|<1 $$ 当$\rho = 0$时，即$X$与$Y$独立，样本相关系数$r$的密度函数为 : $$ f(r|n)=\frac{2^{n - 3}(1 - r^2)^{(n - 4)/2}}{\pi(n - 3)!}\Gamma^2\left(\frac{n - 1}{2}\right), \quad |r| < 1 $$ 因此，可以用此分布作为, 零假设为$X$与$Y$独立时的统计量$r$的零分布, 来检验零假设是否成立。

> (书P124-定理5.4.1)：假设$x_1,\dots,x_n$是来自p元正态分布$N_p(\mu,\Sigma)$的i.i.d.样本，如果$\rho_{ij}=0$，则样本相关系数$r$的密度函数为： $$ f(r|n)=\frac{2^{n - 3}(1 - r^2)^{(n - 4)/2}}{\pi(n - 3)!}\Gamma^2\left(\frac{n - 1}{2}\right), \quad |r| < 1 $$

### 应用：$\rho=0$的假设检验

> **检验问题**：(双侧检验：检验变量之间是否存在任何形式的相关性：正相关或负相关) $X$与$Y$独立
> 
> **等价于**： $$ H_0:\rho = 0,\quad v.s.\quad H_1:\rho \neq 0 $$

检验方案一： 计算出C，比较r与C的大小。

1.  给定显著性水平 $0 < \alpha < 0.5$（通常取为0.05）；
2.  计算临界值 $C > 0$，满足 $_{-C}^{C} f(r|n) , dr = 1 - ; $
3.  如果 $|r|=\frac{|v_{xy}|}{\sqrt{v_{xx}v_{yy}}}>C$，则拒绝零假设，即认为 $X$ 与 $Y$ 不独立。

检验方案二： 换另外一种方式来确定C：转换为查表计算的t值

通常采用统计量 $T = $作为检验$X$与$Y$是否独立的统计量。

将相关系数$r=\frac{v_{xy}}{\sqrt{v_{xx}v_{yy}}}$带入得： $$ T = \sqrt{n - 2} \cdot \frac{v_{xy}v_{xx}^{-1/2}}{\sqrt{v_{yy} - v_{xy}^2v_{xx}^{-1}}} $$

> 由Wishart分布的性质6( 独立分解性质 )知, 当$X$与$Y$独立，即$\rho = 0$时，有 :
> +   $v_{yy}-v_{xy}^2v_{xx}^{-1}$与$v_{xy}v_{xx}^{-1/2}$相互独立；
> +   $v_{yy}-v_{xy}^2v_{xx}^{-1}\stackrel{d}{\sim}\chi^2(n - 2)$；
> +   $v_{xy}v_{xx}^{-1/2}\stackrel{d}{\sim}N_1(0,1)$；
> t分布：$X\sim N_1(0,1), Y\sim \chi^2(n), t=\frac{X}{\sqrt{\frac{Y}n}}$为服从自由度为n的t分布。 $$ t=\frac{X}{\sqrt{\frac{Y}n}}\sim t(n) $$

在零假设($\rho=0$)下： $$ \begin{align} T &= \sqrt{n - 2} \cdot \frac{r}{\sqrt{1 - r^2}} = \frac{v_{xy}v_{xx}^{-1/2}}{\sqrt{\frac{v_{yy}-v_{xy}^2v_{xx}^{-1}}{n - 2}}}\\ &\stackrel{d}{=} \frac{N_1(0,1)}{\sqrt{\frac{\chi^2(n - 2)}{n - 2}}}\\ &\stackrel{d}{\sim}t(n - 2) \end{align} $$ 总结检验方案二： $$ H_0: \rho = 0, \quad v.s. \quad H_1: \rho \neq 0, $$
1.  给定显著性水平 $0 < \alpha < 0.5$;
2.  如果 $|T|>t_{1-\frac{\alpha}{2}}(n - 2)$，则拒绝零假设，即认为$X$与$Y$不独立， 其中$t_{1-\frac{\alpha}{2}}(n - 2)$是自由度为$(n - 2)$的标准$t$分布的$(1 - \frac{\alpha}{2})$分位点。

检验方案三：单侧正/负相关检验：检验变量之间是否存在**正/负相关**。

| **独立 vs 正相关**的检验问题 | **独立 vs 负相关**的检验问题 |
| --- | --- |
| $H_0: \rho = 0, \quad v.s. \quad H_1: \rho > 0$ | $H_0: \rho = 0, \quad v.s. \quad H_1: \rho < 0$ |
| 计算检验的$p$值: $p = P\{t(n - 2)\ge T\}$ | 计算检验的$p$值: $p = P\{t(n - 2)\le T\}$ |
| 如果$p$值小于显著性水平$\alpha$( $p<\alpha$ )，则拒绝零假设。 | 如果$p$值小于显著性水平$\alpha$( $p<\alpha$ )，则拒绝零假设。 |

**例子(栗子，吃一口)**

> 在Ch1中的栗子继续拿来讨论：
> ![image-20241205095330519](https://cdn.jsdelivr.net/gh/SchwertLin/Pic/img/image-20241205095330519.png)
> (1)变量$x_3$与$x_4$独立与正相关检验问题
> 检验统计量为 $$ \begin{align} T &= \sqrt{n - 2} \cdot \frac{r}{\sqrt{1 - r^2}} \\ &= \sqrt{13 - 2} \cdot \frac{0.030}{\sqrt{1 - 0.030^2}} \\ &=0.0995 \end{align} $$ 因此，变量$x_3$与$x_4$独立与正相关检验问题： $$ p = P\{t(11) \geq 0.0995\} = 0.4612 > 0.05, $$ 故而不能拒绝$x_3$与$x_4$之间的相互独立性。(接受$H_0$)
> 2.  变量$x_2$与$x_3$独立与负相关检验问题： $$ p = P\{t(11) \leq - 0.4655\} = 0.3253 > 0.05, $$ 则不能拒绝$x_2$与$x_3$之间的相互独立性。 (接受$H_0$)
> 3.  变量$y$与$x_3$独立与负相关检验问题： $$ p = P\{t(11) \leq - 2.1\} = 0.0298 < 0.05, $$ 则拒绝$y$与$x_3$之间的相互独立性，认为它们负相关。(拒绝$H_0$)

### B. 样本相关系数的渐近分布（总体不服从正态分布）

注意到，样本相关系数$r$可以改写成

| $v_{xy}$                                                                                                                                                                                                                                                                                                                                                                                                                                                  | $v_{xx}$                                                                                                                                                                                                                                                                                                                                                                                                                             | $v_{yy}$                                                                                                                                                                                                                                                                                                                                                                                                                             |
| --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| $\begin{align} v_{xy} &= \frac{1}{n} \sum_{i=1}^{n} (x_i - \bar{x})(y_i - \bar{y}) \\ &= \frac{1}{n} \sum_{i=1}^{n} x_i y_i - \frac{1}{n} \sum_{i=1}^{n} x_i \bar{y} - \frac{1}{n} \sum_{i=1}^{n} y_i \bar{x} + \frac{1}{n} \sum_{i=1}^{n} \bar{x} \bar{y} \\ &= \frac{1}{n} \sum_{i=1}^{n} x_i y_i - \bar{x} \bar{y} - \bar{y} \bar{x} + \bar{x} \bar{y} \\ &= \frac{1}{n} \sum_{i=1}^{n} x_i y_i - \bar{x} \bar{y} \\ &= t_5 - t_1 t_2 \end{align}$ | $\begin{align}v_{xx}&= \frac{1}{n} \sum_{i=1}^{n} (x_i - \bar{x})^2 \\&= \frac{1}{n} \sum_{i=1}^{n} (x_i^2 - 2 x_i \bar{x} + \bar{x}^2) \\&= \frac{1}{n} \sum_{i=1}^{n} x_i^2 - 2 \bar{x} \cdot \frac{1}{n} \sum_{i=1}^{n} x_i + \frac{1}{n} \sum_{i=1}^{n} \bar{x}^2 \\&= \frac{1}{n} \sum_{i=1}^{n} x_i^2 - 2 \bar{x} \cdot \bar{x} + \bar{x}^2 \\&= \frac{1}{n} \sum_{i=1}^{n} x_i^2 - \bar{x}^2 \\&= t_3 - t_1^2\end{align}$ | $\begin{align}v_{yy}&= \frac{1}{n} \sum_{i=1}^{n} (y_i - \bar{y})^2 \\&= \frac{1}{n} \sum_{i=1}^{n} (y_i^2 - 2 y_i \bar{y} + \bar{y}^2) \\&= \frac{1}{n} \sum_{i=1}^{n} y_i^2 - 2 \bar{y} \cdot \frac{1}{n} \sum_{i=1}^{n} y_i + \frac{1}{n} \sum_{i=1}^{n} \bar{y}^2 \\&= \frac{1}{n} \sum_{i=1}^{n} y_i^2 - 2 \bar{y} \cdot \bar{y} + \bar{y}^2 \\&= \frac{1}{n} \sum_{i=1}^{n} y_i^2 - \bar{y}^2 \\&= t_4 - t_2^2\end{align}$ |

$$ r = \frac{v_{xy}}{\sqrt{v_{xx}v_{yy}}}= \frac{t_5 - t_1 t_2}{\sqrt{t_3 - t_1^2} \cdot \sqrt{t_4 - t_2^2}} = g(t_1, t_2, t_3, t_4, t_5)\\ \begin{cases} t_1 = n^{-1} \sum_{i = 1}^{n} x_i, \\ t_2 = n^{-1} \sum_{i = 1}^{n} y_i,\\ t_3 = n^{-1} \sum_{i = 1}^{n} x_i^2,\\ t_4 = n^{-1} \sum_{i = 1}^{n} y_i^2,\\ t_5 = n^{-1} \sum_{i = 1}^{n} x_iy_i. \end{cases} $$

记随机变量序列$z_i=(x_i,y_i,x_i^2,y_i^2,x_iy_i)'$，$1\leq i\leq n$， 并令： $$ \bar{Z} = n^{-1}\sum_{i = 1}^{n}z_i=(t_1,t_2,t_3,t_4,t_5)'. $$ 由于$z_{1},\cdots,z_{n}$ i.i.d.，因此由独立同分布随机变量和的中心极限定理知：

> 当样本量 $n$ 增加时，样本均值向量 $\bar{\mathbf{Z}}$ 的分布会趋近于多元正态分布，无论原始随机向量 $\mathbf{Z}_i$ 的分布形态如何，前提是每个 $\mathbf{Z}_i$ 有有限的期望和协方差。
> **定理（多元中心极限定理）**： 设 $\{ \mathbf{Z}_i \}_{i=1}^n$ 是一组相互独立且同分布（i.i.d.）的 p维随机向量，具有期望向量$ = E(*i) $和协方差矩阵 $\boldsymbol{\Sigma} = \text{Cov}(\mathbf{Z}_i)$。当 n 足够大时，标准化的样本均值向量$\sqrt{n} (\bar{\mathbf{Z}} - \boldsymbol{\mu})$近似服从多元正态分布 $N_p(\mathbf{0}, \boldsymbol{\Sigma})$，即 $$ \sqrt{n} (\bar{\mathbf{Z}} - \boldsymbol{\mu}) \xrightarrow{d} N_p(\mathbf{0}, \boldsymbol{\Sigma}) $$ 其中，${} =* {i=1}^n _i $是样本均值向量。
> **引入渐进分布：**
> 令：$c_{ij}(n)=\frac{v_{ij}(n)}{\sqrt{\sigma_{ii}(n)\sigma_{jj}(n)}}$，$c_{ij}(n)$是经过标准化的协方差项，$v_{ij}(n)$是样本协方差，$\sigma_{ii}(n),\sigma_{jj}(n)$是样本方差。
> 令$U(n)=\frac1n\begin{pmatrix}c_{ii}(n)\\c_{jj}(n)\\c_{ij}(n)\end{pmatrix},c_{ij}(n)=\frac{v_{ij}(n)}{\sqrt{\sigma_{ii}(n)\sigma_{jj}(n)}},b=\begin{pmatrix}1\\1\\\rho\end{pmatrix}$，
> 给出$\sqrt{n}(U(n)-b)\overset{d}{\rightarrow}N_3(0,\Sigma),n\rightarrow\infty$.这个$B_n$分布的均值为0，协方差为$E(b_{ij}b_{st})=\sigma_{is}\sigma_{jt}+\sigma_{it}\sigma_{js}$. $$ \Sigma=\begin{pmatrix}2&2\rho^2&2\rho\\2\rho^2&2&2\rho\\2\rho&2\rho&1+\rho^2\end{pmatrix} $$
> **(书p133 定理5.4.3)** 令$\{U(n)\}$是一列p维的随机向量，b是一个p维固定向量，当$n\rightarrow\infty$,使得$\sqrt{n}(U(n)-b)\overset{d}{\rightarrow}N_p(0,\Sigma)$, 此处$0_{p\times 1}, \Sigma_{p\times p}$.
> 假设$f(u)$是一个向量值函数，其中每个分量$f_j(u)$在$u=b$处有非零矩阵，定义矩阵$\Phi_b$，其$(i,j)$元素为$\frac{\partial f_j(u)}{\partial u_i}|_{u=b}$. 当$n\rightarrow\infty$,使得: $$ \sqrt{n}[f(U(n))-f(b)]\overset{d}{\rightarrow}N_m(0,\Phi_b'\Sigma\Phi_b) $$ 上面的$r = \frac{v_{xy}}{\sqrt{v_{xx}v_{yy}}}= \frac{t_5 - t_1 t_2}{\sqrt{t_3 - t_1^2} \cdot \sqrt{t_4 - t_2^2}} = g(t_1, t_2, t_3, t_4, t_5)$的计算有些复杂，换一个$r=\frac{u_3}{\sqrt{u_1u_2}}$来验证一下这个定理： $$ \begin{align} &r=\frac{u_3}{\sqrt{u_1u_2}}\\ &\frac{\partial r}{\partial u_1}|_{u=b}=-\frac 1 2 u_3u_2 (u_1u_2)^{-\frac 3 2}\\ &\frac{\partial r}{\partial u_2}|_{u=b}=-\frac 1 2 u_3u_1 (u_1u_2)^{-\frac 3 2}\\ &\frac{\partial r}{\partial u_3}|_{u=b}=(u_1u_2)^{-\frac 1 2}\\ &f(b)=f(\begin{pmatrix}1\\1\\\rho\end{pmatrix})=\rho代入：\\ &\frac{\partial r}{\partial u_1}|_{u=b}=-\frac 1 2\rho\\ &\frac{\partial r}{\partial u_2}|_{u=b}=-\frac 1 2\rho\\ &\frac{\partial r}{\partial u_3}|_{u=b}=1\\ \end{align} $$ $\Phi_b'\Sigma\Phi_b=\begin{pmatrix}-\frac 1 2\rho&-\frac 1 2\rho&1\end{pmatrix}\begin{pmatrix}2&2\rho^2&2\rho\\2\rho^2&2&2\rho\\2\rho&2\rho&1+\rho^2\end{pmatrix}\begin{pmatrix}-\frac 1 2\rho\\-\frac 1 2\rho\\1\end{pmatrix}=(1-\rho^2)^2$

让我们回到：$r = \frac{v_{xy}}{\sqrt{v_{xx}v_{yy}}}= \frac{t_5 - t_1 t_2}{\sqrt{t_3 - t_1^2} \cdot \sqrt{t_4 - t_2^2}} = g(t_1, t_2, t_3, t_4, t_5)$: $$ \sqrt{n}(\bar{Z}-\mu_Z)\stackrel{d}{\rightarrow}N_5(0,\Sigma_Z)\\ \mu_Z = E(z_1)=\begin{pmatrix} 0\\ 0\\ 1\\ 1\\ \rho \end{pmatrix}, \Sigma_Z = \text{Cov}(z_1)=\begin{pmatrix} 1 & \rho & 0 & 0 & 3\rho\\ \rho & 1 & 0 & 0 & 3\rho\\ 0 & 0 & 2\rho^2 & 2\rho^2 & 2\rho\\ 0 & 0 & 2\rho^2 & 2\rho^2 & 2\rho\\ 3\rho & 3\rho & 2\rho & 2\rho & 1+\rho^2 \end{pmatrix} $$
此时有将统计量$\bar{Z}$映射到$r$上的变换g，其中g是在期望处可微。 $$ \begin{cases} g(\bar{Z}) = g(t_1, t_2, t_3, t_4, t_5) = r\\ g(\mu_Z) = \rho \end{cases} $$ 再由Cramér定理（定理5.4.3），可得样本相关系数$r$的渐近分布： $$ \begin{align} \sqrt{n}(r - \rho) &= \sqrt{n}(g(\bar{Z}) - g(\mu_Z)) \\&\stackrel{d}{\rightarrow} N(0, (g'(\mu_Z))'\Sigma_Z g'(\mu_Z))\\ &\stackrel{d}{\rightarrow} N(0, (1 - \rho^2)^2) \end{align} $$ 其中$g'$是$g$的一阶偏导。 注意：上面的结论与$\rho$是否为0无关。

> **Q: Cramer定理？（Delta方法）**
> A: 在上面定理5.4.3有提到，总的来说，假设我们有一个大样本的均值向量$\bar Z$,且它的分布趋近于正态分布（由中心极限定理可以得到），那么这个均值向量$\bar Z$可以应用一个可微函数$g(\cdot)$ ，经过变换后的量$g(\bar Z)$也会趋于正态分布。

## C. 置信区间(区间估计)

> 由于样本相关系数的精确分布不是分布自由的，即与未知的总体相关系数$\rho$有关，因此无法用于置信区间的构造。

因此使用其渐近分布构造总体相关系数$\rho$的区间估计。**但是渐进方差$\sigma^2=(1-\rho^2)^2$包含未知参数$\rho$**, 因此很难直接利用渐进正态分布来构造$\rho$的置信区间。为解决这个问题，采用下面两种方法。

### (1) plug-in插入方法

既然渐进方差$\sigma^2=(1-\rho^2)^2$包含未知参数$\rho$, 可用其极大似然估计$r(n)$进行替换。

当$n\rightarrow\infty$，可以证明$r(n)\overset{P}{\rightarrow}\rho$, 然后由Slutsky定理有： $$ \frac{\sqrt{n}[r(n)-\rho]}{1-r^2(n)}=\frac{\sqrt{n}[r(n)-\rho]}{1-\rho^2}\frac{1-\rho^2}{1-r^2(n)}\stackrel{d}{\rightarrow} N(0, 1),n\rightarrow \infty $$ 因此，总体相关系数$\rho$的置信水平为$(1 - \alpha)$的区间估计为 ： $$ \left[r - \frac{(1 - r^2)Z_{1 - \alpha/2}}{\sqrt{n}}, r + \frac{(1 - r^2)Z_{1 - \alpha/2}}{\sqrt{n}}\right] $$ 其中$Z_{1 - \alpha/2}$是标准正态分布的$(1 - \alpha/2)$分位点。

### 置信区间的统计意义

记： $Pr$表示概率。 $$ C_L = r - n^{-1/2}(1 - r^2)Z_{1-\alpha/2}\\ C_U = r + n^{-1/2}(1 - r^2)Z_{1-\alpha/2} $$ $$ \begin{align} \Pr\{C_L \leq \rho \leq C_U\} &= \Pr\left\{\left|\frac{\sqrt{n}(r - \rho)}{1 - r^2}\right| \leq Z_{1-\alpha/2}\right\}\\ &\approx \Pr\{|N(0, 1)| \leq Z_{1-\alpha/2}\}\\ &= 1 - \alpha \end{align} $$

**是栗子，我们有救了**

![image-20241206112623399](https://cdn.jsdelivr.net/gh/SchwertLin/Pic/img/image-20241206112623399.png)

1.  变量$x_3$与$x_4$的相关系数$\rho_{34}$的置信区间: $$ \begin{align} C_L &= r - n^{-1/2}(1 - r^2)Z_{1 - \alpha/2} \\ & = 0.030 - 13^{-1/2}(1 - 0.030^2) \times 1.96 \\ &= -0.513\\ C_U& = r + n^{-1/2}(1 - r^2)Z_{1 - \alpha/2} \\ &= 0.030 + 13^{-1/2}(1 - 0.030^2) \times 1.96\\ &= 0.573 \end{align} $$

  
| 变量 | 置信区间 | 相互独立性 |
| --- | --- | --- |
| 变量$x_3$与$x_4$的相关系数$\rho_{34}$ | $[-0.513, 0.573]$ | 0在此区间里，故不能拒绝$x_3$与$x_4$之间的相互独立性。 |
| 变量$x_2$与$x_3$的相关系数$\rho_{23}$ | $[-0.672, 0.394]$ | 0在此区间里，故也不能拒绝$x_2$与$x_3$之间的相互独立性。 |
| 变量$x_1$与$x_3$的相关系数$\rho_{13}$ | $[-0.999, -0.650]$ | 0不在此区间里，故不能认为$x_1$与$x_3$之间是相互独立的。 |

### (2) 方差齐性变换(Fisher Z变换)

求函数$f$, 使得$f(r(n))$的渐进方差为1，即： $$ \sqrt{n}[f(r(n))-f(\rho)]\overset{d}{\rightarrow}N(0,1) $$ $$ \sqrt{n}[f(r(n))-f(\rho)]\overset{d}{\rightarrow}N(0,(f'(\rho))^2(1-\rho^2)^2)\\ $$ 所以：$(f'(\rho))^2(1-\rho^2)^2=1$，通过这个计算出函数式子为：$f(\rho)=\frac12\ln\frac{1-\rho}{1+\rho}$,代入上式： $$ \sqrt{n} \left( \frac{1}{2} \ln \frac{1 + r}{1 - r} - \frac{1}{2} \ln \frac{1 + \rho}{1 - \rho} \right) \stackrel{d}{\rightarrow} N(0, 1) $$ 由上式可以构造$\frac{1}{2} \ln \frac{1 + \rho}{1 - \rho}$置信水平为$1-\alpha$的置信区间为： $$ \left[\frac12\ln\frac{1+r(n)}{1-r(n)}]-\frac{1}{\sqrt{n}}z_{1-\alpha/2},\frac12\ln\frac{1+r(n)}{1-r(n)}]+\frac{1}{\sqrt{n}}z_{1-\alpha/2}\right] $$ 为构造$\rho$的置信区间，对上面的置信区间进行变换，可得到$\rho$的置信水平为$1-\alpha$的置信区间为 $$ \left[ \frac{\frac{1 + r}{1 - r}e^{-a}-1}{\frac{1 + r}{1 - r}e^{-a}+1}, \frac{\frac{1 + r}{1 - r}e^{a}-1}{\frac{1 + r}{1 - r}e^{a}+1} \right] ,a = \frac{2}{\sqrt{n}}Z_{1 - \alpha/2} $$ 称$Z = \frac{1}{2} \ln \frac{1 + r}{1 - r}$为Fisher的$Z$变换。**通常使用Fisher Z变换方法构造$\rho$的置信区间**。

**栗子**

水泥在凝固时释放的热量与水泥中化学成分的关系案例(续) 设定置信水平$1-\alpha = 0.95$。

> 变量$x_3$与$x_4$的相关系数$\rho_{34}$的置信区间的计算： $$ \left[ \frac{\frac{1 + 0.030}{1 - 0.030}e^{-a}-1}{\frac{1 + 0.030}{1 - 0.030}e^{-a}+1}, \frac{\frac{1 + 0.030}{1 - 0.030}e^{a}-1}{\frac{1 + 0.030}{1 - 0.030}e^{a}+1} \right] = [-0.237, 0.293] $$ 其中$a = \frac{2}{\sqrt{n}}Z_{1-\alpha/2} = \frac{2}{\sqrt{13}} \cdot 1.96 = 1.0872$。

| 变量                            | 置信区间               |
| ----------------------------- | ------------------ |
| 变量$x_3$与$x_4$的相关系数$\rho_{34}$ | $[-0.237, 0.293]$  |
| 变量$x_2$与$x_3$的相关系数$\rho_{23}$ | $[-0.390, 0.131]$  |
| 变量$x_1$与$x_3$的相关系数$\rho_{13}$ | $[-0.894, -0.716]$ |

注意：置信区间变窄。

## 3.2.3 正态总体均值的置信域估计

## A.单总体

设$x_1,\dots,x_n$是来自p元正态总体$N_p(\mu,\Sigma)$的随机样本，其中$\mu\in\mathbb{R}^p,\Sigma>0,n>p$. 上面给出了总体均值向量$\mu$和总体协方差矩阵$\Sigma$的无偏估计分别是样本均值向量$\bar x$和样本协方差矩阵$S$. **下面讨论$\mu$的置信域估计问题，分别在总体协方差阵$\Sigma$已知和未知的两种情况下讨论。**

### $\boldsymbol{\Sigma}$已知

如果总体协方差矩阵 $\Sigma$ 已知，样本均值向量 $\bar{x}$的分布可以通过标准化后的形式来推导出： $$ n(\bar{\mathbf{X}} - \boldsymbol{\mu})'\boldsymbol{\Sigma}^{-1}(\bar{\mathbf{X}} - \boldsymbol{\mu}) \stackrel{d}{\rightarrow} \chi^2(p) $$ 则$\boldsymbol{\mu}$的水平为$(1 - \alpha)$的置信域估计为： $$ D = \left\{\boldsymbol{\mu} \in \mathbb{R}^p : n(\bar{\mathbf{X}} - \boldsymbol{\mu})'\boldsymbol{\Sigma}^{-1}(\bar{\mathbf{X}} - \boldsymbol{\mu}) \leq \chi^2_{1 - \alpha}(p)\right\} $$ 即有 $\Pr\{\boldsymbol{\mu} \in D\} = 1 - \alpha$. 意味着在大量的重复实验中，置信域 $D$将包含真实总体均值 $\mu$的概率为 $1 - \alpha$。

> **Q: $\chi^2$分布与置信域的联系？**
> 
> A: 具体来说，样本均值 $\bar{x}$ 和总体均值 $\mu$ 之间的偏差经过标准化后（即通过协方差矩阵的逆来标准化）符合 $^2(p) $分布。这意味着，我们可以通过卡方分布的分位点来构建置信区间。
> 
> 置信域 D中$^2_{1 - }(p) $是卡方分布自由度为 $p$ 时，置信度为 $(1 - \alpha)$ 的分位点。这表示总体均值 $\mu$ 在给定的样本数据下落入该置信域的概率为 $1 - \alpha$。

### $\Sigma$未知

因为$\Sigma$我们无从得知，所以使用$\Sigma$的无偏估计$S=\frac 1{n-1}V$来代替。令 ： $$ \begin{align} T^2 &= n(\bar{X} - \mu)'S^{-1}(\bar{X} - \mu)\\ &=n(n - 1)(\bar{X} - \mu)'V^{-1}(\bar{X} - \mu)\\ &\sim T^2_p(n-1) \end{align} $$

> 由正态样本统计量的性质知 ：$\sqrt{n}(\bar{X} - \mu) \stackrel{d}{\rightarrow} N(0, \Sigma)$, $V \stackrel{d}{\rightarrow} W_p(n - 1, \Sigma)$, 且${X} $与$V$独立.
> 
> Hotelling $T^2$分布性质如下：
> 
>  
> | 性质 | 说明 |
> | --- | --- |
> | 1. | $X'W^{-1}X \stackrel{d}{=} \frac{\chi^2(p)}{\chi^2(n - p + 1)}$,其中分子分母相互独立； |
> | 2. | $\frac{n - p + 1}{np}T_p^2(n) \stackrel{d}{=} \frac{\chi^2(p)/p}{\chi^2(n - p + 1)/(n - p + 1)} \stackrel{d}{\sim} F(p,(n - p + 1))$ |

因此有： $$ T^2 = (n - 1)(\sqrt{n}(\bar{X} - \mu))'V^{-1}(\sqrt{n}(\bar{X} - \mu)) \stackrel{d}{\rightarrow} T_p^2(n - 1) $$ $$ \frac{1}{n - 1}T^2 = n(\bar{X} - \mu)'V^{-1}(\bar{X} - \mu) \stackrel{d}{\rightarrow} \frac{\chi^2(p)}{\chi^2(n-p)} $$ $$ \frac{n - p}{(n - 1)p}T^2 \stackrel{d}{\rightarrow} \frac{\chi^2(p)/p}{\chi^2(n - p)/(n - p)} \stackrel{d}{\rightarrow} F(p, n - p) $$ 则当$\boldsymbol{\Sigma}$未知时，$\boldsymbol{\mu}$的水平为$(1 - \alpha)$的置信域估计为 : $$ D = \left\{\boldsymbol{\mu} \in \mathbb{R}^p : \frac{n(n - p)}{p}(\bar{X} - \boldsymbol{\mu})'V^{-1}(\bar{X} - \boldsymbol{\mu}) \leq F_{1 - \alpha}(p, n - p)\right\} $$ 即有 $\Pr\{\boldsymbol{\mu} \in D\} = 1 - \alpha$.

> PS: 因为这个置信域D是一个二次型，那么上述的不等式就是对这个二次型的约束，所以，这个**置信域是一个超椭球。**
> +   协方差矩阵 $V$ 的逆 $V^{-1}$ 定义了椭球的方向和形状，特征值决定了每个方向上的伸缩因子。
> +   $F$分布的临界值 $F_{1-\alpha}(p, n-p)$ 确定了超椭球的大小。

## B.两总体

设独立总体$X \stackrel{d}{\sim} N_p(\boldsymbol{\mu}_1, \boldsymbol{\Sigma})$，$Y \stackrel{d}{\sim} N_p(\boldsymbol{\mu}_2, \boldsymbol{\Sigma})$，$\boldsymbol{\mu}_1, \boldsymbol{\mu}_2 \in \mathbb{R}^p$，$\boldsymbol{\Sigma}>0$。 (*属于同一维度空间，但分布不同。*)

记 $\mathbf{X} = (X_1, \cdots, X_m)$，$\mathbf{Y} = (Y_1, \cdots, Y_n)$分别为来自总体$X$和$Y$的样本，$\min\{m, n\} > p$。 我们要构造总体均值差$\boldsymbol{\delta} = \boldsymbol{\mu}_1 - \boldsymbol{\mu}_2$的置信域估计。

已知：

 
| 已知条件 | 对应公式 |
| --- | --- |
| 样本X的样本离差阵和协方差矩阵 | $V_1=\sum^n_{i=1}(x_i-\bar x)(x_i-\bar x)',S_1=\frac1{n-1}V_1$ |
| 样本Y的样本离差阵和协方差矩阵 | $V_2=\sum^n_{i=1}(y_i-\bar y)(y_i-\bar y)',S_2=\frac1{n-1}V_2$ |

我们下面讨论的问题是：

1.  $\Sigma_1=\Sigma_2=\Sigma$: ①$\Sigma$未知，②$\Sigma$已知
2.  $\Sigma_1\neq\Sigma_2$（**这种情况在本课程中不涉及，下面也不会涉及**）

因此下面对于$\Sigma$未知、$\Sigma$已知的考虑的前提是$\Sigma_1=\Sigma_2=\Sigma$.

### $\Sigma$已知

由$\bar{X} \stackrel{d}{\sim} N_p(\boldsymbol{\mu}_1, \boldsymbol{\Sigma}/m)$，$\bar{Y} \stackrel{d}{\sim} N_p(\boldsymbol{\mu}_2, \boldsymbol{\Sigma}/n)$，有: $$ (\bar X-\bar Y)\overset{d}{\sim}N_p(\delta,(\frac1m+\frac1n)\Sigma)=N_p(\delta,\frac{mn}{m + n}\Sigma) $$

> 根据二次型的性质：$X\sim N_p(\mu,\Sigma),\Sigma>0$,假设有个p阶方阵 $A\ge0$,则有$(X-\mu)'A(X-\mu)\sim\chi^2_m,m=tr(A\Sigma)$. 当$A=\Sigma^{-1}$时, $(X-\mu)'A(X-\mu)\sim\chi^2_p$.

$$ \frac{mn}{m + n}((\bar{X} - \bar{Y}) - \delta)'\Sigma^{-1}((\bar{X} - \bar{Y}) - \delta) \stackrel{d}{\rightarrow} \chi^2(p) $$

由此得到$\delta$的水平为$(1 - \alpha)$的置信域估计为: $$ D = \left\{\delta \in \mathbb{R}^p : \frac{mn}{m + n}((\bar{X} - \bar{Y}) - \delta)'\Sigma^{-1}((\bar{X} - \bar{Y}) - \delta) \leq \chi^2_{1 - \alpha}(p)\right\}. $$

### $\Sigma$未知

记$V_X$和$V_Y$分别为总体$X$和$Y$的样本离差阵。

由$X$和$Y$的联合密度函数: $$ \begin{align} &(2\pi)^{-(m + n)p/2}|\boldsymbol{\Sigma}|^{-(m + n)/2} \cdot \\ &\exp\left\{-\frac{1}{2}\text{tr}[\boldsymbol{\Sigma}^{-1}(V_X + V_Y + m(\bar{X}-\boldsymbol{\mu}_1)(\bar{X}-\boldsymbol{\mu}_1)' + n(\bar{Y}-\boldsymbol{\mu}_2)(\bar{Y}-\boldsymbol{\mu}_2)')]\right\} \end{align} $$ 知$(\boldsymbol{\mu}_1,\boldsymbol{\mu}_2,\boldsymbol{\Sigma})$的极大似然估计为$(\bar{X},\bar{Y},(V_X + V_Y)/(m + n))$。

记$V = V_X + V_Y$，并令 : $$ T^2 = \frac{mn(m + n - 2)}{m + n}((\bar{X}-\bar{Y})-\boldsymbol{\delta})'V^{-1}((\bar{X}-\bar{Y})-\boldsymbol{\delta}) $$ 由于$(\bar{X}-\bar{Y})$与$V$相互独立，且 $$ \sqrt{\frac{mn}{m + n}}((\bar{X}-\bar{Y})-\boldsymbol{\delta}) \stackrel{d}{\rightarrow} N_p(0,\boldsymbol{\Sigma}), \quad V \stackrel{d}{\rightarrow} W_p(m + n - 2,\boldsymbol{\Sigma})\\ T^2 \stackrel{d}{\rightarrow} T_p^2(m + n - 2) $$ 进而可知 $$ \begin{align} &\frac{m + n - p - 1}{(m + n - 2)p}T^2 \\ &= \frac{(m + n - p - 1)mn}{(m + n)(m + n - 2)p}((\bar{X}-\bar{Y})-\boldsymbol{\delta})'V^{-1}((\bar{X}-\bar{Y})-\boldsymbol{\delta}) \\ &\stackrel{d}{\sim} F(p,m + n - p - 1) \end{align} $$ 由此得到$\boldsymbol{\delta}$的水平为$(1 - \alpha)$的置信域估计为 $$ D = \left\{ \boldsymbol{\delta} \in \mathbb{R}^p :\begin{align} \frac{(m + n - p - 1)mn}{(m + n)p}((\bar{X} - \bar{Y}) - \boldsymbol{\delta})'V^{-1}((\bar{X} - \bar{Y}) - \boldsymbol{\delta})\\ \leq F_{1 - \alpha}(p, m + n - p - 1)\end{align} \right\} $$

## 3.2.4 正态总体均值的Bayes估计

> Bayes方法两要素：
> 
> 1.  样本的密度函数形式已知、只是参数未知.
> 2.  参数也被视为随机变量，其密度函数（先验密度）完全确定.
> 
> 先验密度如何确定？
> 
> 3.  专业知识和专家经验.
> 4.  数学方法，如：共轭先验、Jeffery先验、无信息先验等.

### A. Bayes推断

基于后验密度（分布）： **后验密度 ∝ 似然函数 × 先验密度**

+   数据(样本)的似然函数为给定参数下的条件密度：$f(X|\theta)$
+   数据(样本)和参数的联合密度：$h(X, \theta)=f(X|\theta)\pi(\theta)$
+   数据(样本)的边缘密度：$H(X)=\int f(X|\theta)\pi(\theta)d\theta$
+   Bayes后验密度为给定数据(样本)下参数的条件密度： $p(\theta|X)=\frac{h(X, \theta)}{H(X)}=\frac{f(X|\theta)\pi(\theta)}{H(X)} \propto f(X|\theta)\pi(\theta)$.

$$ p(\theta|X)=\frac{h(X, \theta)}{H(X)}=\frac{f(X|\theta)\pi(\theta)}{H(X)} \propto f(X|\theta)\pi(\theta) $$

**逆Wishart分布**

若$X^{-1} \stackrel{d}{\sim} W_p(n, \boldsymbol{\Sigma})$，则称随机矩阵$X$服从逆Wishart分布，记为$X \stackrel{d}{\sim} IW_p(n, \boldsymbol{\Sigma}^{-1})$，$\boldsymbol{\Sigma}>0$。

逆Wishart分布的密度函数 : $$ f_p(X)=\frac{|\boldsymbol{\Sigma}|^{-n/2}|X|^{-(n + p + 1)/2} \exp \left\{-\frac{1}{2} \text{tr}(\boldsymbol{\Sigma}^{-1} X^{-1})\right\}}{2^{(np/2)} \Gamma_p\left(\frac{n}{2}\right)}, \quad X>0 $$

**多元正态分布参数$(\boldsymbol{\mu}, \boldsymbol{\Sigma})$的先验分布** $$ \begin{cases} \boldsymbol{\Sigma} \stackrel{d}{\sim} IW_p(\alpha, T) \\ \text{在} \boldsymbol{\Sigma} \text{给定的条件下}, \boldsymbol{\mu} \stackrel{d}{\sim} N_p(\boldsymbol{\theta}, k^{-1} \boldsymbol{\Sigma}) \end{cases} $$ 其中，$\alpha, T, \boldsymbol{\theta}$和$k$为超参数。

**后验密度** $$ \pi_1(\boldsymbol{\Sigma} | \mathbf{X})=\frac{\left|\mathbf{T}_{n}\right|^{\alpha_{n} / 2}|\boldsymbol{\Sigma}|^{-\left(\alpha_{n}+p+1\right) / 2} \exp \left\{-\frac{1}{2} \operatorname{tr}\left(\mathbf{T}_{n} \boldsymbol{\Sigma}^{-1}\right)\right\}}{2^{\left(\alpha_{n} p / 2\right)} \pi^{p(p - 1) / 4} \prod_{i = 1}^{p - 1} \Gamma\left(\frac{\alpha_{n}-i + 1}{2}\right)}=I W_{p}\left(\alpha_{n}, \mathbf{T}_{n}\right) \\ \pi_2(\boldsymbol{\mu} | \boldsymbol{\Sigma}, \mathbf{X})=\frac{(2 \pi)^{-p / 2}|\boldsymbol{\Sigma}|^{-1 / 2} \exp \left\{-\frac{k n}{2(k + n)}(\boldsymbol{\mu}-\boldsymbol{\theta}_{n})^{\prime} \boldsymbol{\Sigma}^{-1}(\boldsymbol{\mu}-\boldsymbol{\theta}_{n})\right\}}{(2 \pi)^{p / 2}|\boldsymbol{\Sigma}|^{-1 / 2}}=N_{p}\left(\boldsymbol{\theta}_{n}, k_{n}^{-1} \boldsymbol{\Sigma}\right) $$ 其中， $$ \alpha_{n}=n+\alpha, \quad \mathbf{T}_{n}=\mathbf{T}+\mathbf{V}+\frac{k n(\overline{\mathbf{X}}-\boldsymbol{\theta})(\overline{\mathbf{X}}-\boldsymbol{\theta})^{\prime}}{k + n}\\ \boldsymbol{\theta}_{n}=\frac{n \overline{\mathbf{X}}+k \boldsymbol{\theta}}{n + k}, \quad k_{n}=n + k $$ 因此，该先验分布是共轭先验分布。

> 注：后验密度（分布）的形式一般都比较复杂，通常采用Markov chain Monte Carlo方法来计算。

**Bayes估计**

+   Bayes估计 = 参数的后验均值
+   $\mu$的Bayes估计：$\hat{\mu}_B = \boldsymbol{\theta}_n$
+   $\boldsymbol{\Sigma}$的Bayes估计：$\hat{\boldsymbol{\Sigma}}_B=\frac{\mathbf{T}_n}{\alpha_n - p - 1}$ (性质8)

## 作业1

设$X_1,\dots,X_n$,i.i.d.$\sim N_p(\mu,\Sigma)$, $\mu$已知, $\Sigma>0$未知. 求$\Sigma$的极大似然估计.

> 首先，我们知道这个答案是$S=\frac1{n-1}V$(雾)，然后开始写...

对于每个样本 $X_i \in \mathbb{R}^p$，其概率密度函数为：

$$ f(X_i; \mu, \Sigma) = \frac{1}{(2\pi)^{p/2} |\Sigma|^{1/2}} \exp\left( -\frac{1}{2} (X_i - \mu)' \Sigma^{-1} (X_i - \mu) \right) $$ 由于 $X_1, X_2, \dots, X_n$ 是独立同分布的，因此样本的联合密度函数为： $$ L(\Sigma; X_1, X_2, \dots, X_n) = \prod_{i=1}^n f(X_i; \mu, \Sigma)\\ L(\Sigma; X_1, X_2, \dots, X_n) = \prod_{i=1}^n \frac{1}{(2\pi)^{p/2} |\Sigma|^{1/2}} \exp\left( -\frac{1}{2} (X_i - \mu)' \Sigma^{-1} (X_i - \mu) \right)\\ \ell(\Sigma; X_1, X_2, \dots, X_n) = \log L(\Sigma; X_1, X_2, \dots, X_n)\\ \ell(\Sigma; X_1, X_2, \dots, X_n) = -\frac{np}{2} \log(2\pi) - \frac{n}{2} \log|\Sigma| - \frac{1}{2} \sum_{i=1}^n (X_i - \mu)' \Sigma^{-1} (X_i - \mu)\\ $$ 为了求 $\Sigma$ 的极大似然估计 $\hat{\Sigma}$，我们对对数似然函数 $\ell(\Sigma)$ 关于 $\Sigma$ 求导数，并令其等于零。

> $$ \frac{\partial}{\partial \Sigma} \log|\Sigma| = \Sigma^{-1}\\ \frac{\partial}{\partial \Sigma} \left( a \Sigma^{-1} b \right) = -\Sigma^{-1} a b' \Sigma^{-1} $$

$$ \begin{align} \frac{\partial\ell}{\partial\Sigma}&=-\frac n2\Sigma^{-1}+\frac{1}{2}\sum^n_{i=1}\Sigma^{-1}(X_i-\mu)(X_i-\mu)'\Sigma^{-1}=0\\ n\Sigma^{-1}&=\sum^n_{i=1}\Sigma^{-1}(X_i-\mu)(X_i-\mu)'\Sigma^{-1}\\ \Sigma n\Sigma^{-1}\Sigma&=\sum^n_{i=1}\Sigma\Sigma^{-1}(X_i-\mu)(X_i-\mu)'\Sigma^{-1}\Sigma\\ n\Sigma &=\sum^n_{i=1}(X_i-\mu)(X_i-\mu)'\\ \hat{\Sigma} &= \frac{1}{n} \sum_{i=1}^n (X_i - \mu)(X_i - \mu)' \end{align} $$

绷不住了，上一篇写了6天？？！乐，这篇时间更久捏。

[TOC]

> 接续上篇，依旧讲多元正态分布，聚焦于检验部分。

**主要的计算步骤：**

1.  计算极大似然估计，得到极大似然估计量，比如$\hat\mu,\hat\Sigma$之类。
2.  然后计算似然比：$\lambda=\frac{\sup_{\theta\in\Theta_0}L(\theta|X)}{\sup_{\theta\in\Theta}L(\theta|X)}$
3.  得到似然比检验统计量：$T=-2\ln(\lambda)$/或者是其他的统计量，主要看$\lambda$服从何分布。

# 3.3 多元正态分布的检验

多元正态分布的检验问题包括：

| 单总体 | 多总体 | 多变量 |
| --- | --- | --- |
| 均值检验 | 均值比较检验 | 独立性检验 |
| 协方差检验 | 协方差比较检验 | 条件独立性检验 |
| \--- | 均值和协方差同时比较检验 | \--- |

## 3.3.0 均值向量的改进估计

总体均值向量$\mu$的极大似然估计$\hat \mu =\bar x$, 定义用$\bar x$估计$\mu$的损失函数为$L(\bar x,\mu)\ge0$.

+   $L(\bar x,\mu)>0$：取值越大，表示$\bar x$离$\mu$的距离越来越远，损失越来越大。
+   $L(\bar x,\mu)=0$：用$\bar x$估计$\mu$没有损失。

**实际问题中，对于均值向量$\mu$的估计，希望找到一个对于所有的$(\mu,\Sigma)$, 几乎处处使得风险函数=0的估计。** 但是实际上这样的估计通常是不存在的，因此我们退而求其次，希望找到一个估计$\hat \mu$, 使得其风险函数小于$\bar x$的风险，或者不比$\bar x$的风险大。**这就是改进估计。**

### $\Sigma$已知

令$\bar x=(\bar x_1,\dots,\bar x_p)',\mu=(\mu_1,\dots,\mu_p)'$, 平方和损失函数定义为： $$ L(\bar x,\mu)=\sum^n_{i=1}(\bar x_i-\mu_i)'(\bar x_i-\mu_i)=(\bar x-\mu)'(\bar x-\mu) $$ 一个好的估计希望平方损失越小越好，在统计决策理论中，损失函数的平均值称为风险函数。$\bar x$作为$\mu$的估计，它在平方和损失函数下的风险函数为： $$ \begin{align} R(\bar x)&=E[L(\bar x,\mu)]=E[(\bar x-\mu)'(\bar x-\mu)]\\ &=tr\left\{E[(\bar x-\mu)'(\bar x-\mu)]\right\}\\ &=\frac{tr(\Sigma)}{n}\\ \end{align} $$ $\bar x$的风险函数$R(\bar x)$只依赖于$\Sigma$,与$\mu$无关。

+   当p=1,2时：在平方和损失函数下，样本均值$\bar x$是总体均值$\mu$的容许估计，改进不存在。
+   当p$$3时：样本均值$x$是总体均值$$的不容许估计。

> **极大似然估计：**
> 
> 设$X=(x_1,\dots,x_n)'$是来自多元正态总体$X\sim N_p(\mu,\Sigma)$的样本，其中$n>p,\mu\in\mathbb{R}^p,\Sigma>0$. $$ \begin{align} L(\mu,\Sigma)&=\prod^n_{i=1}\frac{1}{(2\pi)^{\frac p 2}|\Sigma|^{\frac 1 2}}\exp[-\frac 1 2 (x_i-\mu)'\Sigma^{-1}(x_i-\mu)]\\ &=\frac{1}{(2\pi)^{np/2}|\Sigma|^{n/2}}\exp\left[-\frac{1}{2}\sum_{i = 1}^{n}(x_{i}-\mu)'\Sigma^{-1}(x_{i}-\mu)\right]\\ &=\frac{1}{(2\pi)^{np/2}|\Sigma|^{n/2}}\exp\left[-\frac{1}{2}\text{tr}\left(\Sigma^{-1}\left\{\sum_{i = 1}^{n}(x_{i}-\mu)(x_{i}-\mu)'\right\}\right)\right]\\ &=\frac{1}{(2\pi)^{np/2}|\Sigma|^{n/2}}\exp\left[-\frac{1}{2}\text{tr}\left(\Sigma^{-1}\{V + n(\bar{x}-\mu)(\bar{x}-\mu)'\}\right)\right] \end{align} $$ 首先给定 $\Sigma>0$ 时，求 $\mu$ 的极大似然估计，即求对数似然函数 $\ln L(\mu,\Sigma)$ 的极大值点。由式(5.3)，给定 $\Sigma>0$，关于 $\mu$ 的对数似然函数为 $$ \begin{align} \ln L(\mu,\Sigma)&=-\frac{n}{p}\ln2\pi-\frac{n}{2}\ln|\Sigma|-\frac{1}{2}\text{tr}(\Sigma^{-1}\{V + n(\bar{x}-\mu)(\bar{x}-\mu)'\})\\ &=-\frac{n}{p}\ln2\pi-\frac{n}{2}\ln|\Sigma|-\text{tr}(\Sigma^{-1}V)-\frac{n}{2}(\bar{x}-\mu)'\Sigma^{-1}(\bar{x}-\mu)\\ &\leq-\frac{n}{p}\ln2\pi-\frac{n}{2}\ln|\Sigma|-\text{tr}(\Sigma^{-1}V) \end{align} $$ 上式不等式中等号成立当且仅当 $\mu = \bar{x}$。因此，总体均值向量 $\mu$ 的极大似然估计为样本均值向量 $\bar{x}$。由$E(\bar{x})=\mu$，因此，样本均值向量 $\bar{x}$ 是 $\mu$ 的无偏估计。 将上式中的 $\mu$ 用它的极大似然估计 $\bar{x}$ 替换，得到 $\Sigma$ 的似然函数为: $$ L(\bar{x},\Sigma)=\frac{(2\pi)^{np/2}}{|\Sigma|^{n/2}}\exp\left[-\frac{1}{2}\text{tr}(\Sigma^{-1}V)\right] $$ 令 $\Sigma^{-1/2}V\Sigma^{-1/2}=UAU'$，其中 $U$ 是正交矩阵，$\Lambda=\text{diag}(\lambda_1,\cdots,\lambda_p)$ 是对角矩阵，则上式可以简化为 $$ L(\bar{x},\Sigma)=\frac{1}{(2\pi)^{np/2}|V|^{n/2}}\prod_{k = 1}^{p}\left[\lambda_k^{n/2}\exp\left\{-\frac{\lambda_k}{2}\right\}\right] $$ 由于 $f(x)=x^{n/2}\exp\{-x/2\}$ 在 $x = n$ 处取最大值，所以上式在 $\lambda_1=\cdots=\lambda_p=n$ 时取最大值，从而可知，$\Sigma$ 的极大似然估计 $\hat{\Sigma}$ 满足条件 $\hat{\Sigma}^{-1/2}V\hat{\Sigma}^{-1/2}=nI_p$。由此可见，$\Sigma$ 的极大似然估计为 $\hat{\Sigma}=V/n$。
> 
> **定理5.1.2** 设 $x_i=(x_{i1},\cdots,x_{ip})'(i = 1,\cdots,n)$ 为来自 $p$ 元正态总体 $N_p(\mu,\Sigma)$ 的一组随机样本，$n>p$，$\bar{x}$ 为样本均值向量，$V$ 为样本离差阵，则 $\mu$ 和 $\Sigma$ 的极大似然估计分别为 $\hat{\mu}=\bar{x}$ 和 $\hat{\Sigma}=V/n$。

## 3.3.1 单总体均值检验

设$\mathbf{X}=(x_1,x_2,\cdots,x_n)$是来自多元正态总体$N_p(\boldsymbol{\mu},\boldsymbol{\Sigma})$的$n$个独立样本，其中$\boldsymbol{\mu}\in\mathbb{R}^p$，$\boldsymbol{\Sigma}>0$，$n>p$。 我们关心如下总体均值$\boldsymbol{\mu}$的检验问题： $$ H_0:\boldsymbol{\mu}=\boldsymbol{\mu}_0,\quad v.s.\quad H_1:\boldsymbol{\mu}\neq\boldsymbol{\mu}_0 $$ 记$\bar{\mathbf{x}}$和$V$分别是样本均值和样本离差阵。

> **似然比检验方法**
> 
> 假设我们有一个统计模型，参数空间为$\Theta$, 其中包含了所有可能的参数值。检验问题通常表述为： $$ H_0:\theta\in\Theta_0，\quad v.s.\quad H_1:\theta\in\Theta_1=\Theta\backslash\Theta_0 $$ $H_0$表述为参数$\theta$属于一个特定的子集$\Theta_0$, $H_1$表述为参数$\theta$不属于原假设所定义的子集$\Theta_0$, 即属于$\Theta$中除$\Theta_0$之外的所有可能值。符号  表示集合的差集运算。
> 
> 记样本$X$下的似然函数为$L(\theta|X) = f(X|\theta)$。 似然比定义为在原假设 $H_0$ 下，似然函数的最大值与在整个参数空间 $\Theta$ 下的似然函数最大值之比。 $$ \lambda=\frac{\sup_{\theta\in\Theta_0}L(\theta|X)}{\sup_{\theta\in\Theta}L(\theta|X)} $$ 此处写的是上确界（所有上界中最小的一个），即使$L(\theta|x)$没有最大元素，但上确界仍然存在 ，这是sup与max的区别。
> 
> 似然比检验统计量为 ： $$ T=-2\ln(\lambda)=-2\ln\frac{\sup_{\theta\in\Theta_0}L(\theta|X)}{\sup_{\theta\in\Theta}L(\theta|X)} $$ 可以通过$T$在零假设$H_0$下的分布（零分布）构造检验的拒绝域。

### (1) $\boldsymbol{\Sigma}$已知的情形

均值参数$\boldsymbol{\mu}$的似然比 $$ \begin{align} L(\bar{x},\Sigma)&=\frac{1}{(2\pi)^{np/2}|\Sigma|^{n/2}}\exp\left[-\frac{1}{2}\text{tr}\left(\Sigma^{-1}\{V + n(\bar{x}-\mu)(\bar{x}-\mu)'\}\right)\right]\\\\ \lambda&=\frac{\sup_{\theta\in\Theta_0}L(\theta|X)}{\sup_{\theta\in\Theta}L(\theta|X)}\\ &=\frac{\exp\left\{-\frac 1 2\text{tr}(\boldsymbol{\Sigma}^{-1}(n(\bar{\mathbf{x}}-\boldsymbol{\mu}_0)(\bar{\mathbf{x}}-\boldsymbol{\mu}_0)'))\right\}}{\sup_{\boldsymbol{\mu}\in\mathbb{R}^p}\left[\exp\left\{-\frac 1 2\text{tr}(\boldsymbol{\Sigma}^{-1}(n(\bar{\mathbf{x}}-\boldsymbol{\mu})(\bar{\mathbf{x}}-\boldsymbol{\mu})'))\right\}\right]} \\ &=\frac{\exp\left\{-\frac 1 2n(\bar{\mathbf{x}}-\boldsymbol{\mu}_0)'\boldsymbol{\Sigma}^{-1}(\bar{\mathbf{x}}-\boldsymbol{\mu}_0)\right\}}{\sup_{\boldsymbol{\mu}\in\mathbb{R}^p}\left[\exp\left\{-\frac 1 2n(\bar{\mathbf{x}}-\boldsymbol{\mu})'\boldsymbol{\Sigma}^{-1}(\bar{\mathbf{x}}-\boldsymbol{\mu})\right\}\right]}\\ &=\frac{\exp\left\{-\frac 1 2 n(\bar{\mathbf{x}}-\boldsymbol{\mu}_0)'\boldsymbol{\Sigma}^{-1}(\bar{\mathbf{x}}-\boldsymbol{\mu}_0)\right\}}{\exp\left\{-\frac 1 2 n(\bar{\mathbf{x}}-\boldsymbol{\hat\mu})'\boldsymbol{\Sigma}^{-1}(\bar{\mathbf{x}}-\boldsymbol{\hat\mu})\right\}},\quad\hat\mu=\bar x\\ & =\exp\left\{-\frac 1 2n(\bar{\mathbf{x}}-\boldsymbol{\mu}_0)'\boldsymbol{\Sigma}^{-1}(\bar{\mathbf{x}}-\boldsymbol{\mu}_0)\right\} \end{align} $$ 因此似然比检验统计量为 $$ T = - 2\ln(\lambda)=n(\bar{\mathbf{x}}-\boldsymbol{\mu}_0)'\boldsymbol{\Sigma}^{-1}(\bar{\mathbf{x}}-\boldsymbol{\mu}_0) $$ 故当$T>\chi^2_{1-\alpha}(p)$时拒绝零假设，其犯第一类错误的概率为$\alpha$。

### (2) $\boldsymbol{\Sigma}$未知的情形

记$V_0=\sum_{i = 1}^{n}(x_{i}-\boldsymbol{\mu}_0)(x_{i}-\boldsymbol{\mu}_0)'=V+n(\bar x-\mu_0)'(\bar x-\mu_0)$ 参数$\boldsymbol{\mu}$的似然比为 ($\Sigma =\frac1{n-1}V$): $$ \begin{align} \lambda&=\frac{\sup_{\boldsymbol{\Sigma}}\left[|\boldsymbol{\Sigma}|^{-n/2}\exp\left\{-\frac 1 2\text{tr}(\boldsymbol{\Sigma}^{-1}(V + n(\bar{\mathbf{x}}-\boldsymbol{\mu}_0)(\bar{\mathbf{x}}-\boldsymbol{\mu}_0)'))\right\}\right]}{\sup_{\{\boldsymbol{\mu},\boldsymbol{\Sigma}\}}\left[|\boldsymbol{\Sigma}|^{-n/2}\exp\left\{-\frac 1 2\text{tr}(\boldsymbol{\Sigma}^{-1}(V + n(\bar{\mathbf{x}}-\boldsymbol{\mu})(\bar{\mathbf{x}}-\boldsymbol{\mu})'))\right\}\right]}\\ &=\frac{\sup_{\boldsymbol{\Sigma}}\left[|\boldsymbol{\Sigma}|^{-n/2}\exp\left\{-\frac 1 2\text{tr}(\boldsymbol{\Sigma}^{-1}V_0)\right\}\right]}{\sup_{\{\boldsymbol{\mu},\boldsymbol{\Sigma}\}}\left[|\boldsymbol{\Sigma}|^{-n/2}\exp\left\{-\frac 1 2\text{tr}(\boldsymbol{\Sigma}^{-1}(V + n(\bar{\mathbf{x}}-\boldsymbol{\mu})(\bar{\mathbf{x}}-\boldsymbol{\mu})'))\right\}\right]} \\ &=\frac{|\boldsymbol{\hat\Sigma_0}|^{-n/2}\exp\left\{-\frac 1 2\text{tr}(\boldsymbol{\hat\Sigma_0}^{-1}V_0)\right\}}{|\boldsymbol{\hat\Sigma}|^{-n/2}\exp\left\{-\frac 1 2\text{tr}(\boldsymbol{\hat\Sigma}^{-1}(V + n(\bar{\mathbf{x}}-\boldsymbol{\hat\mu})(\bar{\mathbf{x}}-\boldsymbol{\hat\mu})'))\right\}} \\ \end{align} $$ 其中$\hat\Sigma_0$是原假设$H_0$为真时：$\mu=\mu_0,\Sigma>0$时的极大似然估计。 $$ \hat\Sigma_0=\frac1n\sum^n_{i=1}(x_i-\mu_0)(x_i-\mu_0)' $$ 分母中的$\hat\mu,\hat\Sigma$是当$\mu\in\mathbb{R}^p,\Sigma>0$时，$\mu,\Sigma$的极大似然估计。 $$ \hat \mu=\bar x\\ \hat\Sigma=\frac 1 n \sum^n_{i=1}(x_i-\bar x) (x_i-\bar x)'=\frac V n $$ 继续计算$\lambda$, 分母后面的exp因为$\hat \mu=\bar x$所以等于0，$e^0=1$;且$\hat\Sigma_0=\frac{V_0}n$有： $$\begin{align} \lambda&=\frac{|\frac{V_0}n|^{-n/2}e^{-\frac {np} 2}}{\left|\frac V n\right|^{-n/2}},\quad e^{-\frac {np} 2}常数项忽略\\ &=\frac{\left|V_0\right|^{-n/2}}{\left|V\right|^{-n/2}}\\ &=\left(\frac{\left|V\right| + n(\bar{\mathbf{x}}-\boldsymbol{\mu}_0)(\bar{\mathbf{x}}-\boldsymbol{\mu}_0)'}{\left|V\right|}\right)^{-n/2} \\ &=\left|I_p + nV^{-1/2}(\bar{\mathbf{x}}-\boldsymbol{\mu}_0)(\bar{\mathbf{x}}-\boldsymbol{\mu}_0)'V^{-1/2}\right|^{-n/2}\\ &=(1 + n(\bar{\mathbf{x}}-\boldsymbol{\mu}_0)'V^{-1}(\bar{\mathbf{x}}-\boldsymbol{\mu}_0))^{-n/2} \end{align}$$
利用似然比原理，在$\lambda$较小时拒绝原假设$H_0: \mu=\mu_0$, 从而认为备择假设成立$H_1$. 当原假设$H_0: \mu=\mu_0$成立时，由$n(n-1)(\bar x-\mu_0)'V^{-1}(\bar x-\mu_0)\sim T^2_p(n-1)$, 所以通常取： $$ T^{2}=n(n - 1)({x}-*{0})'V{-1}({x}-*{0})=n({x}-*{0})'S{-1}({x}-*{0}) $$ 为检验统计量。并在$T^2$较大时拒绝原假设$H_0$, 从而认为备择假设$H_1$成立。

根据Hotelling $T^2$分布的性质有: $$ T^{2} \stackrel{d}{\rightarrow} T_{p}^{2}(n - 1)\\ \frac{n - p}{(n - 1)p}T^{2} \stackrel{d}{\rightarrow} F(p, n - p) $$ 则当$\frac{n - p}{(n - 1)p}T^{2}>F_{1-\alpha}(p, n - p)$时拒绝零假设，其犯第一类错误的概率为$\alpha$。

检验的p值为： $$ p_v=Pr(F_{p,n-p}\ge\frac{n-p}{(n-1)p}T^2) $$

### 栗子(检验单总体、两总体均值)

**(1)**: 在正态假设下，哥特式教堂的长度和中殿长度是否与罗马式教堂具有相同的均值？

![image-20241208213813501](https://cdn.jsdelivr.net/gh/SchwertLin/Pic/img/image-20241208213813501.png)

计算哥特式教堂数据的$\bar x,V$: $$ \bar x=\begin{pmatrix}121.12\\22.84\end{pmatrix},V=\begin{pmatrix}19466.70& 2257.90\\2257.90& 469.56\end{pmatrix} $$ n=16,p=2, $H_0:\mu=\mu_0,\quad v.s.\quad H_1:\mu\neq\mu_0,\quad \mu_0=\begin{pmatrix}145.29\\22.69\end{pmatrix}$, $\Sigma$未知。 $$ T^2=n(n-1)(\bar X-\mu_0)'V^{-1}(\bar X-\mu_0)=17.283\\ $$ 设定显著性水平为$\alpha=0.05$, 计算检验的p值： $$ \begin{align} p_v&=Pr(F_{p,n-p}\ge\frac{n-p}{(n-1)p}T^2)\\ &=Pr(F(2,14)\ge8.0654)\\ &=0.0047\\ &<0.05 \end{align} $$ **结论：**故拒绝零假设，$\mu\neq\mu_0$, 认为哥特式教堂和罗马式教堂没有相同的长度和中殿高度。

**(2):** 哥特式教堂的长度与罗马式教堂长度是否具有相同的均值？

这实际上是一个**单总体正态分布检测**。哥特式教堂的样本协方差阵: $$ S=\frac{V}{n-1}=\begin{pmatrix}19466.70/15& 2257.90/15\\2257.90/15& 469.56/15\end{pmatrix}=\begin{pmatrix}12977.78& 150.53\\150.53& 31.3\end{pmatrix}=\begin{pmatrix}s_{11}&s_{12}\\s_{21}&s_{22}\end{pmatrix} $$ t-检验与检验的p值： $$ t_1=n =4 =-2.648\\

p=Pr{|t(15)||t_1|}=2Pr(t(15))=0.017 $$ **总结：**$p\le\alpha$因此认为哥特式教堂的长度与罗马式教堂长度没有相同均值。

**(3):** 哥特式教堂的中殿高度与罗马式教堂的中殿高度是否具有相同的均值？ $$ t_2=\sqrt n\frac{\bar X_2-22.69}{\sqrt{s_{22}}}=4\times\frac{22.84-22.69}{\sqrt{31.3}}=0.107\\\\ p=Pr\left\{|t(15)|\ge|t_2|\right\}=2Pr(t(15)\ge 0.107)=0.916\gt 0.05 $$ **总结：**$p\gt\alpha$因此认为哥特式教堂的中殿高度与罗马式教堂的中殿高度具有相同的均值.

**两种教堂长度和中殿高度的比较问题**（例1续）

如果设定 $\mu_0^=\begin{pmatrix}131\\21\end{pmatrix}$。 考虑如下的协方差阵 $\Sigma$ 未知时的均值检验问题： $$ H_0:\mu = \mu_0^*，\quad v.s.\quad H_1:\mu\neq\mu_0^* $$ 此时Hotelling$T^2$ 检验统计量、计算的p值为 ： $$ T^2=n(n - 1)(\bar{X}-\mu_0^*)'V^{-1}(\bar{X}-\mu_0^*) = 11.507 $$$$p=P\left\{F(p,n - p)\geq\frac{n - p}{(n - 1)p}T^2\right\} =P\left\{F(2,14)\geq5.370\right\}=0.019 $$ **结论**：拒绝零假设。

1') 哥特式教堂的长度与罗马式教堂长度是否有相同均值的t - 检验、p值： $$ t_1^*=\sqrt{n}\cdot\frac{\bar{X}_1 - 131}{\sqrt{S_{11}^*}}=\sqrt{16}\cdot\frac{121.12 - 131}{\sqrt{1297.78}}=-1.097$$ $$p = P_r\{|t(15)|\geq|t_1^*|\}=2P_r\{t(15)\leq - 1.097\}=0.290>0.05 $$ **结论**：因此认为哥特式教堂的长度与罗马式教堂长度有相同均值。

2') 哥特式教堂的中殿高度与罗马式教堂的中殿高度是否有相同均值的t - 检验、p值： $$ t_2^*=\sqrt{n}\cdot\frac{\bar{X}_2 - 21}{\sqrt{S_{22}^*}}=\sqrt{16}\cdot\frac{22.84 - 21}{\sqrt{31.30}}=1.315$$ $$p = P_r\{|t(15)|\geq|t_2^*|\}=2P_r\{t(15)\geq1.315\}=0.208>0.05 $$ **结论**：因此认为哥特式教堂的中殿高度与罗马式教堂的中殿高度有相同的均值。

## 3.3.2 两个多元总体均值比较的检验

记 $X=(x_1,\cdots,x_m)$ 和 $Y=(y_1,\cdots,y_n)$ 分别为来自总体 $N_p(\mu_1,\Sigma)$ 和 $N_p(\mu_2,\Sigma)$ 的独立样本，$\mu_1,\mu_2\in R^p$，$\Sigma>0$，$\min(m,n)>p$。

两个总体均值是否相等的检验问题为: $$ H_0:\mu_1 = \mu_2，\quad v.s.\quad H_1:\mu_1\neq\mu_2 $$ 注意：此时两个总体的协方差阵相等。 记 $\bar{x}$ 和 $\bar{y}$ 分别为总体 $X$ 和 $Y$ 的样本均值。

## (1) $\Sigma$ 已知的情形

$(\mu_1,\mu_2)$ 的似然函数为(去掉常数项): $$ L(\mu_1,\mu_2)=\exp\left\{-\frac{1}{2}[m(\bar{x}-\mu_1)'\Sigma^{-1}(\bar{x}-\mu_1)+n(\bar{y}-\mu_2)'\Sigma^{-1}(\bar{y}-\mu_2)]\right\}$$ $$\hat{\mu}_0=\frac{m\bar{x}+n\bar{y}}{m + n}=\frac{\sum_{i = 1}^{m}x_i+\sum_{j = 1}^{n}y_j}{m + n} $$ 当 $\mu_1=\mu_2=\mu$ 时，$\mu$ 的极大似然估计是 $\hat{\mu}_0$。

检验问题的似然比为: $$ \begin{align} \lambda&=\frac{\sup_{\mu}L(\mu,\mu)}{\sup_{\{\mu_1,\mu_2\}}L(\mu_1,\mu_2)}\\ &=\exp\left\{-\frac{1}{2}[m(\bar{x}-\hat{\mu}_0)'\Sigma^{-1}(\bar{x}-\hat{\mu}_0)+n(\bar{y}-\hat{\mu}_0)'\Sigma^{-1}(\bar{y}-\hat{\mu}_0)]\right\}\\ &=\exp\left\{-\frac{1}{2}\left[\frac{mn}{m + n}(\bar{x}-\bar{y})'\Sigma^{-1}(\bar{x}-\bar{y})\right]\right\} \end{align} $$

> $$ m(\bar{x}-\hat{\mu}_0)'\Sigma^{-1}(\bar{x}-\hat{\mu}_0)+n(\bar{y}-\hat{\mu}_0)'\Sigma^{-1}(\bar{y}-\hat{\mu}_0)=\frac{mn}{m + n}(\bar{x}-\bar{y})'\Sigma^{-1}(\bar{x}-\bar{y}) $$
> 
> ![image-20241210134445146](https://cdn.jsdelivr.net/gh/SchwertLin/Pic/img/image-20241210134445146.png)

则检验比检验统计量为: $$ T=-2\log(\lambda)=\frac{mn}{m + n}(\bar{x}-\bar{y})'\Sigma^{-1}(\bar{x}-\bar{y})\vert_{H_0}\stackrel{d}{\sim}\chi^2(p) $$ 当 $T>\chi^2_{1-\alpha}(p)$ 时拒绝零假设，其犯第一类错误的概率为 $\alpha$。

## (2) $\Sigma$ 未知的情形

记$V_X$和$V_Y$分别为总体$X$和$Y$的样本离差阵，$V = V_X+V_Y$。

$(\mu_1,\mu_2,\Sigma)$ 的似然函数为: $$ L(\mu_1,\mu_2,\Sigma)=\frac{1}{\vert\Sigma\vert^{\frac{(m + n)}2}} \exp\left\{-\frac{1}{2}\text{tr}[\Sigma^{-1}(V + m(\bar{x}-\mu_1)(\bar{x}-\mu_1)' + n(\bar{y}-\mu_2)(\bar{y}-\mu_2)')]\right\} $$ 当$\mu_1,\,u_2\in\mathbb{R}^p,\Sigma>0$时，$\mu_1$和$\mu_2$的极大似然估计分别为：$\hat\mu_1=\bar x,\hat\mu_2=\bar y$，$\Sigma$的极大似然估计为$\hat\Sigma={V_1+V_2}/{(n+m)}$.在原假设$H_0$成立时($\mu_1=\mu_2=\mu$)，$\mu$的极大似然估计为$\hat\mu_0=(n\bar x+m\bar y)/(n+m)$. 在原假设$H_0$成立时，将似然函数$L(\mu_1,\mu_2,\Sigma)$中的均值向量$\mu_1=\mu_2=\hat\mu_0$, 从而得到原假设$H_0$成立时的$\Sigma$的似然函数为： $$ \begin{align} L(\Sigma)&=\frac{1}{\vert\Sigma\vert^{\frac{(m + n)}2}} \exp\left\{-\frac{1}{2}\text{tr}[\Sigma^{-1}(V_1+V_2 + m(\bar{x}-\hat\mu_0)(\bar{x}-\hat\mu_0)' + n(\bar{y}-\hat\mu_0)(\bar{y}-\hat\mu_0)')]\right\}\\ \hat \Sigma_0&=\frac{V_1+V_2 + m(\bar{x}-\hat\mu_0)(\bar{x}-\hat\mu_0)'+ n(\bar{y}-\hat\mu_0)(\bar{y}-\hat\mu_0)'}{m+n}\\ \hat \Sigma_0&=\frac{V_1+V_2 + \frac{mn}{m + n}(\bar{x}-\bar{y})(\bar{x}-\bar{y})'}{m+n} \end{align} $$ 因为$m(\bar{x}-\hat{\mu}_0)'\Sigma^{-1}(\bar{x}-\hat{\mu}_0)+n(\bar{y}-\hat{\mu}_0)'\Sigma^{-1}(\bar{y}-\hat{\mu}_0)=\frac{mn}{m + n}(\bar{x}-\bar{y})'\Sigma^{-1}(\bar{x}-\bar{y})$, 所以有$m(\bar{x}-\hat\mu_0)(\bar{x}-\hat\mu_0)'+ n(\bar{y}-\hat\mu_0)(\bar{y}-\hat\mu_0)'= \frac{mn}{m + n}(\bar{x}-\bar{y})(\bar{x}-\bar{y})'$

检验问题的似然比为: $$ \begin{align} \lambda&=\frac{\sup_{\{\mu,\Sigma\}}L(\mu,\mu,\Sigma)}{\sup_{\{\mu_1,\mu_2,\Sigma\}}L(\mu_1,\mu_2,\Sigma)}\\ &=\left(\frac{\vert V_1+V_2 + \frac{mn}{(m + n)}(\bar{x}-\bar{y})(\bar{x}-\bar{y})'\vert}{\vert V_1+V_2\vert}\right)^{-(m + n)/2}\\ &=\vert I_p+\frac{mn}{m+n}(V_1+V_2)^{-\frac 1 2}(\bar{x}-\bar{y})(\bar{x}-\bar{y})'(V_1+V_2)^{-\frac 1 2}\vert^{-(m + n)/2}\\ &=\left(1+\frac{mn}{m + n}(\bar{x}-\bar{y})'(V_1+V_2)^{-1}(\bar{x}-\bar{y})\right)^{-(m + n)/2} \end{align} $$ 令 : $$ T^2=\frac{mn(m + n - 2)}{m + n}(\bar{x}-\bar{y})'(V_1+V_2)^{-1}(\bar{x}-\bar{y})\\\\ T^2\vert_{H_0}\stackrel{d}{\sim}T^2_p(m + n - 2) $$ 取$T^2$为检验统计量，在原假设$H_0$为真($\mu_1=\mu_2$)时，$T^2\stackrel{d}{\sim}T^2_p(m + n - 2)$, 且在$T^2$较大时拒绝原假设$H_0$, 从而认为备择假设$H_1$成立($\mu_1\neq\mu_2$). 再根据Hotelling $T^2$分布的性质： $$ \frac{1}{(m + n - 2)}T^2_p(n+m-2)\overset{d}{=}\frac{\chi^2_p}{\chi^2_{m + n - p - 1}}$$ $$ \frac{(m + n - p - 1)}{(m + n - 2)p}T^2\overset{d}{\sim}F(p,m + n - p - 1)$$ $$ p_v=Pr\left( F_{1-\alpha}(p,m + n - p - 1)\ge\frac{(m + n - p - 1)}{(m + n - 2)p}T^2\right) $$ 因此，当$p<\alpha$ 时拒绝零假设， 其犯第一类错误的概率为 $\alpha$。

## MLE小结

**似然比检验统计量**由似然函数在极大似然估计下的似然函数值决定。

相同协方差阵下正态总体均值和协方差阵的**极大似然估计(MLE)**：

 
| 均值 | 协方差阵 |
| --- | --- |
| 单总体：均值的极大似然估计为样本均值; | 计算在给定均值极大似然估计下协方差阵的似然函数: |
| 多总体：各总体均值无约束的极大似然估计为各自的样本均值; | $\vert\Sigma\vert^{-n/2}\exp\{-\frac 1 2\text{tr}(\Sigma^{-1}W)\}$ |
| 多总体：在各总体均值相等的约束条件下，均值的极大似然估计为将所有样本看成是来自同一总体时的样本均值; | 其中$W$是仅与数据有关的正定矩阵，则协方差矩阵的极大似然估计$\hat{\Sigma}=W/n$。 |

## 3.3.3 多元Behrens - Fisher问题

记 $X=(x_1,\cdots,x_m)$ 和 $Y=(y_1,\cdots,y_n)$ 分别为来自总体 $N_p(\mu_1,\Sigma_1)$ 和 $N_p(\mu_2,\Sigma_2)$ 的独立样本，$\mu_1,\mu_2\in R^p$，$\Sigma_1,\Sigma_2>0$，$\min(m,n)>p$。

**Behrens - Fisher问题**：即在 $\Sigma_1\neq\Sigma_2$ 时，如下的检验问题： $$ H_0:\mu_1 = \mu_2，\quad v.s.\quad H_1:\mu_1\neq\mu_2 $$

### (1) $m = n$ 的情形

令 $Z=X - Y=(z_1,\cdots,z_n)$，易知 $Z$ 是来自总体 $N_p(\mu,\Sigma)$ 的独立样本， 其中，$\mu=\mu_1-\mu_2$，$\Sigma=\Sigma_1+\Sigma_2$，$z_i=x_i - y_i$，$1\leq i\leq n$。 因此，对 $Z$ 做 $\Sigma$ 未知下的如下检验即可 $$ H_0:\mu = 0,\quad v.s.\quad H_1:\mu\neq 0 $$ 即**单总体协方差阵未知时均值是否为0的检验**。

> 因为X,Y同是n维“向量”，所以可将$Z=X-Y$作为一个单独的多元正态总体，$\mu_z=\mu_x-\mu_y,\Sigma_z=\Sigma_x+\Sigma_y$. 所以检验$\mu_x=\mu_y$就是检验$\mu_z=0$.

### (2) $m\neq n$ 的情形

检验统计量为： $$ T^2 = (\bar{x}-\bar{y})'S^{-1}(\bar{x}-\bar{y}) $$ 其中，$S = \frac {S_X}m+ \frac{S_Y}n$，$S_X$，$S_Y$分别是$X$，$Y$的样本协方差阵。

#### 2.1) 有限样本下的近似分布

在零假设$H_0:\mu_1=\mu_2$下，$T^2$近似服从Hotelling$T^2$分布$T^2_p(f)$: $$ f=\frac{ \left[(\bar{x}-\bar{y})'S^{-1}(\bar{x}-\bar{y})\right]^2 }{ \frac{\left[(\bar{x}-\bar{y})'S^{-1}S_XS^{-1}(\bar{x}-\bar{y})\right]^2}{m^2(m - 1)} + \frac{\left[(\bar{x}-\bar{y})'S^{-1}S_YS^{-1}(\bar{x}-\bar{y})\right]^2}{n^2(n - 1)} } $$ 相应检验的$p$值为: $$ p = P\left\{F(p,f - p + 1)\geq\frac{f - p + 1}{fp}T^2\right\} $$

#### 2.2) 渐近分布 (总体不服从正态分布)

**或者是，没有证据表明总体服从正态分布。因此，我们将其渐渐近为正态分布来计算。**

假设$(m + n)\to\infty$，$m/(m + n)\to\alpha$，$0 < \alpha< 1$， 则在零假设下有: $$ T^2\stackrel{d}{\to}\chi^2(p) $$ 则当$T^2>\chi^2_{1 - \alpha}(p)$时拒绝零假设，其犯第一类错误的概率近似为$\alpha$。

也可以用$\chi^2(p)$分布的一阶校正来近似$T^2$的分布。

> **Q: $\chi^2(p)$分布的一阶校正是什么？**
> A: 
> **一阶校正（First-Order Correction）** 在统计学中指的是对某一统计量的分布进行调整，以提高其与理论分布（如卡方分布$\chi^2(p)$）的拟合度，尤其是在样本量较小或其他条件不完全满足时。这种校正旨在减少近似分布与实际分布之间的偏差，从而提高假设检验的准确性和可靠性。通过一阶校正，$T^2$统计量在有限样本下的分布更接近于$\chi^2(p)$分布，从而提高了假设检验的准确性。
> **Bartlett校正（Bartlett Correction）**:
> Bartlett校正是最常见的一阶校正方法之一，主要应用于似然比检验（Likelihood Ratio Test, LRT）中。其基本思想是通过引入一个校正因子，调整似然比统计量，使其在有限样本下的均值更接近卡方分布的均值。
> **定义**：设$T$为未校正的似然比统计量，其期望值在原假设下通常为自由度的数目，但在有限样本下可能偏离。Bartlett校正通过引入一个校正因子$c$，定义校正后的统计量为： $$ T_{\text{校正}} = c \cdot T $$ 使得$T_{\text{校正}}$的期望值更接近于$\chi^2(p)$分布的自由度$p$。
> **Hotelling的$T^2$检验中的一阶校正**:
> 当样本量不等时，检验统计量$T^2$的分布在有限样本下并不完全符合卡方分布$\chi^2(p)$，因此需要进行一阶校正以提高检验的准确性。
> **具体步骤**：
> 1.  **计算未校正的$T^2$统计量**： $$ T^2 = (\bar{x} - \bar{y})' S^{-1} (\bar{x} - \bar{y}) $$ 其中，$S = \frac{S_X}{m} + \frac{S_Y}{n}$，$S_X$和$S_Y$分别是两个样本的离差平方和矩阵。
> 2.  **计算Bartlett校正因子$c$**：
>     校正因子的具体计算公式依赖于具体的检验方法和样本数据。在Hotelling的$T^2$检验中，$c$通常基于样本量、变量数目和样本协方差矩阵的特性来确定。
> 3.  **计算校正后的统计量$T_{\text{校正}}$**： $$ T_{\text{校正}} = c \cdot T^2 $$
> 4.  **确定检验的p值**：
>     使用校正后的统计量$T_{\text{校正}}$，根据卡方分布$\chi^2(p)$计算p值： $$ p = P\left\{ \chi^2(p) \geq T_{\text{校正}} \right\} $$
> 另外，可以尝试似然比统计量及其渐近分布。
> **Wilks定理**： 
> (**Wilks定理** 为这些似然比检验提供了**理论基础**，说明在原假设成立时，检验统计量的**渐近分布**为卡方分布。)
> 在正则条件下，对检验问题: $$ H_0:\theta\in\Theta_0,\quad v.s. \quad H_1:\theta\in\Theta_1=\Theta\backslash\Theta_0 $$ 似然比检验统计量: $$ T = - 2\log(\lambda)=- 2\log\frac{\sup_{\theta\in\Theta_0}L(\theta|X)}{\sup_{\theta\in\Theta}L(\theta|X)} $$ 在零假设下有极限分布: $$ T\vert_{H_0}\stackrel{d}{\to}\chi^2(p) $$ 其中 $p = \dim(\Theta)-\dim(\Theta_0)$。

## 例：Behrens - Fisher检验问题

$H_0:\mu_x = \mu_y$。 设有一组数据，经处理后有： $$ \bar{x}=\begin{pmatrix}9.82\\15.06\end{pmatrix},\quad\bar{y}=\begin{pmatrix}13.05\\22.57\end{pmatrix}\\ S_x=\begin{pmatrix}120.000&-16.304\\-16.304&17.792\end{pmatrix},\quad S_y=\begin{pmatrix}81.796&32.098\\32.098&53.801\end{pmatrix} $$ 其中，$p = 2$，$m = 16$，$n = 11$。 没有证据认为$\Sigma_1=\Sigma_2$，因而这是Behrens - Fisher检验问题。采用近似Hotelling $T^2$ 检验方法。 经计算得: $$ \bar x-\bar y=\begin{pmatrix}-3.23\\-7.51\end{pmatrix}\\ S=\frac{S_x}{m}+\frac{S_y}{n}=\begin{pmatrix}7.5&-1.019\\-1.019&1.112\end{pmatrix}+\begin{pmatrix}7.436&2.918\\2.918&4.891\end{pmatrix}=\begin{pmatrix}14.936&1.899\\1.899&6.003\end{pmatrix}\\ T^2 = (\bar{x}-\bar{y})'S^{-1}(\bar{x}-\bar{y})=9.4447 $$ 代入公式得自由度$f = 14$。

```
import numpy as np  
  
S_x = np.array([[ 120, -16.304],[-16.304,  17.792]] )  
S_y = np.array([[81.796,32.098],[32.098,53.801]])  
x_y= np.array([[-3.23], [-7.51]])  
S_itv= np.array([[ 0.06975803, -0.02206738],[-0.02206738,0.17356421]] )  
  
ans_1 = np.dot(np.dot(x_y.T,S_itv),x_y)**2  
ans_2 = np.dot(np.dot(np.dot(np.dot(x_y.T,S_itv),S_x),S_itv),x_y)**2/(16*16*15)  
ans_3 = np.dot(np.dot(np.dot(np.dot(x_y.T,S_itv),S_y),S_itv),x_y)**2/(11*11*10)  
  
f = ans_1/(ans_2+ans_3)  
  
print(ans_1) # [[89.23120903]]  
print(ans_2) # [[0.16334961]]  
print(ans_3) # [[6.2108612]]  
print(f) # [[13.99878537]]约等于14
```

因此检验的$p$值为: $$ \begin{align} 0.025&< P\left\{F(p,f - p + 1)\geq\frac{f - p + 1}{fp}T^2\right\}\\ &= P\left\{F(2,13)\geq\frac{13}{28}T^2\right\} \\ &<0.05 \end{align} $$ **结论**：拒绝零假设。

## 3.3.4 多元方差分析

设有 $k$ 个相互独立的总体 $X_i\stackrel{d}{\sim}N_p(\mu_i,\Sigma)$，$\mu_i\in R^p$，$\Sigma>0$。

$(x_{i1},\cdots,x_{in_i})$ 是来自总体 $X_i$ 的样本，$1\leq i\leq k$。记 $n=\sum_{i = 1}^{k}n_i$，$n\geq p + k$。

考虑检验问题： $$ H_0:\mu_1=\cdots=\mu_k,\quad v.s.\quad H_1:\mu_1,\cdots,\mu_k 不全相等 $$ **我们要检验的是 k 个多元正态总体均值向量是否都相同。**

似然函数为 : $$ L(\mu_1,\cdots,\mu_k,\Sigma)=\vert\Sigma\vert^{-n/2}\exp\left\{-\frac{1}{2}\text{tr}\left(\Sigma^{-1}\left[\sum_{i = 1}^{k}V_i+\sum_{i = 1}^{k}n_i(\bar{x}_i-\mu_i)(\bar{x}_i-\mu_i)'\right]\right)\right\} $$ 其中，$\bar{x}_i$ 和 $V_i$ 分别是**第 $i$ 个总体**的样本均值和样本离差阵，$1\leq i\leq k$。 记 $\bar{x}$ 为**全部样本**下的样本均值。 $$ \bar x=\frac 1 n\sum_{i = 1}^{k}n_i\bar{x}_i\\ \bar{x}_i = \frac{1}{n_i}\sum_{j=1}^{n_i} x_{ij}\\ V_i = \sum_{j=1}^{n_i} (x_{ij} - \bar{x}_i)(x_{ij} - \bar{x}_i)' $$

> **似然函数的推导**:
> 
> 给定参数$(\mu_1,\mu_2,\ldots,\mu_k,\Sigma)$ 的前提下，各个样本来自互相独立的多元正态总体，因此联合似然函数可表示为： $$ L(\mu_1,\ldots,\mu_k,\Sigma) = \prod_{i=1}^k \prod_{j=1}^{n_i} f(x_{ij}|\mu_i,\Sigma) $$ 其中多元正态密度函数为： $$ f(x_{ij}|\mu_i,\Sigma)= \frac{1}{(2\pi)^{p/2}|\Sigma|^{1/2}}\exp\left(-\frac{1}{2}(x_{ij}-\mu_i)'\Sigma^{-1}(x_{ij}-\mu_i)\right) $$ 将所有样本合并，取对数似然函数 $=L $，**再略去与参数无关的常数项**并经过一定的矩阵代数运算与整理（使用迹的运算属性），最终得到 $$ L(\mu_1,\cdots,\mu_k,\Sigma)= | \Sigma |^{-n/2}\exp\left\{-\frac{1}{2}\text{tr}\left[\Sigma^{-1}\left(\sum_{i=1}^k V_i + \sum_{i=1}^k n_i(\bar{x}_i - \mu_i)(\bar{x}_i - \mu_i)'\right)\right]\right\} $$ 在这里，我们可以看到似然函数中分为两部分：
> 
> 1.  $\sum_{i=1}^k V_i$：反映了所有组内部的变异信息（各组样本点围绕各自组均值$\bar{x}_i$的变异）。
> 2.  $\sum_{i=1}^k n_i(\bar{x}_i - \mu_i)(\bar{x}_i - \mu_i)'$：反映了样本组均值与总体均值$\mu_i$之间的偏差。

### (1) $\Sigma$ 已知的情形

**检验问题的似然比为**: $$ \begin{align} \lambda&=\frac{\sup_{\mu}L(\mu,\cdots,\mu)}{\sup_{\{\mu_1,\cdots,\mu_k\}}L(\mu_1,\cdots,\mu_k)} \\ &=\frac{ | \Sigma |^{-n/2}\exp\left\{-\frac{1}{2}\text{tr}\left[\Sigma^{-1}\left(\sum_{i=1}^k V_i + \sum_{i=1}^k n_i(\bar{x}_i - \mu)(\bar{x}_i - \mu)'\right)\right]\right\}}{ | \Sigma |^{-n/2}\exp\left\{-\frac{1}{2}\text{tr}\left[\Sigma^{-1}\sum_{i=1}^k V_i\right] \right\}}\\ &=\exp\left\{-\frac{1}{2}\text{tr}\left(\Sigma^{-1}\left[\sum_{i = 1}^{k}n_i(\bar{x}_i-\bar{x})(\bar{x}_i-\bar{x})'\right]\right)\right\} \end{align} $$ $\text{SSB}=\sum_{i = 1}^{k}n_i(\bar{x}_i-\bar{x})(\bar{x}_i-\bar{x})'$为组间离差阵 (Sum of Squares Between)。

**则似然比检验统计量为** : $$ \begin{align} T&=-2\log(\lambda)=\text{tr}\left[\Sigma^{-1}(\text{SSB})\right] \\ &=\sum_{i = 1}^{k}\text{tr}\left(n_i\Sigma^{-1}(\bar{x}_i-\bar{x})(\bar{x}_i-\bar{x})'\right) \\ &=\sum_{i = 1}^{k}n_i(\bar{x}_i-\bar{x})'\Sigma^{-1}(\bar{x}_i-\bar{x}) \end{align} $$ 在原假设的大样本情形下，T渐近服从$\chi^2(p(k-1))$分布。 $$ \begin{align} \text{SSB}\stackrel{d}{\sim}W_p(k - 1,\Sigma)& \Rightarrow \Sigma^{-1/2}(\text{SSB})\Sigma^{-1/2}\stackrel{d}{\sim}W_p(k - 1,I_p) \\ &\Rightarrow \text{tr}(\Sigma^{-1/2}(\text{SSB})\Sigma^{-1/2})\stackrel{d}{\sim}\chi^2((k - 1)p) \\ &\Rightarrow \text{tr}[\Sigma^{-1}(\text{SSB})]\stackrel{d}{\sim}\chi^2((k - 1)p)\\ &\Rightarrow T\stackrel{d}{\sim}\chi^2((k - 1)p \end{align} $$ 若观测到的检验统计量 $T>\chi^2_{1 - \alpha}((k - 1)p)$，则在显著性水平 $\alpha$下拒绝原假设 $H_0$，否则不拒绝。

### (2) $\Sigma$ 未知的情形

SSW为组内离差阵 (Sum of Squares Within)，SST为总离差阵 (Total Sum of Squares)，记为:  $$=*{i = 1}^{k}V_i=*{i = 1}^{k}*{j = 1}^{n_i}(x*{ij}-{x}*i)(x*{ij}-{x}*i)'\ V_iW_p(n*{i}-1,) i.i.d.\ SSWW_p(n-k,)\\ $$
$$\begin{align} \text{SST}&=\sum_{i = 1}^{k}V_i+\sum_{i = 1}^{k}n_i(\bar{x}_i-\bar{x})(\bar{x}_i-\bar{x})' \\ &=\text{SSW}+\text{SSB} \\ &=\sum_{i = 1}^{k}\sum_{j = 1}^{n_i}(x_{ij}-\bar{x})(x_{ij}-\bar{x})' \end{align}$$ 由前面的分析有: $SSW\sim W_p(k-1,\Sigma),SSB\sim W_p(n-k,\Sigma)$。当原假设$H_0$成立时，$SST\sim W_p(n-1,\Sigma)$，且SSW和SSB相互独立。则检验的似然比为: $$ = =()^{n 2} $$ 利用似然比原理，在$\lambda$较小时拒绝原假设$H_0$，从而认为备择假设$H_1$成立，即$\mu_1\neq\dots\neq\mu_k$。当原假设$H_0$成立时，SSW和SSB相互独立。由Wilks分布定义得： $$ =(p,n-k,k-1) $$ 因此，当 $\Lambda<\Lambda_{p,n - k,k - 1}(\alpha)$ 时拒绝零假设。 也可以用似然比检验统计量的渐近分布，即: $$ - 2()=- n()^2((k - 1)p) $$

> **定理3.1** 在原假设$H_0$成立时，有如下结论成立： $$ \text{SST}\stackrel{d}{\sim}W_p(n - 1,\Sigma)\\ \text{SSW}\stackrel{d}{\sim}W_p(n - k,\Sigma)\\ \text{SSB}\stackrel{d}{\sim}W_p(k - 1,\Sigma) $$ 且$\text{SSB}$与$\text{SSW}$相互独立。
> **证明**：
> 记 $X=(X_1,\cdots,X_k)_{p\times n}$，其中 $X_i=(x_{i1},\cdots,x_{in_i})_{p\times n_i}$，$1\leq i\leq k$ 记 $J_n$ 为 $n\times n$ 的全1矩阵，并令 $$ \begin{align} C &= I_n - J_n/n\\ C_1&=\begin{pmatrix} I_{n_1}-J_{n_1}/n_1&0&\cdots&0\\ 0&I_{n_2}-J_{n_2}/n_2&\cdots&0\\ \vdots&\vdots&\ddots&\vdots\\ 0&0&0&I_{n_k}-J_{n_k}/n_k \end{pmatrix}\\ C_2 &= C - C_1 \end{align} $$ 不难推知有 : $$ \text{SST}=XCX'\\ \text{SSW}=XC_1X'\\ \text{SSB}=XC_2X' $$ 又知 $C$ 和 $C_1$ 都是幂等阵，且: $$ \text{rank}(C)=\text{tr}(C)=n - 1,\quad \text{rank}(C_1)=\text{tr}(C_1)=n - k, \\ \text{SST}-\text{SSW}=\text{SSB}>0 $$ 在零假设下，它们的分布与共同的 $\mu$ 无关， 因此可设 $X$ 是服从 $N_{p\times n}(0,I_n\otimes\Sigma)$ 的矩阵正态分布， 由 Wishart 分布二次型的性质得证定理。

当总体数$k\leq3$，或样本维数$p\leq2$时，可以转化为$F$分布。

 
| p/k | 检验统计量                                                                               |
| --- | ----------------------------------------------------------------------------------- |
| p=1 | $\frac{n - k}{k - 1}\cdot\frac{1-\Lambda}{\Lambda}\stackrel{d}{\sim}F(k - 1,n - k)$ |
| k=2 | $\frac{n - 1 - p}{p}\cdot\frac{1-\Lambda}{\Lambda}\stackrel{d}{\sim}F(p,n - 1 - p)$ |
| p=2 | $F(2(k - 1), 2(n - k - 1))$                                                         |
| k=3 | $F(2p,2(n - 2 - p))$                                                                |

## 例：多元方差分析

![image-20241211113052807](https://cdn.jsdelivr.net/gh/SchwertLin/Pic/img/image-20241211113052807.png)

**检验问题：这3种生产方法对完成任务是否有差异？**

本例中，总体个数 $k = 3$，样本维数 $p = 4$。

3个总体的样本量$n_1=n_2=n_3 = 10$，总样本量$n = 30$。

假设3个总体均为**正态**，且协方差阵$\Sigma$相等但未知。 采用Wilks检验。

计算3个总体的样本离差阵为 $$ V_1=\begin{pmatrix} 204.74 & 203.56 & 224.07 & 165.01\\ 203.56 & 228.71 & 245.87 & 159.91\\ 224.07 & 245.87 & 295.35 & 189.77\\ 165.01 & 159.91 & 189.77 & 170.65 \end{pmatrix} \\ V_2=\begin{pmatrix} 173.66 & 150.15 & 191.63 & 192.39\\ 150.15 & 163.34 & 202.17 & 198.70\\ 191.63 & 202.17 & 287.38 & 259.35\\ 192.39 & 198.70 & 259.35 & 268.18 \end{pmatrix}\\ V_3=\begin{pmatrix} 244.64 & 205.11 & 236.86 & 239.73\\ 205.11 & 203.34 & 225.30 & 230.08\\ 236.86 & 225.30 & 277.15 & 258.73\\ 239.73 & 230.08 & 258.73 & 265.79 \end{pmatrix}\\ $$ 计算组内离差阵、组间离差阵为: $$ \text{SSW}=V_1 + V_2+V_3=\begin{pmatrix} 623.04 & 558.82 & 652.56 & 597.13\\ 558.82 & 595.40 & 673.34 & 588.69\\ 652.56 & 673.34 & 859.88 & 707.85\\ 597.13 & 588.69 & 707.85 & 704.62 \end{pmatrix} \\ \text{SSB}=\begin{pmatrix} 105.27 & 164.01 & 66.91 & 157.12\\ 164.01 & 261.15 & 82.68 & 218.02\\ 66.91 & 82.68 & 124.81 & 202.01\\ 157.12 & 218.02 & 202.01 & 361.31 \end{pmatrix} $$ 因此可以计算出Wilks检验统计量: $$ \Lambda=\frac{\vert\text{SSW}\vert}{\vert\text{SSW}+\text{SSB}\vert}=0.1068 $$ 记 $$ F=\frac{n - 2 - p}{p}\cdot\frac{1-\sqrt{\Lambda}}{\sqrt{\Lambda}}=12.3597 $$ 由于总体个数$k = 3$，有$F\stackrel{d}{\sim}F(2p,2(n - 2 - p))$.

因此检验的$p$值为$p = \Pr\{F(2p,2(n - 2 - p))\geq12.3597\}=2.0840\times10^{-9}$

**结论**：因为 p 值比 0.05 小得多，所以结论是有显著差异。如选用标准显著性水平 $\alpha = 0.05$，显然 p 值小于 0.05；如选用$\alpha = 0.01$ 或更严格标准，p 值依然小于这些标准。显然，我们有非常强的统计证据拒绝原假设，认为 3 种生产方法对完成生产任务有显著差异。

## 3.3.5 多元均值和方差的同时检验

设有$k$个相互独立的总体$X_{ij}\stackrel{d}{\sim}N_p(\mu_i,\Sigma_i)$，$\mu_i\in R^p$，$\Sigma_i > 0$。

$(x_{i1},\cdots,x_{in_i})$是来自总体$X_i$的样本，$1\leq i\leq k$。记$n=\sum_{i = 1}^{k}n_i$，$n\geq p + k$。

考虑检验问题： $$ \begin{cases} H_0:\mu_1=\cdots=\mu_k,\quad\Sigma_1=\cdots=\Sigma_k\\ H_1:\mu_1,\cdots,\mu_k不全相等，或\Sigma_1,\cdots,\Sigma_k不全相等 \end{cases} $$ 似然函数为 ： $$ L(\mu_1,\cdots,\mu_k,\Sigma_1,\cdots,\Sigma_k)=\prod_{i = 1}^{k}|\Sigma_i|^{-n_i/2}\exp\left\{-\frac{1}{2}\text{tr}\left(\sum_{i = 1}^{k}\Sigma_i^{-1}[V_i + n_i(\bar{x}_i - \mu_i)(\bar{x}_i - \mu_i)']\right)\right\} $$ 先考虑两个似然比 :  
$$ \begin{align} \lambda_1&=\frac{\sup_{\{\mu_1,\cdots,\mu_k,\Sigma\}}L(\mu_1,\cdots,\mu_k,\Sigma,\cdots,\Sigma)}{\sup_{\{\mu_1,\cdots,\mu_k,\Sigma_1,\cdots,\Sigma_k\}}L(\mu_1,\cdots,\mu_k,\Sigma_1,\cdots,\Sigma_k)} \\ &=\frac{n^{pn/2}\prod_{i = 1}^{k}|V_i|^{n_i/2}}{\prod_{i = 1}^{k}n_i^{pn_i/2}\cdot|\sum_{i = 1}^{k}V_i|^{n/2}}\\\\ \lambda_2&=\frac{\sup_{(\mu,\Sigma)}L(\mu,\cdots,\mu,\Sigma,\cdots,\Sigma)}{\sup_{(\mu_1,\cdots,\mu_k,\Sigma)}L(\mu_1,\cdots,\mu_k,\Sigma,\cdots,\Sigma)} \\ &=\left(\frac{|SSW|}{|SSW + SSB|}\right)^{n/2}\\ &=\left(\frac{|\sum_{i = 1}^{k}V_i|}{|\sum_{i = 1}^{k}\sum_{j = 1}^{n_i}(x_{ij}-\bar{x})(x_{ij}-\bar{x})'|}\right)^{n/2} \end{align} $$ 则总似然比为： $$ \begin{align} \lambda&=\frac{\sup_{(\mu,\Sigma)}L(\mu,\cdots,\mu,\Sigma,\cdots,\Sigma)}{\sup_{(\mu_1,\cdots,\mu_k,\Sigma_1,\cdots,\Sigma_k)}L(\mu_1,\cdots,\mu_k,\Sigma_1,\cdots,\Sigma_k)}\\ & =\lambda_1\lambda_2 \\ & =\frac{n^{pn/2}}{\prod_{i = 1}^{k}n_i^{pn_i/2}}\cdot\frac{\prod_{i = 1}^{k}|V_i|^{n_i/2}}{\left|\sum_{i = 1}^{k}\sum_{j = 1}^{n_i}(x_{ij}-\bar{x})(x_{ij}-\bar{x})'\right|^{n/2}} \end{align} $$ 很难推导似然比$\lambda$的精确分布，故用其渐近分布，也就是利用Wilks定理。 $$ \dim(\Theta)=k(p + p(p + 1)/2)=kp(p + 3)/2 $$ $$ \dim(\Theta_0)=p + p(p + 1)/2 $$ $$
 \dim(\Theta)-\dim(\Theta_0)=(k - 1)p(p + 3)/2 $$ 由Wilks定理知 : $$ - 2\log(\lambda)\stackrel{d}{\to}\chi^2((k - 1)p(p + 3)/2) $$ $$
 p = \Pr\{\chi^2((k - 1)p(p + 3)/2)\geq - 2\log(\lambda)\} $$ 若$p\leq\alpha$，则拒绝零假设。

思考下列检验问题：

  
| 检验问题 | 原假设$H_0$ | 备择假设$H_1$ |
| --- | --- | --- |
| 单样本协方差阵检验 | $H_0:\Sigma = \Sigma_0$ | $H_1:\Sigma\neq\Sigma_0$ |
| 单样本均值和协方差阵的联合检验 | $H_0:\mu = \mu_0,\Sigma = \Sigma_0$ | $H_1:\mu\neq\mu_0或\Sigma\neq\Sigma_0$ |
| 多总体协方差阵比较问题 | $H_0:\Sigma_1=\cdots=\Sigma$ | $d H_1:\Sigma_1,\cdots,\Sigma_k不全等$ |

> 参考思路：
> 
> 1.  计算似然比检验统计量。
> 2.  再由Wilks定理导出检验统计量的渐近分布。
> 3.  构造检验方案。

## 例：检验多总体协方差阵是否相等

![image-20241211113052807](https://cdn.jsdelivr.net/gh/SchwertLin/Pic/img/image-20241211113052807.png)**问题：3种生成方法的协方差阵是否相等？**

即3总体的协方差的比较问题： $$ H_0:\Sigma_1=\Sigma_2=\Sigma_3,\quad v.s.\quad H_1:\Sigma_1,\Sigma_2,\Sigma_3不全相等 $$ 检验的似然比为： $$ \begin{align} \lambda&=\frac{\sup_{(\mu_1,\mu_2,\mu_3,\Sigma)}L(\mu_1,\mu_2,\mu_3,\Sigma,\Sigma,\Sigma)}{\sup_{(\mu_1,\mu_2,\mu_3,\Sigma_1,\Sigma_2,\Sigma_3)}L(\mu_1,\mu_2,\mu_3,\Sigma_1,\Sigma_2,\Sigma_3)}\\ &=\frac{n^{pn/2}\prod_{i = 1}^{3}|V_i|^{n_i/2}}{\prod_{i = 1}^{3}n_i^{pn_i/2}\cdot|\sum_{i = 1}^{3}V_i|^{n/2}} \end{align} $$ 由Wilks定理知 （p=4, k=3, $n_1=n_2=n_3=10,n=30$）: $$ - 2\log(\lambda)\stackrel{d}{\to}\chi^2((k - 1)p(p + 1)/2) $$ $$  \begin{align} p &= \Pr\{\chi^2((k - 1)p(p + 1)/2)\geq - 2\log(\lambda)\}\\ &=Pr\{\chi^2(20)\ge-2\log(\lambda)\} \end{align} $$ 经计算，有 : $$ |V_1| = 5.0698\times 10^{6}, |V_2| = 4.2057\times 10^{6}, |V_3| = 7.2397\times 10^{5}, $$$$ |V| = |V_1 + V_2 + V_3| = 5.0218\times 10^{8},$$$$ - 2\log(\lambda)=24.631$$ $$
 p = Pr\{\chi^2(20)\geq - 2\log(\lambda)\}=Pr\{\chi^2(20)\geq 24.631\}=0.2159\gt0.05 $$ **结论**：没有足够证据拒绝零假设，即认为3个总体的协方差阵相等.

## 3.3.6 独立性检验

设$(x_1,\cdots,x_n)$是来自总体$X\sim N_p(\mu,\Sigma)$的独立样本， 其中$\mu\in R^p, \Sigma>0,n>p$。 将$X$和$\Sigma$分别剖分为 $$ X = \left( \begin{array}{c} X_1\\ \vdots\\ X_m \end{array} \right), \Sigma = \left( \begin{array}{ccc} \Sigma_{11}&\cdots&\Sigma_{1m}\\ \vdots&\ddots&\vdots\\ \Sigma_{m1}&\cdots&\Sigma_{mm} \end{array} \right) $$ 其中，$X_i\in R^{p_i}$，$\Sigma_{ij}$是$p_i\times p_j$的矩阵，$1\leq i,j\leq m$，$\sum_{i = 1}^{m}p_i = p$。

我们感兴趣的问题是：**$X_1,\cdots,X_m$ 是否相互独立？**

对应的检验问题为： $$ H_0:\Sigma_{ij} = 0, 1\leq i,\quad v.s.\quad H_1:\Sigma_{ij}不全为0, \quad 1\leq i<j\leq m $$ 考虑似然比检验。 似然函数为(去掉常数项) : $$ L(\mu,\Sigma)=\vert\Sigma\vert^{-n/2}\exp\left\{-\frac{1}{2}\text{tr}(\Sigma^{-1}(V + n(\bar{x}-\mu)(\bar{x}-\mu)'))\right\} $$ 我们将$\mu$，$\bar{x}$和$V$作相应剖分 : $$ \mu=\left(\begin{array}{c} \mu_{1} \\ \vdots \\ \mu_{m} \end{array}\right), \bar{x}=\left(\begin{array}{c} \bar{x}_{1} \\ \vdots \\ \bar{x}_{m} \end{array}\right), V=\left(\begin{array}{ccc} V_{11} & \cdots & V_{1m} \\ \vdots & & \vdots \\ V_{m1} & \cdots & V_{mm} \end{array}\right) $$ 在零假设$\Sigma_{ij} = 0(i\neq j)$下，似然函数为： $$ L_{0}(\mu_{1},\cdots,\mu_{m},\Sigma_{11},\cdots,\Sigma_{mm})\\ =\prod_{i = 1}^{m}|\Sigma_{ii}|^{-n/2}\exp\left\{-\frac{1}{2}\sum_{i = 1}^{m}\text{tr}(\Sigma_{ii}^{-1}[V_{ii}+n(\bar{x}_{i}-\mu_{i})(\bar{x}_{i}-\mu_{i})'])\right\} $$ 则似然比统计量为： $$ \begin{align} \lambda &= \frac{\sup_{(\mu_1,\cdots,\mu_m,\Sigma_{11},\cdots,\Sigma_{mm})} L_0(\mu_1,\cdots,\mu_m,\Sigma_{11},\cdots,\Sigma_{mm})}{\sup_{(\mu,\Sigma)} L(\mu,\Sigma)} \\&= \left( \frac{\left| V \right|}{\prod_{i = 1}^{m}\left| V_{ii} \right|}\right)^{n/2} \end{align} $$ 由Wilks定理知 $$ - 2 \log(\lambda) \stackrel{d}{\rightarrow} \chi^2\left(\frac{p^2 - \sum_{i = 1}^{m} p_i^2}2\right) $$ 其中自由度的计算如下： $$ \dim(\Theta) = p + p(p + 1)/2\\ \dim(\Theta_0) = p + \sum_{i = 1}^{m} p_i(p_i + 1)/2 \\ \dim(\Theta) - \dim(\Theta_0) = \left(p^2 - \sum_{i = 1}^{m} p_i^2\right)/2 $$

## 精确分布

考虑$m = 2$的情形. 此时$X$剖分为$p_1$维和$p_2$维两部分，$p_1 + p_2 = p$.

相应的似然比为$\lambda=\left(\frac{|V|}{\left|V_{11}\right|\cdot\left|V_{22}\right|}\right)^{n/2}$.

又由矩阵的分块运算知 $\left|V\right|=\left|\begin{matrix}V_{11}&V_{12}\\V_{21}&V_{22}\end{matrix}\right|=\left|V_{11}\right|\cdot\left|V_{22}-V_{21}V_{11}^{-1}V_{12}\right|$

因此 $$ \begin{align} \lambda&=\left(\frac{\left|V_{22}-V_{21}V_{11}^{-1}V_{12}\right|}{\left|V_{22}\right|}\right)^{\frac n 2} \\&=\left(\frac{\left|V_{22}-V_{21}V_{11}^{-1}V_{12}\right|}{\left|\left(V_{22}-V_{21}V_{11}^{-1}V_{12}\right)+V_{21}V_{11}^{-1}V_{12}\right|}\right)^{\frac n 2} \end{align} $$ 由于$V \stackrel{d}{\sim} W_p(n - 1,\Sigma)$，且在零假设下有 $\Sigma=\left(\begin{matrix}\Sigma_{11}&0\\0&\Sigma_{22}\end{matrix}\right)$， 由Wishart分布的独立分解性质知: 令$\Lambda=\lambda^{2 / n}=\vert V\vert/(\vert V_{11}\vert\cdot\vert V_{22}\vert)$，有$\Lambda\stackrel{d}{\sim}\Lambda_{p_{2},n - 1 - p_{1},p_{1}}$。 $$ \begin{align} \Lambda &= \frac{\vert V_{22}-V_{21}V_{11}^{-1}V_{12}\vert}{\vert(V_{22}-V_{21}V_{11}^{-1}V_{12})+V_{21}V_{11}^{-1}V_{12}\vert}\\ &\stackrel{d}{=} \frac{\vert W_{p_2}(n - 1 - p_1,\Sigma_{22})\vert}{\vert W_{p_2}(n - 1 - p_1,\Sigma_{22})+W_{p_2}(p_1,\Sigma_{22})\vert}\\ &\stackrel{d}{\approx} \Lambda_{p_2,n - 1 - p_1,p_1} \end{align} $$

 
| $p_1/p_2$ | 服从分布 |
| --- | --- |
| $p_{1}=1$ | $\frac{n - 1 - p_{2}}{p_{2}}\cdot\frac{1 - \Lambda}{\Lambda}\stackrel{d}{\sim}F(p_{2},n - 1 - p_{2})$ |
| $p_{1}=2$ | $\frac{n - 2 - p_{2}}{p_{2}}\cdot\frac{1 - \sqrt{\Lambda}}{\sqrt{\Lambda}}\stackrel{d}{\sim}F(2p_{2},2(n - 2 - p_{2}))$ |
| $p_{2}=1$ | $\frac{n - 1 - p_{1}}{p_{1}}\cdot\frac{1 - \Lambda}{\Lambda}\stackrel{d}{\sim}F(p_{1},n - 1 - p_{1})$ |
| $p_{2}=2$ | $\frac{n - 2 - p_{1}}{p_{1}}\cdot\frac{1 - \sqrt{\Lambda}}{\sqrt{\Lambda}}\stackrel{d}{\sim}F(2p_{1},2(n - 2 - p_{1}))$ |

特别地，当$p_1 = p_2 = 1$时，似然比和检验统计量分别为 : $$ \begin{align} \lambda&=\left(\frac{|V|}{|V_{11}| \cdot |V_{22}|}\right)^{n / 2}=\left(\frac{v_{11} v_{22}-v_{12}^{2}}{v_{11} v_{22}}\right)^{n / 2} \\ &=\left(1 - \frac{v_{12}^{2}}{v_{11} v_{22}}\right)^{n / 2}=\left(1 - r^{2}\right)^{n / 2}\\ \\ &\frac{n - 1 - p_1}{p_1} \cdot \frac{1 - \lambda^{2 / n}}{\lambda^{2 / n}}=(n - 2) \frac{r^{2}}{1 - r^{2}} \\ &\stackrel{d}{\sim} F(1, n - 2)\\ & \stackrel{d}{=} t^{2}(n - 2) \end{align} $$

## 例: 独立性检验

![image-20241212120340721](https://cdn.jsdelivr.net/gh/SchwertLin/Pic/img/image-20241212120340721.png)

**检验问题：$(x_1,x_3)$是否与$(x_2,x_4)$相互独立？**

$(x_1,x_2,x_3,x_4)$的样本离差阵V为： $$ V=\left(\begin{array}{cccc} 415.2&251.1& - 372.6& - 290.0\\ 251.1&2905.7& - 166.5& - 3041.0\\ - 372.6& - 166.5&492.3&38.0\\ - 290.0& - 3041.0&38.0&3362.0 \end{array}\right)\\ V_{11}=\left(\begin{array}{cc} 415.2& - 372.6\\ - 372.6&492.3 \end{array}\right), V_{22}=\left(\begin{array}{cc} 2905.7& - 3041.0\\ - 3041.0&3362.0 \end{array}\right) $$ $(x_1,x_3)$和$(x_2,x_4)$的样本离差阵分别为 $V_{11},V_{22}$, 样本量$n = 13$。

计算离差阵的行列式有：$\vert V\vert=2.1321\times10^9,\vert V_{11}\vert=6.5572\times 10^4,\vert V_{22}\vert=5.2128\times10^5$, 似然比统计量的值为： $$ \Lambda=\lambda^{\frac 2 n}=\lambda^{\frac 2 13}=\frac{\vert V\vert}{\vert V_{11}\vert · \vert V_{22}\vert}=0.0624 $$ 由于$p_1=p_2=2,n=13$, 检验统计量、p值为: $$ \frac{n-2-p_1}{p_1}·\frac{1-\sqrt \Lambda}{\sqrt \Lambda}=\frac 9 2·\frac{1- \lambda^{\frac 1 {13}}}{\lambda^{\frac 1 {13}}}=13.514$$ $$\begin{align} p&=Pr\{F(2p_1,2(n-2-p_1))\ge13.514\}\\ &=Pr\{F(4,18)\ge 13.514\}\\ &=2.94\times 10^{-5}<0.05 \end{align} $$ **结论：** 拒绝原假设，认为$(x_1,x_3)$不与$(x_2,x_4)$相互独立。

> 当$m = p$时，似然比为: $$ \lambda = \left( \frac{\vert V \vert}{\prod_{i = 1}^{p} v_{ii}} \right)^{n/2} = \vert R \vert^{n/2} $$ 可由样本相关系数矩阵$R$的分布给出检验方案。

## 3.3.7 条件独立性检验

将$X$剖分为$q_1$维和$q_2$维两部分，$q_1 + q_2=p$，并对$\Sigma$作相应剖分，有: $$ X=\begin{pmatrix}X_1\\X_2\end{pmatrix},\quad \Sigma=\begin{pmatrix}\Sigma_{11}&\Sigma_{12}\\\Sigma_{21}&\Sigma_{22}\end{pmatrix} $$ 因此，在$X_2$给定下$X_1$的条件协方差阵为: $$ T = Cov(X_1|X_2)=\Sigma_{1|2}=\Sigma_{11}-\Sigma_{12}\Sigma_{22}^{-1}\Sigma_{21} $$ 再将$X_1$和条件协方差阵$T$作剖分 : $$ X_1=\begin{pmatrix}X_{11}\\\vdots\\X_{1m}\end{pmatrix},\quad T=\begin{pmatrix}T_{11}&\cdots&T_{1m}\\\vdots&\ddots&\vdots\\T_{m1}&\cdots&T_{mm}\end{pmatrix} $$ 其中$X_{1i}$为$p_i$维向量，$1\leq i\leq m,\sum_{i = 1}^{m}p_i=q_1$, $T_{ij}$是$p_i\times p_j$的矩阵，$1\leq i,j\leq m$。

> **理解每个$X_{1i}$为$p_i$维：**
> 假设我们在研究某种疾病的患者数据，收集了以下几类信息：
> $X_1$ :健康指标

| $X_{11}$: 血压                       | $X_{12}$:血糖水平                    | $X_{13}$: 胆固醇水平                          |
| ---------------------------------- | -------------------------------- | ---------------------------------------- |
| 收缩压（Systolic Blood Pressure, SBP）  | 空腹血糖（Fasting Blood Glucose, FBG） | 总胆固醇（Total Cholesterol, TC）              |
| 舒张压（Diastolic Blood Pressure, DBP） |                                  | 高密度脂蛋白胆固醇（High-Density Lipoprotein, HDL） |
|                                    |                                  | 低密度脂蛋白胆固醇（Low-Density Lipoprotein, LDL）  |

> X₂人口统计信息: 年龄（Age）、性别（Gender）
> **变量划分**：
> 总体变量： $X = (X_1, X_2)$ p=8
> +   $q_1 = 2 + 1 + 3 = 6$（血压2维，血糖1维，胆固醇3维）。
> +   $q_2 = 2$（年龄1维，性别1维）。
> 对$X_1$有： $$ X_1= \begin{pmatrix} X_{11} \\ X_{12} \\ X_{13} \end{pmatrix},X_{11} = \begin{pmatrix} \text{SBP} \\ \text{DBP} \end{pmatrix},X_{12} = \begin{pmatrix} \text{FBG} \end{pmatrix},X_{13} = \begin{pmatrix} \text{TC} \\ \text{HDL} \\ \text{LDL} \end{pmatrix} $$ 所以，有$\sum^m_{i=1}p_i=q_i$.总的来说，是对一个$p\times n$的多元正态总体的**n**在不断的划分。

感兴趣的问题是：**在给定$X_2$的条件下，$X_1$的分量$X_{11},\cdots,X_{1m}$是否相互独立？**

对应的检验问题为: $$ H_0:T_{ij} = 0,1\leq i<j\leq m,\quad v.s.\quad H_1:T_{ij}不全为0,\quad1\leq i<j\leq m $$

## A. 检验统计量的构造

将样本离差阵$V$作相应剖分 $V=\begin{pmatrix}V_{11}&V_{12}\\V_{21}&V_{22}\end{pmatrix}$， 计算在$X_2$给定后$X_1$的样本条件离差阵 $W = V_{1|2}=V_{11}-V_{12}V_{22}^{-1}V_{21}$。

由于$V\stackrel{d}{\sim}W_p(n - 1,\Sigma)$，有 $W\stackrel{d}{\sim}W_{q_1}(n - q_2 - 1,\Sigma_{1|2})$。

> 注意：此时，$W$可以看成是:
> +   均值为 $\mu_{1|2}=E(X_1|X_2=x_2)=\mu_1+\Sigma_{12}\Sigma_{22}^{-1}(x_2-\mu_2)$
> +   协方差阵为 $\Sigma_{1|2}=Cov(X_1|X_2=x_2)=\Sigma_{11}-\Sigma_{12}\Sigma_{22}^{-1}\Sigma_{21}$
> 的$q_1$维正态总体的$n - q_2$个(虚拟)独立样本的样本离差阵。

再将样本条件离差阵$W$作相应剖分: $$ W=\begin{pmatrix}W_{11}&\cdots&W_{1m}\\\vdots&\ddots&\vdots\\W_{m1}&\cdots&W_{mm}\end{pmatrix} $$ 其中，$W_{ij}$是$p_i\times p_j$的矩阵，$1\leq i,j\leq m$。

相似地，基于这组虚拟样本，可得检验的似然比为 : $$ \eta=\left(\frac{\prod_{i = 1}^{m}|W_{ii}|}{|W|}\right)^{-(n - q_2)/2} $$ 再利用3.3.6中的**独立性检验**结果导出检验统计量的精确分布或渐近分布。

![image-20241212231349854](https://cdn.jsdelivr.net/gh/SchwertLin/Pic/img/image-20241212231349854.png)

## 例：条件独立性检验

![image-20241212120340721](https://cdn.jsdelivr.net/gh/SchwertLin/Pic/img/image-20241212120340721.png)

**检验问题：给定$(x_1,x_2)$的条件下，$y$与$(x_3,x_4)$是否相互独立？**

$(x_1,x_2,x_3,x_4,y)$的样本离差阵为 : $$ V=\begin{pmatrix}415.2&251.1&- 372.6&- 290.0&776.0\\251.1&2900.5&- 166.5&- 3041.0&2293.0\\- 372.6&- 166.5&492.3&38.0&- 618.2\\- 290.0&- 3041.0&38.0&3362.0&- 2481.7\\776.0&2293.0&- 618.2&- 2481.7&2715.8\end{pmatrix} $$ 经计算，可得给定$(x_1,x_2)$的条件下，$(x_3,x_4,y)$的样本条件离差阵为 : $$ W=\begin{pmatrix}156.68&- 161.08&39.17\\- 161.08&177.51&- 41.99\\39.17&- 41.99&57.91\end{pmatrix} $$ 本例中，$q_1 = 3$，$q_2=2$，$n = 13$，因此样本量变为虚拟样本量: $$ m=n - q_2=13 - 2 = 11$$ $$W_{11}=\begin{pmatrix}156.68&- 161.08\\- 161.08&177.51\end{pmatrix},w_{22}=57.91 $$ 因此，条件独立性检验的似然比的值为 : $$ \begin{align} \lambda&=\left(\frac{\vert W\vert}{\vert W_{11}\vert\cdot\vert w_{22}\vert}\right)^{m/2}=\left(\frac{\vert W\vert}{\vert W_{11}\vert\cdot\vert w_{22}\vert}\right)^{11/2}=0.8256^{11/2}\\\\ \Lambda&=\lambda^{2/m}=0.8256 \end{align} $$ 本例中，$p_1 = 2$，$p_2 = 1$，虚拟样本量$m = 11$ 检验统计量的值为 : $$ F=\frac{m - 1 - p_1}{p_1}\cdot\frac{1-\Lambda}{\Lambda}=\frac{11 - 1 - 2}{2}\cdot\frac{1 - 0.8256}{0.8256}=0.8397 $$ 检验的$p$值为 $p=\text{Pr}\{F(p_1,m - 1 - p_1)\geq0.8397\}$ $=\text{Pr}\{F(2,8)\geq0.8397\}$ $=0.466$ 结论：不能拒绝给定$(x_1,x_2)$的条件下，$y$与$(x_3,x_4)$相互独立的假设。

![image-20241212235252315](https://cdn.jsdelivr.net/gh/SchwertLin/Pic/img/image-20241212235252315.png)

## 作业：两总体均值检验

设 $X\stackrel{d}{\sim}N_p(\mu_1,\Sigma)$ 和 $Y\stackrel{d}{\sim}N_p(\mu_2,\Sigma)$ 是两个相互独立的 $p$ 维正态总体，其中 $\Sigma>0$ 未知。设 $x_1,\cdots,x_m$ 是来自总体 $X$ 的 $m$ 个独立样本，$y_1,\cdots,y_n$ 是来自总体 $Y$ 的 $n$ 个独立样本，其中 $m + n\geq p + 2$。 请给出如下检验问题的检验方案 : $$ H_0:\mu_1 = -\mu_2,\quad v.s.\quad H_1:\mu_1\neq-\mu_2 $$ $\Sigma$相等，所以和Berman-Fisher检验问题无关。就是单纯的两总体的均值比较问题，但是注意假设中有负号。

**①线性变换：令$\widetilde Y=-Y\sim N_p(-\mu_2,\Sigma),\mu_1=-\mu_2=\widetilde \mu_2,\widetilde \mu_2=E[\widetilde Y]$**后续就按最普通的进行计算即可。

**②根据似然比做**：直接比较在原假设和备择假设下的最大似然值，判断是否拒绝原假设。

在$H_0$下: $$ \hat\mu_1=\frac{m\bar x-n\bar y}{m+n},\hat\mu_2=\frac{n\bar y-m\bar x}{m+n}\\\\ \hat \Sigma=\frac{1}{m+n}[V+\frac{mn}{m+n}(\bar x+\bar y)(\bar x+\bar y)'] $$ 题目给出$\Sigma$未知，此时样本离差阵$V=V_1+V_2$. $(\mu_1,\mu_2,\Sigma)$的似然函数为：  
$$ L(\mu_1,\mu_2,\Sigma)=\vert\Sigma\vert^{-(m + n)/2}\times\\ \exp\left\{-\frac{1}{2}\text{tr}[\Sigma^{-1}(V + m(\bar{x}-\mu_1)(\bar{x}-\mu_1)' + n(\bar{y}-\mu_2)(\bar{y}-\mu_2)')]\right\} $$ 检验问题的似然比为: $$ \begin{align} \lambda&=\frac{\sup_{\{\mu,\Sigma\}}L(\mu,\mu,\Sigma)}{\sup_{\{\mu_1,\mu_2,\Sigma\}}L(\mu_1,\mu_2,\Sigma)}\\ &=\left(\frac{\vert V_1+V_2 + \frac{mn}{m+n}(\bar{x}+\bar{y})(\bar{x}+\bar{y})'\vert}{\vert V_1+V_2\vert}\right)^{-(m + n)/2}\\ &=\left(1+\frac{mn}{m + n}(\bar{x}+\bar{y})'(V_1+V_2)^{-1}(\bar{x}+\bar{y})\right)^{-(m + n)/2} \end{align} $$ 令 : $$ T^2=\frac{mn(m + n - 2)}{m + n}(\bar{x}+\bar{y})'V^{-1}(\bar{x}+\bar{y})\\\\ T^2\vert_{H_0}\stackrel{d}{\sim}T^2_p(m + n - 2) $$ 因此，当 $\frac{(m + n - p - 1)}{(m + n - 2)p}T^2>F_{1-\alpha}(p,m + n - p - 1)$ 时拒绝零假设， 其犯第一类错误的概率为 $\alpha$。

> **Q: $\hat\mu_1=\frac{m\bar x-n\bar y}{m+n},\hat\mu_2=\frac{n\bar y-m\bar x}{m+n}$是怎么得到？**
> A: 通过极大似然估计得到，下面是具体过程。
> 我们有两个独立的 $p$ 维正态总体：$X~N_p(\mu_1,\Sigma),Y~N_p(\mu_2,\Sigma)$
> 其中，协方差矩阵 $\Sigma$ 是相同的且未知的。我们从每个总体中分别抽取了独立的样本：
> +   总体 $X$：样本 $x_1, x_2, \cdots , x_m$
> +   总体 $Y$：样本 $y_1, y_2, \cdots , y_n$
> 样本量满足 $m + n p + 2$，以确保检验的有效性。我们要检验的假设为：
> $$ H_0: \mu_1 = -\mu_2 \quad \text{vs.} \quad H_1: \mu_1 \neq -\mu_2 $$
> **步骤1：构造似然函数**: 对于两个总体 $X$ 和 $Y$，其联合似然函数为两个独立正态分布的乘积：
> $$ L(\mu_1, \mu_2, \Sigma) = L_X(\mu_1, \Sigma) \times L_Y(\mu_2, \Sigma) $$ $$ L_X(\mu_1, \Sigma) = \prod_{i=1}^m \frac{1}{(2\pi)^{p/2} |\Sigma|^{1/2}} \exp\left( -\frac{1}{2} (x_i - \mu_1)^\top \Sigma^{-1} (x_i - \mu_1) \right)$$ $$ L_Y(\mu_2, \Sigma) = \prod_{j=1}^n \frac{1}{(2\pi)^{p/2} |\Sigma|^{1/2}} \exp\left( -\frac{1}{2} (y_j - \mu_2)^\top \Sigma^{-1} (y_j - \mu_2) \right)$$ $$ L(\mu_1, \mu_2, \Sigma) = \frac{1}{(2\pi)^{(m+n)p/2} |\Sigma|^{(m+n)/2}} \exp\left( -\frac{1}{2} \left[ \sum_{i=1}^m (x_i - \mu_1)^\top \Sigma^{-1} (x_i - \mu_1) + \sum_{j=1}^n (y_j - \mu_2)^\top \Sigma^{-1} (y_j - \mu_2) \right] \right)\\ $$ **步骤2：对数似然函数**为了简化计算，我们取对数似然函数： $$ \begin{align} &\ell(\mu_1, \mu_2, \Sigma)= \log L(\mu_1, \mu_2, \Sigma) \\ &=-\frac{(m+n)p}{2} \log(2\pi) - \frac{(m+n)}{2} \log |\Sigma| - \frac{1}{2} \left[ \sum_{i=1}^m (x_i - \mu_1)^\top \Sigma^{-1} (x_i - \mu_1) + \sum_{j=1}^n (y_j - \mu_2)^\top \Sigma^{-1} (y_j - \mu_2) \right] \end{align} $$ **步骤3：在原假设 $ H_0 $ 下最大化似然函数**: 在原假设 $ H_0: _1 = -_2 $ 下，我们有 $ _2 = -_1 $。因此，对数似然函数变为： $$ \ell(\mu_1, \Sigma) = -\frac{(m+n)p}{2} \log(2\pi) - \frac{(m+n)}{2} \log |\Sigma| - \frac{1}{2} \left[ \sum_{i=1}^m (x_i - \mu_1)^\top \Sigma^{-1} (x_i - \mu_1) + \sum_{j=1}^n (y_j + \mu_1)^\top \Sigma^{-1} (y_j + \mu_1) \right]\\\\ $$
> 求导： $$ \begin{align} \frac{\partial \ell}{\partial \mu_1} = \sum_{i=1}^m \Sigma^{-1} (x_i - \mu_1) - \sum_{j=1}^n \Sigma^{-1} (y_j + \mu_1) &= 0\\ \sum_{i=1}^m (x_i - \mu_1) &= \sum_{j=1}^n (y_j + \mu_1)\\ \sum_{i=1}^m x_i - m\mu_1 &= \sum_{j=1}^n y_j + n\mu_1\\ \sum_{i=1}^m x_i - \sum_{j=1}^n y_j &= (m + n)\mu_1\\ \mu_1 = \frac{\sum_{i=1}^m x_i - \sum_{j=1}^n y_j}{m + n} &= \frac{m\bar{x} - n\bar{y}}{m + n} \end{align} $$
> 由于 $ _2 = -_1 $，则$_2 = $
> 对 $ $ 的求偏导数同理。
> 1.  对数似然函数中涉及 $ $ 的部分：
> $$ -\frac{(m+n)}{2} \log |\Sigma| - \frac{1}{2} \text{tr}\left[ \Sigma^{-1} \left( \sum_{i=1}^m (x_i - \mu_1)(x_i - \mu_1)^\top + \sum_{j=1}^n (y_j + \mu_1)(y_j + \mu_1)^\top \right) \right] $$
> 2.  对 $ $ 的偏导数为零：
> $$ -\frac{(m+n)}{2} \Sigma^{-1} + \frac{1}{2} \Sigma^{-1} \left( \sum_{i=1}^m (x_i - \mu_1)(x_i - \mu_1)^\top + \sum_{j=1}^n (y_j + \mu_1)(y_j + \mu_1)^\top \right) \Sigma^{-1} = 0 $$
> 3.  解得：
> $$\begin{align} \Sigma &= \frac{1}{m + n} \left( \sum_{i=1}^m (x_i - \mu_1)(x_i - \mu_1)^\top + \sum_{j=1}^n (y_j + \mu_1)(y_j + \mu_1)^\top \right)\\ \hat{\Sigma} &= \frac{1}{m + n} \left[ V_X + V_Y + \frac{mn}{m + n} (\bar{x} + \bar{y})(\bar{x} + \bar{y})^\top \right]\\ V_X &= \sum_{i=1}^m (x_i - \bar{x})(x_i - \bar{x})^\top, \quad V_Y = \sum_{j=1}^n (y_j - \bar{y})(y_j - \bar{y})^\top \end{align}$$

