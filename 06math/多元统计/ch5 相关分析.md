
# 5.0 例：家庭特征与家庭消费之间的关系

![image-20241213235458701](https://cdn.jsdelivr.net/gh/SchwertLin/Pic/img/image-20241213235458701.png)

统计分析方法：**典型相关分析**

> 典型相关分析：研究两组变量之间相关性的一种统计分析方法，也是一种**降维**技术。

# 5.1 复相关系数

> 之前我们评估两个随机变量$X,Y$之间的相关程度，使用的是Pearson相关系数：$\rho(X,Y)=\frac{Cov(X,Y)}{\sqrt{Var(X)Var(Y)}}$. **但当X 和 Y 其中之一换成随机向量时，Pearson相关系数就不再适用。**
> 
> 为衡量随机变量和随机向量、随机向量和随机向量之间的相关程度，一个常用的方法就是**采用线性投影，讲随机向量通过某个线性变化投影成一元随机变量**，然后就可以采用两变量的相关系数来定义随机变量和随机向量、随机向量和随机向量之间的相关程度。

相关关系：

| 两个单变量之间 | 一个单变量与一个向量之间 | 两个向量之间 |
| --- | --- | --- |
| "一对一" | "一对多" | "多对多" |
| (简单)相关系数、偏相关系数 | 复相关系数 | 典型相关系数 |

## 5.1.1 总体复相关系数

设随机向量$Y \sim N_p(\mu, \Sigma)$，其中$\Sigma>0$。

将$Y$，$\mu$和$\Sigma$分别剖分为： $$ Y = \begin{pmatrix} y_1 \\ Y_2 \end{pmatrix}, \quad \mu = \begin{pmatrix} \mu_1 \\ \mu_2 \end{pmatrix}, \quad \Sigma = \begin{pmatrix} \sigma_{11} & \Sigma_{12} \\ \Sigma_{21} & \Sigma_{22} \end{pmatrix} $$ 其中，$y_1, \mu_1 \in\mathbb{R}^1$；$\sigma_{11}>0$；$Y_2, \mu_2, \Sigma_{21}=\Sigma_{12}' \in\mathbb{R}^{p - 1}$；$\Sigma_{22}$是$(p - 1)$阶正定阵。

考虑$y_1$与$a'Y_2$之间的简单相关系数，其中$a \in\mathbb{R}^{p - 1}$， $$ \begin{align} \rho_{y_1,a'Y_2} &= \frac{\text{Cov}(y_1,a'Y_2)}{\sqrt{\text{Var}(y_1)}\sqrt{\text{Var}(a'Y_2)}} = \frac{\text{Cov}(y_1,Y_2)a}{\sqrt{\sigma_{11}}\sqrt{a'\text{Var}(Y_2)a}}\\ &= \frac{\Sigma_{12}a}{\sqrt{\sigma_{11}}\sqrt{a'\Sigma_{22}a}} \end{align} $$ 则定义$y_1$与$Y_2$的复相关系数为: $$ \rho_{y_1,Y_2} = \sup_{a \in R^{p - 1}} \rho_{y_1,a'Y_2} = \frac{1}{\sqrt{\sigma_{11}}} \sup_{a \in R^{p - 1}} \frac{\Sigma_{12}a}{\sqrt{a'\Sigma_{22}a}} $$ 由$\rho_{y_1,Y_2}$的非负性、Cauchy - Schwarz不等式知 : $$ \rho_{y_1,Y_2} = \frac{1}{\sqrt{\sigma_{11}}} \sqrt{\sup_{a \in R^{p - 1}} \frac{(\Sigma_{12}a)^2}{a'\Sigma_{22}a}} = \sqrt{\frac{\Sigma_{12}\Sigma_{22}^{-1}\Sigma_{21}}{\sigma_{11}}} $$ 上式在$a = c\Sigma_{22}^{-1}\Sigma_{21}$达最大, c是任一非零常数。$a = \Sigma_{22}^{-1}\Sigma_{21}$对应线性模型中的回归系数：$y_1=a_0+a'Y_2+\varepsilon$, $E(y_1|Y_2)=a_0+a'X,\varepsilon$是随机误差。**这就是复相关系数的平方$\rho^2(X,Y)$常被用于刻画线性模型拟合程度的一个原因。**

**定理 1**: 当$a = \Sigma_{22}^{-1}\Sigma_{21}$时，$y_1-a'Y_2$的方差取得最小值：$\sigma_{11}-\Sigma_{12}\Sigma_{22}^{-1}\Sigma_{21}=\text{Var}(y_1|Y_2)$，$y_1$与$a'Y_2+a_0$最接近，$a+0=E(y_1)-a'E(Y_2)$。

$y_1$与$a'Y_2$的相关系数最大，为复相关系数$\rho_{y_1,Y_2}$，本质上刻画了$y_1$和$Y_2$的线性相关程度。

> **证明**： 对任意$b \in\mathbb{R}^{p - 1}$，有 : $$ \begin{align} \text{Var}(y_1 - b'Y_2)&=\text{Var}[(y_1 - a'Y_2)+(a - b)'Y_2]\\ &=\text{Var}(y_1 - a'Y_2)+(a - b)'\text{Cov}(Y_2)(a - b)\\&+2\text{Cov}[(y_1 - a'Y_2),(a - b)'Y_2] \end{align} $$ 由于$a = \Sigma_{22}^{-1}\Sigma_{21}$，则有: $$ \begin{align} \text{Cov}[(y_1 - a'Y_2),Y_2]&=\text{Cov}(y_1,Y_2)-a'\text{Cov}(Y_2,Y_2)\\ &=\Sigma_{12}-a'\Sigma_{22}\\ &=0 \end{align} $$ 方差关系有： $$ $$\begin{align} Var(y_1 - b'Y_2) &= Var(y_1 - a'Y_2)+(a - b)'Var(Y_2)(a - b)\\ &= Var(y_1 - a'Y_2)+(a - b)'\Sigma_{22}(a - b)\\ &\geq Var(y_1 - a'Y_2) \\\\ Var(y_1 - a'Y_2) &= Var(y_1)+Var(a'Y_2)-2Cov(y_1,a'Y_2)\\ &= \sigma_{11}+\Sigma_{12}\Sigma_{22}^{-1}\Sigma_{21}-2\Sigma_{12}\Sigma_{22}^{-1}\Sigma_{21}\\ &= \sigma_{11}-\Sigma_{12}\Sigma_{22}^{-1}\Sigma_{21}\\ &= Var(y_1|Y_2) \end{align}$$ $$ 由定理1知：$Var(y_1 - a'Y_2)$达最小意味着$y_1-\mu_1$与$a'Y_2 - a'\mu_2$最接近，即$y_1$与$(\mu_1 - a'\mu_2)+a'Y_2$最接近。
> 
> **因此可以用$(p - 1)$个预报因子$Y_2$的线性组合来预测单个因变量$y_1$，其最优斜率为$a$，最优截距为$(\mu_1 - a'\mu_2)$。**
> 
> 注意到： $$ \begin{align} E(y_1|Y_2) &= \mu_1+\Sigma_{12}\Sigma_{22}^{-1}(Y_2 - \mu_2)\\ &= \mu_1+a'(Y_2 - \mu_2)\\ &= (\mu_1 - a'\mu_2)+a'Y_2 \end{align} $$ 条件期望是最优(方差最小)的线性预测。

## 复相关系数定义(变量-向量之间)

变量$y_1$与向量$Y_2$之间的复相关系数为 $*{y_1,Y_2} = $其中，$*{11}=(y_1)$，$*{22}=(Y_2)$，$*{12}=(y_1,Y_2)$。

**复相关系数$\rho_{y_1,Y_2}$的性质**：

1.  $0 \leq \rho_{y_1,Y_2} \leq 1$；
2.  $\rho_{y_1,Y_2}$越大则$y_1$与$Y_2$的相关性越强；
3.  $\rho_{y_1,Y_2}=0 \Leftrightarrow \Sigma_{12}=0$，即$y_1$与$Y_2$独立。

## 5.1.2 样本复相关系数

> 在实际应用中，我们通常没有总体的参数，而是通过样本来估计这些参数。
> 
> 样本复相关系数 r 是总体复相关系数 $\rho$ 的一个估计。样本复相关系数 r 的形式类似于总体复相关系数，但由于样本的有限性，样本复相关系数会受到抽样误差的影响。为了提高估计的准确性，样本的数量越多，估计的准确性也越高。

设总体$X\stackrel{d}{\sim}N_{p}(\mu,\Sigma)$，其样本为$x_1,\cdots,x_n$。考虑$X$的剖分$X=(x^{(1)},(X^{(2)})')'$。

记$\bar{x}$，$V$和$S$分别为样本均值、样本离差阵和样本协差阵，并对它们作相应剖分。

则由$x^{(1)}$与$X^{(2)}$的复相关系数: $$ \rho_{x^{(1)},X^{(2)}}=\sqrt{\frac{\Sigma_{12}\Sigma_{22}^{-1}\Sigma_{21}}{\sigma_{11}}} $$ 定义$x^{(1)}$与$X^{(2)}$的样本复相关系数为: $$ r_{x^{(1)},X^{(2)}}=\sqrt{\frac{V_{12}V_{22}^{-1}V_{21}}{v_{11}}} $$ 以及$a$的估计为$\hat{a}=V_{22}^{-1}V_{21}$。不难知道，它们分别是复相关系数$\rho_{x^{(1)},X^{(2)}}$和方向$a$的极大似然估计。

> **修正的样本复相关系数**  
> $$ (r_{x^{(1)},X^{(2)}}^^2 = r_{x^{(1)},X^{(2)}}^2-\frac{p - 1}{n - p}(1 - r_{x^{(1)},X^{(2)}}^2) $$ 用途：
> 
> +   当$p = 1$时，修正的样本复相关系数=样本复相关系数;
> +   当$p\geq2$时，修正的样本复相关系数<样本复相关系数。
> 
> 在对线性回归模型做模型选择时，常用修正的样本相关系数来判断是否再选入一个预报因子。

## 样本复相关系数的分布

### $\Sigma_{12}=0$的情形：$x^{(1)}$与$X^{(2)}$独立

由Wishart分布的独立分解性质知，

> $t_1$:衡量残差方差的量,在 $x^{(1)}$和 $X^{(2)}$ 独立的情形下，$t_1$ 会服从自由度为 $n - p$ 的卡方分布 $\chi^2(n - p)$，因为它的形式类似于在进行回归分析时残差平方和的分布。
> 
> $t_2$:是标准化后的 $V_{21}$（$X^{(2)}$ 和$x^{(1)}$ 之间的协方差向量）。我们通过乘以 $V_{22}^{-\frac 1 2}$ 来标准化它。

$$ \begin{align} t_1 &= v_{11}-V_{12}V_{22}^{-1}V_{21}\stackrel{d}{\sim}\sigma_{11}\chi^2(n - p)\\ t_2 &= V_{22}^{-1/2}V_{21}\stackrel{d}{\sim}N_{p - 1}(0,\sigma_{11}I_{p - 1}) \end{align} $$

且$t_1$与$t_2$独立。因此， $$ \begin{align}F&=\frac{n - p}{p - 1}\cdot\frac{r_{x^{(1)},X^{(2)}}^2}{1 - r_{x^{(1)},X^{(2)}}^2}\\ &=\frac{n - p}{p - 1}\cdot\frac{V_{12}V_{22}^{-1}V_{21}}{v_{11}-V_{12}V_{22}^{-1}V_{21}}\\ &=\frac{t_2^2/(p - 1)}{t_1/(n - p)}\stackrel{d}{\sim}F(p - 1,n - p)\end{align} $$ 则由$F$可以检验$x^{(1)}$与$X^{(2)}$是否相互独立。

> 注：该检验与3.3.6中独立性检验在$m = 2$的情形一致。

### 一般情形

考虑变换$Y=\text{diag}(\sigma_{11}^{-\frac 1 2},\Sigma_{22}^{-\frac 1 2})X=\begin{pmatrix}\sigma_{11}^{-\frac 1 2}&0\\0&\Sigma_{22}^{-\frac 1 2}\end{pmatrix}X$，并对$Y$作相同剖分: $$ Y=\begin{pmatrix}y^{(1)}\\Y^{(2)}\end{pmatrix}=\begin{pmatrix}\sigma_{11}^{-\frac 1 2}x^{(1)} \\ \Sigma_{22}^{-\frac 1 2}X^{(2)}\end{pmatrix}\\ Y\stackrel{d}{\sim}N_{p}\left(\begin{pmatrix}\sigma_{11}^{-\frac 1 2}\mu_1\\\Sigma_{22}^{-\frac 1 2}\mu_2\end{pmatrix},\begin{pmatrix}1&\sigma^{-\frac 1 2}_{11}\Sigma_{12}\Sigma_{22}^{-\frac 1 2}\\\sigma^{-\frac 1 2}_{11}\Sigma_{22}^{-\frac 1 2}\Sigma_{21}&I_{p - 1}\end{pmatrix}\right)\\\\ \rho_{y^{(1)},Y^{(2)}}=\Sigma_{12}\Sigma_{21}=\sqrt{\frac{\Sigma_{12}\Sigma_{22}^{-1}\Sigma_{21}}{\sigma_{11}}}=\rho_{x^{(1)},X^{(2)}} $$ 因此，不失一般性，可以假设$X$的协差阵为 $\Sigma=\begin{pmatrix}1&\Sigma_{12}\\\Sigma_{21}&I_{p - 1}\end{pmatrix}$ ,

此时有$\rho_{x^{(1)},X^{(2)}}=\Sigma_{12}\Sigma_{21}$。简记$\rho=\rho_{x^{(1)},X^{(2)}}$。

> **对上述结果的解释说明**：
> 
> Y的均值、方差按照$E[Y]=E[AX]=AE[X],D[Y]=D[AX]=AD[X]A'$计算。
> 
> 有$X=\begin{pmatrix}x^{(1)}\\X^{(2)} \end{pmatrix}\sim N_p(\mu,\Sigma)=N_p\left\{\begin{pmatrix}\mu^{(1)}\\\mu^{(2)} \end{pmatrix},\begin{pmatrix}\sigma_{11}&\Sigma_{12}\\\Sigma_{21}&\Sigma_{22} \end{pmatrix}\right\}$,
> 
> 所以$Y\stackrel{d}{\sim}N_{p}\left(\begin{pmatrix}\sigma_{11}^{-\frac 1 2}\mu_1\\\Sigma_{22}^{-\frac 1 2}\mu_2\end{pmatrix},\begin{pmatrix}1&\sigma^{-\frac 1 2}_{11}\Sigma_{12}\Sigma_{22}^{-\frac 1 2}\\\sigma^{-\frac 1 2}_{11}\Sigma_{22}^{-\frac 1 2}\Sigma_{21}&I_{p - 1}\end{pmatrix}\right)$.
> 
> 对协方差矩阵进行标准化后，每个部分的方差（如 $y^{(1)}$ 和 $Y^{(2)}$ 的方差）变为 1。所以内部向量都是独立同分布的，二者的相关性就体现在$\sigma^{-\frac 1 2}_{11}\Sigma_{22}^{-\frac 1 2}\Sigma_{21}$上。
> 
> **Q: 为什么可以假设$X$的协差阵为 $\Sigma=\begin{pmatrix}1&\Sigma_{12}\\\Sigma_{21}&I_{p - 1}\end{pmatrix}$ ?**
> 
> A: 因为我们通过线性变换$Y=AX$已经证明这两个分量，本身内部都是独立同分布的。
> 
> 通过标准化$x^{(1)}$ 和$X^{(2)}$的方差结构，使得我们可以更加集中于研究$x^{(1)}$ 与$X^{(2)}$之间的相关性，而不需要处理不同变量之间的不同单位和规模。

由Wishart分布的性质知：

1.  $V_{22} \stackrel{d}{\sim} W_{p - 1}(n - 1, I_{p - 1})$；
2.  $t_1 = v_{11}-V_{12}V_{22}^{-1}V_{21} \stackrel{d}{\sim} \sigma_{11}\chi^2(n - p)$，$\sigma_{11}=1 - \rho^2$；
3.  在$V_{22}$给定的条件下，$t_2 = V_{22}^{-\frac 1 2}V_{21} \stackrel{d}{\sim} N_{p - 1}(0, \sigma_{11}I_{p - 1})$；
4.  $t_1$与$(t_2, V_{22})$相互独立。

则在$V_{22}$给定的条件下，根据条件独立性，u 服从一个加权的非中心卡方分布；而u的非中心参数又服从另外一个加权的卡方分布： $$ u = t_{2}'{t}_{2}=V_{12}V_{22}^{-1}V_{21} \stackrel{d}{\sim} (1 - \rho^2)\chi^2(p-1, \eta),\quad\eta=\frac{\sum_{12}V_{22}^{-1}\sum_{21}}{1 - \rho^2}\\ \eta \stackrel{d}{\sim} \tau\chi^2(n - 1)，\tau = \frac{\sum_{12}\sum_{21}}{1 - \rho^2}=\frac{\rho^2}{1 - \rho^2} $$ 由此可以导出$u$的密度函数。 又由于: $$ z = \frac{r^2_{x^{(1)},X^{(2)}}}{1 - r^2_{x^{(1)},X^{(2)}}}=\frac{V_{12}V_{22}^{-1}V_{21}}{v_{11}-V_{12}V_{22}^{-1}V_{21}}=\frac{u}{t_1} $$ 可以导出$z$的分布，进而推出$R = r^2$的密度函数: $$ \frac{(1 - \rho^2)^{\frac{n-1}2}(1 - R)^{\frac{n - p - 2}2}}{\Gamma(\frac{n-1}2)\Gamma(\frac{n - p}2)}\sum_{k = 0}^{\infty}\frac{\rho^{2k}R^{\frac{p-1}2 + k - 1}}{k!\Gamma(\frac{p-1}2 + k)}\Gamma^2(\frac{n-1}2 + k) $$ 密度函数揭示了 **相关性强弱** 对结果的影响，进而使得假设检验更加精确和可靠。例如，如果计算出 $r^2$很小，可以认为$x^{(1)}$ 和 $X^{(2)}$之间几乎没有线性相关性，从而支持它们独立的假设；而如果 $r^2$ 较大，则可能需要进一步检查相关性的显著性。

# 5.2 典型相关分析

## 典型相关系数定义(向量-向量之间)

设$X=(X_1,\dots,X_p)',Y=(Y_1,\dots,Y_q)'$分别为p维和q维随机向量：$\begin{pmatrix}X\\Y\end{pmatrix}\sim N_{p+q}(\mu,\Sigma)$，其协方差矩阵为： $$ \text{Cov}\begin{pmatrix}X\\Y\end{pmatrix} =\Sigma=\begin{pmatrix}\Sigma_{11}&\Sigma_{12}\\\Sigma_{21}&\Sigma_{22}\end{pmatrix} $$ 其中：$\Sigma_{11}:p\times p,\Sigma_{22}:q\times q,\Sigma_{12}=\Sigma_{21}':p\times q$，$\Sigma_{11},\Sigma_{22}$正定。

设a和b分别为p维和q维任意非零的常数向量： $$ \rho(a'X,b'Y)=\frac{a'\Sigma_{12}b}{\sqrt{(a'\Sigma_{11}a)(b'\Sigma_{22}b)}} $$ **由于相关系数$\rho(a'X,b'Y)$不受a和b常数倍的影响，**为简单起见，对$a'X,b'Y$进行标准化，令： $$ Var(a'X)=a'\Sigma_{11}a=1,\quad Var(b'Y)=b'\Sigma_{22}b=1 $$

**(书p485)定理13.1.1**：$a'X$和$b'Y$的最大相关系数为： $$ \max_{a,b}\rho(a'X,b'Y)=\sqrt{\lambda_1} $$ 在标准化的方差约束条件下，最大值在$a\frac{1}{\sqrt{\lambda_1}\Sigma_{11}^{-1}\Sigma_{12}b},b=\Sigma_{22}^{-1}\beta$时达到，其中$\lambda_1,\beta$分别为矩阵$D=\Sigma_{22}^{-\frac 1 2}\Sigma_{21}\Sigma_{11}^{-1}\Sigma_{12}\Sigma_{22}^{-\frac 1 2}$的最大特征值和最大特征值对应的特征向量。

**定理13.1.1**表明，要求a和b，可以先求a再求b，也可以先求b再求a。$a=\Sigma_{11}^{-\frac 1 2}\theta,b=\frac{1}{\sqrt{\lambda_1}\Sigma_{22}^{-1}\Sigma_{21}a}$。

因此把$\sqrt{\lambda_1}$称为 $X$ 和 $Y$ 的**第一典型相关系数**：

+   当$\sqrt{\lambda_1}$越接近0，说明 $X$ 和 $Y$ 的相关程度越弱；
+   当$\sqrt{\lambda_1}$越接近1，说明 $X$ 和 $Y$ 的相关程度越强。

**但上面的得到的$a'X,b'Y$的相关系数$\sqrt{\lambda_1}$往往并不能完全反映 $X$ 和 $Y$ 的相关程度，需要考虑 $X$ 和 $Y$ 的更多组线性组合的相关系数。**

## 5.2.1 总体典型相关分析

设$X=(X_1,\dots,X_p)',Y=(Y_1,\dots,Y_q)'$分别为p维和q维随机向量：$\begin{pmatrix}X\\Y\end{pmatrix}\sim N_{p+q}(\mu,\Sigma)$，其协方差矩阵为： $$ \text{Cov}\begin{pmatrix}X\\Y\end{pmatrix} =\Sigma=\begin{pmatrix}\Sigma_{11}&\Sigma_{12}\\\Sigma_{21}&\Sigma_{22}\end{pmatrix} $$ 其中 : $\Sigma_{11}=Cov(X)>0,\Sigma_{22}=Cov(Y)>0,\Sigma_{12}=\Sigma_{21}'=Cov(X,Y)$.

类似随机变量间相关系数，定义： $$ R=\Sigma_{11}^{-\frac 1 2}\Sigma_{12}\Sigma_{22}^{-\frac 1 2} $$ 根据定理13.1.1，$a'X,b'Y$的最大相关关系$\sqrt{\lambda_1}$就是R的最大奇异值。$\beta,\theta$分别为$R'R,RR'$最大特征值对应的标准化后的特征向量。**当R存在多个非零奇异值时，X 和 Y 存在多组典型相关变量。** 具体定义如下：

> **(书p486)定义13.2(总体的典型相关)**：记R的奇异值分解为： $$ R=P\Lambda Q' $$ 此处, $P=(\theta_1,\dots,\theta_k),Q=(\beta_1,\dots,\beta_k)$分别为$p\times k,q\times k$的**列正交矩阵**。$\Lambda=diag(\sqrt{\lambda_1},\dots,\sqrt{\lambda_k}),\sqrt{\lambda_1}\ge\dots\ge\sqrt{\lambda_k}\ge0$为R的非奇异值。$\theta_i,\beta_i$ 分别为$RR',R'R$对应于共同特征值$\lambda_i$的标准化的特征向量。
> 
> **X 和 Y的典型相关向量：** $$ a_i=\Sigma_{11}^{-\frac 1 2}\theta_i,\quad b_i=\Sigma_{22}^{-\frac 1 2}\beta_i $$ **X 和 Y的第i对典型相关向量**：$(a'_iX,b'_iY)$
> 
> **X 和 Y的第i个典型相关系数**：$\rho_i=\sqrt{\lambda_i}$

## A.典型相关系数的性质

 
| 性质 | 説明 |
| --- | --- |
| 性质13.2.1 | 典型相关变量$a'_iX,b'_iY$的方差都被标准化为1，且不同组的典型相关变量是不相关的。 |
| 性质13.2.2 | 典型相关变量$a_i,b_i$具有如下关系：$\begin{align}a_i&=\frac{1}{\rho_i}\Sigma_{11}^{-1}\Sigma_{12}b_i\\b_i&=\frac 1{\rho_i}\Sigma_{22}^{-1}\Sigma_{21}a_i\\i&=1,\dots,k\end{align}$ |
| 性质13.2.3 | 典型相关变量$a_i,b_i$分别为$\Sigma_{11}^{-1}\Sigma_{12}\Sigma_{22}^{-1}\Sigma_{21},\Sigma_{22}^{-1}\Sigma_{21}\Sigma_{11}^{-1}\Sigma_{12}$的特征向量。 |

> **对13.2.2的说明：**因为$RR'$与$\Sigma_{11}^{-1}\Sigma_{12}\Sigma_{22}^{-1}\Sigma_{21}$具有相同的非零特征值，都是$\vert\lambda\Sigma_{11}-\Sigma_{12}\Sigma_{22}^{-1}\Sigma_{21}\vert=0$的解。**所以 X和Y 的典型相关系数也可以通过后者得到。**
> 
> **证明13.2.3：**根据上面13.2的定义可得： $$ \because\Sigma_{11}^{-1}\Sigma_{12}\Sigma_{22}^{-1}\Sigma_{21}\Sigma_{11}^{-1}\theta_i=\lambda_i\Sigma_{11}^{-1}\theta_i\\ \therefore\Sigma_{11}^{-1}\Sigma_{12}\Sigma_{22}^{-1}\Sigma_{21}a_i=\lambda_ia_i\\ 同理,\Sigma_{22}^{-1}\Sigma_{21}\Sigma_{11}^{-1}\Sigma_{12}b_i=\lambda_ib_i\\ $$

 
| 定理和推论 | 说明 |
| --- | --- |
| 定理13.2.1 | 对固定的$r(1\le r\le k)$,记$f_r=\max_{a,b}a'\Sigma_{12}b$, 其中$a,b$满足约束条件：$a'\Sigma_{11}a=1,b'\Sigma_{22}b=1,a_i'\Sigma_{11}a=0,i=1,\dots,r-1$,则$f_r=\sqrt{\lambda_r}$, 且最大值在$a=a_r,b=b_r$处达到。 |
| 定理13.2.2 | 记 $X^ = U'X + u$, $Y^ = V'Y + v$，其中 $U$ 和 $V$ 分别为 $p \times p$ 和 $q \times q$ 的任意可逆的常数矩阵，$u$ 和 $v$ 分别为 $p \times 1$ 和 $q \times 1$ 的常数向量。 则 $X^$ 和 $Y^$ 的典型相关系数就等于 $X$ 和 $Y$ 的典型相关系数； $X^$ 和 $Y^$ 的典型相关向量分别为： $a_i^ = U^{-1}a_i, \quad b_i^ = V^{-1}b_i$， 其中 $a_i$ 和 $b_i$ 分别为 $X$ 和 $Y$ 的典型相关向量。 |
| 推论13.2.1 | $X^$ 和 $Y^$ 与 $X$ 和 $Y$ 具有相同的典型相关系数和相应的典型相关变量组，且两者典型相关向量间满足：$a_i^ = \text{diag}(\Sigma_{11})^{1/2} a_i, \quad b_i^ = \text{diag}(\Sigma_{22})^{1/2} b_i \\ a_i = (\text{diag}(\Sigma_{11}))^{-1/2} a_i^, \quad b_i = (\text{diag}(\Sigma_{22}))^{-1/2} b_i^$. |

> ところで、既然不会考这个定理的证明，那么我们就暂时(永遠に)不写了hh。
> 
> 对 $X$和 $Y$进行标准化，得：$X^ = (\text{diag}(\Sigma_{11}))^{-1/2} X, \quad Y^ = (\text{diag}(\Sigma_{22}))^{-1/2} Y$, 其中，$\text{diag}(A)$表示由方阵 $A$的对角元素构成的对角矩阵。 由定理 13.2.2，可得推论13.2.1, 值得注意的是，当 $\rho_1, \dots, \rho_p$中存在两个相等时（即 $\rho_r = \rho_{r+1}$​），典型相关系数向量的选择并不唯一。

## 典型相关分析的所有k步

 
| 步骤 | 详细说明(与性质部分同) |
| --- | --- |
| 1 | 设$Cov(X,Y)=\Sigma_{12}$的秩为$k$，则向量$X$与$Y$一共有$k$组（对）典型相关变量和$k$个典型相关系数. |
| 2 | 设$\theta_{1},\cdots,\theta_{k}$和$\beta_{1},\cdots,\beta_{k}$分别是$RR'$和$R'R$的$k$个非零特征根$\lambda_{1}^{2}\geq\cdots\geq\lambda_{k}^{2}>0$所对应的正则正交特征向量，其中$\beta_{i}=R'\theta_{i}/\lambda_{i}$，$1\leq i\leq k$. |
| \- | 令$\mathbf{a}_{i}=\Sigma_{11}^{-\frac 1 2}\theta_{i}$，$\mathbf{b}_{i}=\Sigma_{22}^{-\frac 1 2}\beta_{i}$，$1\leq i\leq k$， 则称$(\mathbf{a}_{i}'X,\mathbf{b}_{i}'Y)$为第$i$组（对）典型相关变量，$\mathbf{a}_{i}'X$与$\mathbf{b}_{i}'Y$的相关系数为$\lambda_{i}>0$，称$\lambda_{i}$为第$i$个典型相关系数，$1\leq i\leq k$. $\mathbf{a}_{i}$和$\mathbf{b}_{i}$分别是$\Sigma_{11}^{-1}\Sigma_{12}\Sigma_{22}^{-1}\Sigma_{21}$和$\Sigma_{22}^{-1}\Sigma_{21}\Sigma_{11}^{-1}\Sigma_{12}$的特征根$\lambda_{i}^{2}$所对应的特征向量，$1\leq i\leq k$. |
| 3 | 第$i$组（对）典型相关变量$(\mathbf{a}_{i}'X,\mathbf{b}_{i}'Y)$是正则的，即 $Var(\mathbf{a}_{i}'X)=\mathbf{a}_{i}'\Sigma_{11}\mathbf{a}_{i} = 1$，$Var(\mathbf{b}_{i}'Y)=\mathbf{b}_{i}'\Sigma_{22}\mathbf{b}_{i}=1$，$1\leq i\leq k$. |
| 4 | 典型相关变量$\{(\mathbf{a}_{i}'X,\mathbf{b}_{i}'Y)\}_{i = 1}^{k}$之间是正交的， 即对$1\leq i<j\leq k$，有: $\begin{align}Cov(\mathbf{a}_{i}'X,\mathbf{a}_{j}'X)=\mathbf{a}_{i}'\Sigma_{11}\mathbf{a}_{j}=0\\Cov(\mathbf{a}_{i}'X,\mathbf{b}_{j}'Y)=\mathbf{a}_{i}'\Sigma_{12}\mathbf{b}_{j}=0\\Cov(\mathbf{b}_{i}'Y,\mathbf{b}_{j}'Y)=\mathbf{b}_{i}'\Sigma_{22}\mathbf{b}_{j}=0\\Cov(\mathbf{b}_{i}'Y,\mathbf{a}_{j}'X)=\mathbf{b}_{i}'\Sigma_{21}\mathbf{a}_{j}=0\end{align}$ |
| 5 | 第1组（对）典型相关变量$(\mathbf{a}_{1}'X,\mathbf{b}_{1}'Y)$是下述条件极值问题的解： 在$\mathbf{a}'\Sigma_{11}\mathbf{a}=1$，$\mathbf{b}'\Sigma_{22}\mathbf{b}=1$的条件下使得$\mathbf{a}'\Sigma_{12}\mathbf{b}$达到最大值，其最大值为$\lambda_{1}>0$. |
| 6 | 对$2\leq i\leq k$，第$i$组（对）典型相关变量$(\mathbf{a}_{i}'X,\mathbf{b}_{i}'Y)$是下述条件极值问题的解： 在$\mathbf{a}'\Sigma_{11}\mathbf{a}=1$，$\mathbf{b}'\Sigma_{22}\mathbf{b}=1$且对任意$1\leq j\leq(i - 1)$都有 $\mathbf{a}'\Sigma_{11}\mathbf{a}_{j}=\mathbf{a}'\Sigma_{12}\mathbf{b}_{j}=\mathbf{b}'\Sigma_{21}\mathbf{a}_{j}=\mathbf{b}'\Sigma_{22}\mathbf{b}_{j}=0$的条件下使得$\mathbf{a}'\Sigma_{12}\mathbf{b}$达到最大值，其最大值为$\lambda_i>0$ |

## 典型相关分析的作用

一、**特征向量与特征根**

设$\Sigma_{12}$的秩为$k$，$k\leq p\leq q$。 则$\Sigma_{11}^{-\frac 1 2}\Sigma_{12}\Sigma_{22}^{-1}\Sigma_{21}\Sigma_{11}^{-\frac 1 2}$的特征根 $\lambda_{1}^{2}\geq\cdots\geq\lambda_{k}^{2}>0 = \lambda_{k + 1}^{2}=\cdots=\lambda_{p}^{2}$所对应的 正则正交特征向量为$\alpha_{1},\cdots,\alpha_{p}$。

相应地，$\Sigma_{22}^{-\frac 1 2}\Sigma_{21}\Sigma_{11}^{-1}\Sigma_{12}\Sigma_{22}^{-\frac 1 2}$的特征根 $\lambda_{1}^{2}\geq\cdots\geq\lambda_{k}^{2}>0 = \lambda_{k + 1}^{2}=\cdots=\lambda_{q}^{2}$所对应的 正则正交特征向量为$\beta_{1},\cdots,\beta_{q}$。

二、**相关性与降维**

令: $$ U = A'\Sigma_{11}^{-\frac 1 2}X,V = B'\Sigma_{22}^{-\frac 1 2}Y\\ W_{1}=C_{1}'\Sigma_{11}^{-\frac 1 2}X,W_{2}=C_{2}'\Sigma_{22}^{-\frac 1 2}Y\\W=(W_{1}',W_{2}')' $$ 其中， $$ A = (\alpha_{1},\cdots,\alpha_{k}),B = (\beta_{1},\cdots,\beta_{k})\\ C_{1}=(\alpha_{k + 1},\cdots,\alpha_{p}),C_{2}=(\beta_{k + 1},\cdots,\beta_{q}) $$ 则有 : $$ Cov\left(\begin{array}{c}U\\V\\W\end{array}\right)=\left(\begin{array}{ccc}I_{k}&\Lambda&0\\\Lambda&I_{k}&0\\0&0&I_{p + q-2k}\end{array}\right) $$ 其中$\Lambda = diag(\lambda_{1},\cdots,\lambda_{k})$。

不难看出，$U$与$V$的相关性等价于$X$与$Y$的相关性。 由于$k\leq min(p,q)$，因此用$U$与$V$分别代表$X$与$Y$ 可以起到数据降维的作用。

事实上，若记$U=(U_{1},\cdots,U_{k})'$，$V=(V_{1},\cdots,V_{k})'$， 则$(U_{i},V_{i})$就是$X$与$Y$的第$i$组(对)典型相关变量， 它们的相关系数就是第$i$个典型相关系数$\lambda_{i}>0$，$1\leq i\leq k$。

## 相关知识：矩阵二次型极值的性质

在此文中，我们给出了两种解释典型相关分析的方法：

 
| SVD-奇异值分解 | 矩阵二次型极值 |
| --- | --- |
| 直接通过对协方差矩阵 R 进行 SVD，获得了最大相关系数（即奇异值）及其对应的特征向量，进而给出了经典的典型相关分析的解法。 | 从优化问题出发的一个理论框架，最终是要解决如何最大化一个关于矩阵的表达式。 |

> 如何通过矩阵的特征值和特征向量来求解最大值。
> 
> **性质1** : 设 $C$ 是 $p \times q$ 的非零矩阵，$A$ 和 $B$ 分别是 $p$ 阶和 $q$ 阶的正定矩阵，则: $$ \sup_{\substack{x \in \mathbb{R}^p \\ y \in \mathbb{R}^q}} \frac{(x'Cy)^2}{(x'Ax)(y'By)} = \lambda_1^2 > 0, $$ 其中，$\lambda_1^2$ 是 $A^{-1}CB^{-1}C'$，$A^{-\frac 1 2}CB^{-1}C'A^{-\frac 1 2}$，$B^{-1}C'A^{-1}C$ 或 $B^{-\frac 1 2}C'A^{-1}CB^{-\frac 1 2}$ 的最大特征根，且 $\lambda_1 > 0$。
> 
> 上式在 $x = A^{-\frac 1 2}\alpha_1$，$y = B^{-\frac 1 2}\beta_1$ 时达极大，且 $x'Cy = \lambda_1$，其中，$\alpha_1$ 和 $\beta_1 = B^{-\frac 1 2}C'A^{-\frac 1 2}\alpha_1/\lambda_1$ 分别是 $\lambda_1^2$ 作为 $A^{-\frac 1 2}CB^{-1}C'A^{-\frac 1 2}$ 和 $B^{-\frac 1 2}C'A^{-1}CB^{-\frac 1 2}$ 的最大特征根所对应的正则特征向量。

由性质1，典型相关分析第1步，约束极值问题 $$ \sup_{\substack{\alpha \in \mathbb{R}^p \\ \beta \in \mathbb{R}^q}}(\rho_{\alpha'X,\beta'Y})^2 = \sup_{\substack{\alpha \in \mathbb{R}^p ,\ \alpha'\Sigma_{11}\alpha = 1 \\ \beta \in \mathbb{R}^q ,\ \beta'\Sigma_{22}\beta = 1}}(a'\Sigma_{12}b)^2 $$ 的解为：$(\alpha'\Sigma_{12}\beta)^2$ 的最大值为 $\lambda_1^2$.

$\lambda_1^2$ 是 $\Sigma_{11}^{-1}\Sigma_{12}\Sigma_{22}^{-1}\Sigma_{21}$，$\Sigma_{11}^{-\frac 1 2}\Sigma_{12}\Sigma_{22}^{-1}\Sigma_{21}\Sigma_{11}^{-\frac 1 2}$，$\Sigma_{22}^{-1}\Sigma_{21}\Sigma_{11}^{-1}\Sigma_{12}$ 或 $\Sigma_{22}^{-\frac 1 2}\Sigma_{21}\Sigma_{11}^{-1}\Sigma_{12}\Sigma_{22}^{-\frac 1 2}$ 的最大特征根，在 $\alpha_1 = \Sigma_{11}^{-\frac 1 2}\alpha_1$，$\beta_1 = \Sigma_{22}^{-\frac 1 2}\beta_1$ 时取最大值，其中，$\alpha_1$ 和 $\beta_1 = \Sigma_{22}^{-\frac 1 2}\Sigma_{21}\Sigma_{11}^{-\frac 1 2}\alpha_1/\lambda_1$ 分别是 $\Sigma_{11}^{-\frac 1 2}\Sigma_{12}\Sigma_{22}^{-\frac 1 2}$ 和 $\Sigma_{22}^{-\frac 1 2}\Sigma_{21}\Sigma_{11}^{-\frac 1 2}$ 的最大特征根 $\lambda_1^2$ 所对应的正则特征向量。

因此，$\alpha_1'X$ 与 $\beta_1'Y$ 的相关系数 $\rho_{\alpha_1'X,\beta_1'Y} = \lambda_1 > 0$。 此时，$\alpha_1$ 和 $\beta_1$ 分别是 $\Sigma_{11}^{-1}\Sigma_{12}\Sigma_{22}^{-1}\Sigma_{21}$ 和 $\Sigma_{22}^{-1}\Sigma_{21}\Sigma_{11}^{-1}\Sigma_{12}$ 的最大特征根 $\lambda_1^2$ 所对应的特征向量。

当 $\Sigma_{12} = 0$ 时，$X$ 与 $Y$ 相互独立。

因此，$X$ 与 $Y$ 的任意线性组合都相互独立，相关系数的最大值也为零。

> 性质2 : 设 $C$ 是秩为 $k$ 的 $p \times q$ 的非零矩阵，$p \leq q$。 则 $p$ 阶矩阵 $CC'$ 的 $p$ 个非负特征根中有 $k$ 个正的特征根 $\lambda_1^2 \geq \cdots \geq \lambda_k^2 > 0$，其余 $p - k$ 个特征根为 $\lambda_{k + 1}^2 = \cdots = \lambda_p^2 = 0$。 同理，$q$ 阶矩阵 $C'C$ 的 $q$ 个非负特征根中有 $\lambda_1^2 \geq \cdots \geq \lambda_k^2 > 0$，其余 $q - k$ 个特征根为 $\lambda_{k + 1}^2 = \cdots = \lambda_q^2 = 0$。
> 
> 记 $\alpha_1,\cdots,\alpha_p$ 为 $CC'$ 的特征根所对应的正则正交特征向量，$\beta_1,\cdots,\beta_q$ 为 $C'C$ 的特征根所对应的正则正交特征向量。
> 
> 相关结论:
> 
> 1.  设 $x \in \mathbb{R}^p$，$y \in \mathbb{R}^q$，则在 $x'x = 1$，$y'y = 1$的正则化约束条件下， $(x'Cy)^2 = _1^2 $当 $x = \alpha_1$，$y = \beta_1$时取最大值，并且 $x'Cy = \lambda_1$；
> 2.  对给定的 $1 \leq m \leq (p - 1)$，$x \in \mathbb{R}^p$，$y \in \mathbb{R}^q$ 满足如下约束条件：
>     +   **正则化约束**：$x'x = 1$，$y'y = 1$；  
>         
>     +   **正交化约束**：对所有 $1 \leq i \leq m$，都有：$\alpha_i'x = 0$，$\beta_i'y = 0$，$\alpha_i'Cy = 0$，$\beta_i'C'x = 0$。
>     +   则在**正则正交约束**下有 ：
>         +   当 $1 \leq m \leq (k - 1)$ 时，$\sup(x'Cy)^2 = \lambda_{m + 1}^2$，当 $x = \alpha_{m + 1}$，$y = \beta_{m + 1}$ 时取最大值，且 $x'Cy = \lambda_{m + 1} > 0$；
>         +   当 $k \leq m \leq (p - 1)$ 时，$x'Cy = 0$。

## 5.2.2 样本典型相关分析

> 在大多数实际应用中$\Sigma$都是未知的，因此，典型相关系数和典型相关变量都是未知的，需要由样本来估计。

设正态总体$(X',Y')'\sim N_{p+q}(\mu,\Sigma)$有样本$\{(x_i,y_i)\}_{i = 1}^{n}$，i.i.d.$n> p + q$，$p\leq q$。 则$\Sigma_{11}$，$\Sigma_{22}$和$\Sigma_{12}$极大似然估计为: $$ \hat{\Sigma}_{11}=\frac 1 n\sum_{i = 1}^{n}(x_i-\bar{x}_n)(x_i-\bar{x}_n)'\\ \hat{\Sigma}_{22}=\frac 1 n\sum_{i = 1}^{n}(y_i-\bar{y}_n)(y_i-\bar{y}_n)'\\ \hat{\Sigma}_{12}=\frac 1 n\sum_{i = 1}^{n}(x_i-\bar{x}_n)(y_i-\bar{y}_n)' $$

## 性质

由于特征根是矩阵中各元素的非退化连续函数，因此由正态随机变量组成的矩阵$RR'$的特征根是连续型随机变量。 那么，该矩阵的特征根以概率1满足： $$ 1>\hat{\lambda}_1^2>\cdots>\hat{\lambda}_p^2>0 $$

## 样本典型相关变量与系数

记$\alpha_1,\cdots,\alpha_p$和$\beta_1,\cdots,\beta_p$分别是$RR'$和$R'R$的特征根$\hat{\lambda}_1^2,\cdots,\hat{\lambda}_p^2$所对应的正则正交特征向量。

令$\hat{a}_i=\hat{\Sigma}_{11}^{-\frac 1 2}\alpha_i$，$\hat{b}_i=\hat{\Sigma}_{22}^{-\frac 1 2}\beta_i$，$1\leq i\leq p$。

+   称$(\hat{a}_i'X,\hat{b}_i'Y)$为第$i$组(对)样本典型相关变量
+   称$\hat{\lambda}_i$为第$i$个样本典型相关系数，$1\leq i\leq p$。

不难知道，$\hat{a}_i$和$\hat{b}_i$分别是$\hat{\Sigma}_{11}^{-1}\hat{\Sigma}_{12}\hat{\Sigma}_{22}^{-1}\hat{\Sigma}_{21}$和$\hat{\Sigma}_{22}^{-1}\hat{\Sigma}_{21}\hat{\Sigma}_{11}^{-1}\hat{\Sigma}_{12}$的特征根$\hat{\lambda}_i^2$所对应的特征向量，$1\leq i\leq p$。

$(\hat{a}_i'X,\hat{b}_i'Y)$和$\hat{\lambda}_i$分别是总体典型相关变量$(a_i'X,b_i'Y)$和总体典型相关系数$\lambda_i$的极大似然估计，$1\leq i\leq p$。

> **Q**: 由于$1>\hat{\lambda}_1^2>\cdots>\hat{\lambda}_p^2>0$，如何判断有意义的典型相关变量？
> 
> A: 即给出一个估计$k\leq p$，认为: $$ \lambda_1^2>\cdots>\lambda_k^2>0\\ \lambda_{k + 1}^2=\cdots=\lambda_p^2 = 0 $$

## 5.2.3 典型相关变量个数的检验

设正态总体$(X,Y)$有样本$\{(x_i,y_i)\}_{i = 1}^{n}$，$n > p + q$，$p \leq q$。 记$V$为样本离差阵: $$ V=\left(\begin{array}{ll} V_{11} & V_{12} \\ V_{21} & V_{22} \end{array}\right) \\\begin{cases}V_{11}=\sum_{i = 1}^{n}(x_i-\bar{x}_n)(x_i-\bar{x}_n)'\\ V_{22}=\sum_{i = 1}^{n}(y_i-\bar{y}_n)(y_i-\bar{y}_n)', \\V_{12}=\sum_{i = 1}^{n}(x_i-\bar{x}_n)(y_i-\bar{y}_n)' \end{cases} $$

## 典型相关变量个数等于0 vs. 大于0的检验问题

典型相关变量个数$k = 0 \Leftrightarrow \Sigma_{12}=0$，即$X$与$Y$独立（不相关）。

因此上述检验问题等价于：正态假设下，$X$与$Y$的独立性检验问题。

似然比统计量为 ： $$ \lambda=\left(\frac{|V|}{|V_{11}||V_{22}|}\right)^{n/2}=\left(\frac{|V_{11}-V_{12}V_{22}^{-1}V_{21}|}{|V_{11}|}\right)^{n/2}\\ =\vert I_p-V_{11}^{-1}V_{12}V_{22}^{-1}V_{21}\vert^{n/ 2}=\left[\prod_{i = 1}^{p}(1-\hat{\lambda}_i^2)\right]^{n/2}\\ T_0=\prod_{i = 1}^{p}(1 - \hat{\lambda}_i^2)=\frac{|V_{11}-V_{12}V_{22}^{-1}V_{21}|}{|(V_{11}-V_{12}V_{22}^{-1}V_{21})+V_{12}V_{22}^{-1}V_{21}|} $$ 在零假设$\Sigma_{12}=0$下，有$T_0\stackrel{d}{\sim}\Lambda_{p,n - 1 - q,q}$。因此可以用零分布$\Lambda_{p,n - 1 - q,q}$构造检验方案，也可由似然比统计量的渐近分布构造检验方案。 $$ - 2\log(\lambda)=-n\sum_{i = 1}^{p}\log(1-\hat{\lambda}_i^2)\stackrel{d}{\sim}\chi^2(pq) $$

## 典型相关变量的个数等于$k$ vs. 大于$k$的检验问题

等价于检验问题： $$ H_0:rank(\Sigma_{12})=k\quad vs.\quad H_1:rank(\Sigma_{12})>k $$ 也等价于检验问题： $$ H_0:\lambda_k^2>0,\lambda_{k + 1}^2 = 0\quad vs.\quad H_1:\lambda_{k + 1}^2>0 $$ 也等价于检验问题： $$ H_0:存在p\times(p - k)的列满秩矩阵C，使得\Sigma_{22}^{-1}\Sigma_{21}C = 0 $$ 似然比统计量为 : $$ \begin{align}\lambda&=\sup_{C}\left[\frac{|C'(V_{11}-V_{12}V_{22}^{-1}V_{21})C|}{|C'V_{11}C|}\right]^{n/2}\\ &=\sup_{C'C = I_{p - k}}\vert C'(I_p-RR')C\vert^{n/2}\\ &=\sup_{D'D = I_{p - k}}\frac{|D'diag(1-\hat{\lambda}_1^2,\cdots,1-\hat{\lambda}_p^2)D|}{|D'D|}\\ &=\left[\prod_{i = k + 1}^{p}(1-\hat{\lambda}_i^2)\right]^{n/2} \end{align} $$ 其中$C$是任意$p\times(p - k)$的列满秩矩阵。 由于$rank(\Sigma_{12})=k$，因此有 $_{12}=( $$\begin{array}{c} C_1 \\ C_2 \end{array}$$

), $其中$C_1$是$kq$的满秩矩阵，而$C_2 = QC_1$，$Q$是$(p - k)k$的矩阵。

因此，有: $$ \begin{align}& \dim(\Theta_0)=p + q + p(p + 1)/2 + q(q + 1)/2 + kq+(p - k)k\\ &\dim(\Theta)-\dim(\Theta_0)=(p - k)(q - k) \end{align} $$ 由Wilks定理知: $$ -2\log(\lambda)=-n\sum_{i = k + 1}^{p}\log(1 - \hat{\lambda}_i^2)\stackrel{d}{\rightarrow}\chi^2((p - k)(q - k)) $$ 进而构造检验方案。也可以采用修正的统计量: $$ -\left(n - 1 - k-\frac{p + q + 1}{2}+\sum_{i = 1}^{k}\hat{\lambda}_i^2\right)\sum_{i = k + 1}^{p}\log(1 - \hat{\lambda}_i^2) $$

# 5.3 广义相关系数

设随机变量$X_{p\times1}$和$Y_{q\times1}$，记: $$ \Sigma = Cov\left(\begin{matrix}X\\Y\end{matrix}\right)=\left(\begin{matrix}\Sigma_{11}&\Sigma_{12}\\\Sigma_{21}&\Sigma_{22}\end{matrix}\right)>0 $$ 称$M_{21}=V_{22}^{-1}V_{21}V_{11}^{-1}V_{12}$为$X$和$Y$的线性关联阵。

记$k = rank(M_{21})$，称$k$为$X$和$Y$的相关秩。

记线性关联阵$M_{21}$的非零特征根为$\lambda_{1}^{2}\geq\cdots\geq\lambda_{k}^{2}>0$。 四、广义相关系数 则下面定义的每个量都称为$X$与$Y$的广义相关系数： $$ \begin{cases} \ \rho_{12}^{(1)}=\left(\prod_{i = 1}^{k}\lambda_{i}\right)^{1/k}\\ \ \rho_{12}^{(2)}=\frac 1 k\sum_{i = 1}^{k}\lambda_{i}^{2}\\ \ \rho_{12}^{(3)}=\lambda_{1}^{2}\\ \ \rho_{12}^{(4)}=\lambda_{k}^{2}\\ \ \rho_{12}^{(5)}=\left(\frac 1 k\sum_{i = 1}^{k}\lambda_{i}^{-2}\right)^{-1} \end{cases} $$

# 5.4 实例分析

![image-20241214114658874](https://cdn.jsdelivr.net/gh/SchwertLin/Pic/img/image-20241214114658874.png)

变量间的相关系数矩阵 |

|  | X1 | X2 | y1 | y2 | y3 |
| --- | --- | --- | --- | --- | --- |
| **X1** | 1.00 | 0.80 | **0.26** | **0.67** | **0.34** |
| **X2** | 0.80 | 1.00 | **0.33** | **0.59** | **0.34** |
| **y1** | **0.26** | **0.33** | 1.00 | 0.37 | 0.21 |
| **y2** | **0.67** | **0.59** | 0.37 | 1.00 | 0.35 |
| **y3** | **0.34** | **0.34** | 0.21 | 0.35 | 1.00 |

典型相关分析:

|  | 典型相关系数 | 典型相关系数的平方 |
| --- | --- | --- |
| 1 | 0.687948 | 0.473272 |
| 2 | 0.186865 | 0.034919 |

X组典型变量的系数$U=a'X$:

|  | U1 | U2 |
| --- | --- | --- |
| X1(就餐) | 0.7689 | \-1.4787 |
| X2(电影) | 0.2721 | 1.6443 |

Y组典型变量的系数$V=b'Y$ :

|  | V1 | V2 |
| --- | --- | --- |
| Y1(年龄) | 0.0491 | 1.0003 |
| Y2(收入) | 0.8975 | \-0.5837 |
| Y3(文化) | 0.1900 | 0.2956 |

$U_1 = 0.7689X_1 + 0.2721X_2; \quad V_1 = 0.0491Y_1 + 0.8975Y_2 + 0.1900Y_3;$ $U_2 = -1.4787X_1 + 1.6443X_2; \quad V_2 = 1.0003Y_1 - 0.5837Y_2 + 0.2956Y_3.$

## 典型变量的结构（相关系数）

|  | U1 | U2 |
| --- | --- | --- |
| X1 | 0.9866 | \-0.1632 |
| X2 | 0.8872 | 0.4461 |

|  | V1 | V2 |
| --- | --- | --- |
| Y1 | 0.4211 | 0.8464 |
| Y2 | 0.9822 | \-0.1101 |
| Y3 | 0.5145 | 0.3013 |

* * *

|  | V1 | V2 |
| --- | --- | --- |
| X1 | 0.6787 | \-0.0305 |
| X2 | 0.6104 | 0.0862 |

|  | U1 | U2 |
| --- | --- | --- |
| Y1 | 0.2897 | 0.1582 |
| Y2 | 0.6757 | \-0.0206 |
| Y3 | 0.3539 | 0.0563 |

+   两个反映消费的指标与第一对典型变量中$U_1$的相关系数分别为0.9866和0.8872，可以看出$U_1$可以作为消费特性的指标；
+   第一对典型变量中$V_1$与$Y_2$之间的相关系数为0.9822，可见典型变量$V_1$主要代表了家庭收入；
+   $U_1$和$V_1$的相关系数为0.6787，这就说明家庭的消费与一个家庭的收入之间其关系是很密切的。

## 检验典型相关变量的个数：$k = 0$ vs. $k>0$

此时，样本量$n = 70$，$p = 2$，$q = 3$。 检验统计量、p值为： $$ \begin{align} - 2\log(\lambda)&=-n\sum_{i = k + 1}^{p}\log(1-\hat{\lambda}_{i}^{2})\\ &=-70[\log(1 - 0.473272)+\log(1 - 0.034919)]\\ &=47.363 \\\\ P\{\chi^{2}(pq)> - 2\log(\lambda)\}&=P\{\chi^{2}(6)>47.363\} \\&= 1.584\times10^{-8}<0.05 \end{align} $$ 结论：拒绝$k = 0$的假设，即不能认为两组变量不相关。

## 检验典型相关变量的个数：$k = 1$ vs. $k>1$

检验统计量、p值为： $$ \begin{align} - 2\log(\lambda)&=-n\sum_{i = k + 1}^{p}\log(1-\hat{\lambda}_{i}^{2})\\ &=-70\log(1 - 0.034919)\\ &=2.488\\\\ P\{\chi^{2}((p - k)(q - k))> - 2\log(\lambda)\}&=P\{\chi^{2}(2)>2.488\}\\&=0.288>0.05 \end{align} $$ 结论：没有足够证据拒绝零假设。可以认为典型相关变量的个数为1。
