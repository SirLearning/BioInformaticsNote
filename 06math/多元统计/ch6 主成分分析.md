
目的：根据二八定律（雾），大量有效的信息都在很少的指标中。所以PCA在尽量减少损失信息的前提下，将多个指标**降维，综合成几个综合指标**。

> 总的来说，PCA就是数据降维。但需要注意的是，得到的降维后的变量无实际意义（基本上就是原各个变量都混合一点的“大杂烩”）。

思路：选取变量的线性组合，使其$\max \Sigma\sim \sum_i \Sigma_i$（使得这个线性组合的方差尽可能的大，接近各个分类的方差之和，进而代表总体的散布程度）。

[TOC]

# 6.0 引入

## 6.0.1 例子

![image-20241215114128375](https://cdn.jsdelivr.net/gh/SchwertLin/Pic/img/image-20241215114128375.png)

![image-20241215114228030](https://cdn.jsdelivr.net/gh/SchwertLin/Pic/img/image-20241215114228030.png)

方差$Var(X)$,选取的是对角线上值最大的前四个。

![image-20241215114254872](https://cdn.jsdelivr.net/gh/SchwertLin/Pic/img/image-20241215114254872.png)

计算相关系数：$\rho_{xy}=\frac{Cov(X,Y)}{\sqrt{Var(X)Var(Y)}}$, 我们选择的方差最大的四个变量中，身高与颈椎点高、腰围高之间相关性交，所以只取身高即可。

**最终选取的变量是：身高和胸围。**

> **但仍存在问题：身高和胸围仍然具有相关性，应该对其进行进一步地压缩，以选出更具有代表性的指标。**
> 
> **Q：**是否有更具代表性一个or少数指标
> 
> 代表性标准：方差最大。

## 6.0.2 主成分分析

记$X$是$p$维随机向量($p>1,Cov(X)=\Sigma$)，我们想基于$X$，找到变量$Y=a'X$($a\in \mathbb{R}^p, X$的线性组合)，令$Y$的方差尽可能地大，足以代表$X$的散布。

> $a\in\mathbb{R}^{m\times p},X\in\mathbb{R}^{p\times1},Y\in\mathbb{R}^{m\times1}$

因为$Cov(X)=\Sigma, Var(a'X)=a'Cov(X)a=a'\Sigma a$，这表明若不对$a$施加约束，则$a'X$的最大方差$\rightarrow \infty$。

所以对$a$施加正则化约束：$a'a=1$，使得优化问题为： $$ \sup_{a'a=1}Var(a'X)=\sup_{a'a=1} a'\Sigma a $$ 令$a_1=\arg\max_{a'a=1}a'\Sigma a$, $a_1'X$是$X$的第一主成分。

+   $a'_1X$是正则化系数下方差最大的$X$的线性组合。
+   $a'_1X$的散布程度最接近$X$, 是代表$X$的首选。

## A.总体协方差矩阵的特征根与特征向量

首先，我们先回顾一下URV分解、SVD分解、Moore-Penrose伪逆：

![image-20241215150754017](https://cdn.jsdelivr.net/gh/SchwertLin/Pic/img/image-20241215150754017.png)

![image-20241215150953899](https://cdn.jsdelivr.net/gh/SchwertLin/Pic/img/image-20241215150953899.png)

![image-20241215151256715](https://cdn.jsdelivr.net/gh/SchwertLin/Pic/img/image-20241215151256715.png)

![image-20241215151352366](https://cdn.jsdelivr.net/gh/SchwertLin/Pic/img/image-20241215151352366.png)

令$\Sigma$的特征根为$\lambda_{1}\geq\cdots\geq\lambda_{p}\geq0$，与这些特征根对应的正则正交特征向量为$\alpha_{1},\cdots,\alpha_{p}$。 易知: $$ \alpha_{1}=\alpha_{1}=(a_{11},\cdots,a_{1p})'\\ V_{ar}(a_{1}'X)=a_{1}'\Sigma a_{1}=\lambda_{1} $$ 则第一主成份：

+   方向：总体协差阵的最大特征根所对应的正则特征向量。
+   方差：总体协差阵的最大特征根。

## B.随机向量的离散程度

设$p$维随机向量$X=(x_{1},\cdots,x_{p})'$，其离散程度的信息可用向量各分量方差的总和表示： $$ V{ar}(x_{1})+\cdots+V{ar}(x_{p}) $$ **第一主成份的作用** ：

将$X$所含离散程度的信息最大化地用一个线性组合变量$a_{1}'X$所含离散程度的信息来代替。

第一主成份离散程度信息的贡献率： $$ \text{contriution}=\frac{V{ar}(a_{1}'X)}{\sum_{i = 1}^{p}V{ar}(x_{i})}\times100\% $$

> **Q：第一主成份代表性是否足够？或第一主成份贡献率是否足够？**
> 
> A: 寻找第二主成份$a_2'X$, 第二主成份应该与第一主成份正交，从而不含有第一主成份的信息。优化问题如下： $$ \sup_{a_{2}'a_{2}=1,\ a_{2}'a_{1}=0}V_{ar}(a_{2}'X)=\sup_{a_{2}'a_{2}=1,\ a_{2}'a_{1}=0}a_{2}'\Sigma a_{2}\\ s.t.\begin{cases} \text{正则化约束：}a_{2}'a_{2}=1\\ \text{正交化约束：}a_{2}'a_{1}=0 \end{cases} $$ 不难知道，$a_{2}=\alpha_{2}=(a_{21},\cdots,a_{2p})'$，$V_{ar}(a_{2}'X)=a_{2}'\Sigma a_{2}=\lambda_{2}$。
> 
> 即，第二主成份:
> 
> +   方向：总体协差阵的第二大特征根所对应的正则特征向量；
> +   方差：总体协差阵的第二大特征根。

**第一主成份与第二主成份的正交性**: $$ Cov(a_{1}'X,a_{2}'X)=a_{1}'\Sigma a_{2}=\lambda_{2}a_{1}'a_{2}=0 $$ 因此，正态总体下，第一主成份与第二主成份相互独立。

第二主成份离散程度信息的贡献率: $$ \text{contribution}=\frac{V_{ar}(a_{2}'X)}{\sum_{i = 1}^{p}V_{ar}(x_{i})}\times100\% $$ 第一、第二主成份的累计贡献率: $$ \text{累计贡献率} = \frac{Var(a_1'X)+Var(a_2'X)}{\sum_{i = 1}^{p}Var(x_i)}×100\% \\ $$

## 6.0.3 回到例子

> 因为$\Sigma$是满秩的，那么$\Sigma$是一个RPN阵，这个时候对它进行SVD分解，得到的U=V都是$R(\Sigma)$值域空间的标准正交基。
> 
> ![image-20241215151614999](https://cdn.jsdelivr.net/gh/SchwertLin/Pic/img/image-20241215151614999.png)
> 
> 那么写一个简单的python程序，对$\Sigma$进行SVD分解结果如下。
> 
> **特征值&奇异值**
> 
> | 序号 | 特征值$\lambda_i$ | 奇异值$\sqrt{\lambda_i}$ |
> | --- | --- | --- |
> | 1 | 10115.7573 | 100.5771 |
> | 2 | 809.2391 | 28.4471 |
> | 3 | 33.0498 | 5.7489 |
> | 4 | 19.8222 | 4.4522 |
> | 5 | 10.2260 | 3.1978 |
> | 6 | 6.6843 | 2.5854 |
> | 7 | 1.9138 | 1.3834 |
> | 8 | 0.8612 | 0.9280 |
> 
> **左奇异向量 $U$**
> 
>         
> | 元素 | $U_{1}$ | $U_{2}$ | $U_{3}$ | $U_{4}$ | $U_{5}$ | $U_{6}$ | $U_{7}$ | $U_{8}$ |
> | --- | --- | --- | --- | --- | --- | --- | --- | --- |
> | $U_{1}$ | \-0.5920 | 0.1849 | \-0.1308 | 0.1612 | \-0.0062 | \-0.0136 | \-0.5614 | 0.5067 |
> | $U_{2}$ | \-0.5469 | 0.1362 | \-0.0860 | 0.0608 | \-0.0676 | \-0.0599 | \-0.0709 | \-0.8112 |
> | $U_{3}$ | \-0.4052 | 0.2028 | 0.2958 | 0.0702 | 0.5535 | 0.1070 | 0.5948 | 0.1752 |
> | $U_{4}$ | \-0.2062 | \-0.0083 | \-0.4074 | 0.2113 | \-0.6080 | \-0.1179 | 0.5662 | 0.2065 |
> | $U_{5}$ | \-0.0638 | \-0.2320 | \-0.1151 | 0.1003 | \-0.0726 | 0.9549 | \-0.0116 | \-0.0397 |
> | $U_{6}$ | \-0.2680 | \-0.9003 | 0.2347 | 0.1167 | 0.0327 | \-0.2170 | \-0.0055 | 0.0272 |
> | $U_{7}$ | \-0.1416 | \-0.1867 | \-0.6008 | \-0.7004 | 0.2935 | \-0.0286 | 0.0667 | 0.0472 |
> | $U_{8}$ | \-0.2183 | 0.0831 | 0.5411 | \-0.6376 | \-0.4763 | 0.1055 | 0.0282 | 0.0854 |
> 
> **右奇异向量 $V^T$**($V=U$)
> 
>         
> | 元素 | $V_{1}$ | $V_{2}$ | $V_{3}$ | $V_{4}$ | $V_{5}$ | $V_{6}$ | $V_{7}$ | $V_{8}$ |
> | --- | --- | --- | --- | --- | --- | --- | --- | --- |
> | $V_{1}$ | \-0.5920 | \-0.5469 | \-0.4052 | \-0.2062 | \-0.0638 | \-0.2680 | \-0.1416 | \-0.2183 |
> | $V_{2}$ | 0.1849 | 0.1362 | 0.2028 | \-0.0083 | \-0.2320 | \-0.9003 | \-0.1867 | 0.0831 |
> | $V_{3}$ | \-0.1308 | \-0.0860 | 0.2958 | \-0.4074 | \-0.1151 | 0.2347 | \-0.6008 | 0.5411 |
> | $V_{4}$ | 0.1612 | 0.0608 | 0.0702 | 0.2113 | 0.1003 | 0.1167 | \-0.7004 | \-0.6376 |
> | $V_{5}$ | \-0.0062 | \-0.0676 | 0.5535 | \-0.6080 | \-0.0726 | 0.0327 | 0.2935 | \-0.4763 |
> | $V_{6}$ | \-0.0136 | \-0.0599 | 0.1070 | \-0.1179 | 0.9549 | \-0.2170 | \-0.0286 | 0.1055 |
> | $V_{7}$ | \-0.5614 | \-0.0709 | 0.5948 | 0.5662 | \-0.0116 | \-0.0055 | 0.0667 | 0.0282 |
> | $V_{8}$ | 0.5067 | \-0.8112 | 0.1752 | 0.2065 | \-0.0397 | 0.0272 | 0.0472 | 0.0854 |

通过成人男子8个身体部位尺寸的协方差阵知： $$ \lambda_{1}=100.5771\\ a_{1}=(0.5920,0.5469,0.4052,0.2062,0.0638,0.2680,0.1416,0.2183)' $$ 第一主成份$\approx0.5\times(\text{身高}+\text{颈椎点高}+\text{腰围高})$。

![image-20241215115616003](https://cdn.jsdelivr.net/gh/SchwertLin/Pic/img/image-20241215115616003.png)

根据定理13.1.1 有： $$ \max_{a,b}\rho(a'X,b'Y)=\sqrt{\lambda_1}\\ Var(a'X)=\sqrt{\lambda_1}=100.57>Var(x_1)=37.115\\ $$ 第一主成份$a_{1}'X$的方差(散布程度)更大。 将其作为成年男子上衣的第一基本特征更具有代表性，以此对人群进行划分将更细致。

国外确定服装号型：第一主成份。

成年男子上衣第一主成份的贡献率$=\frac{100.5771}{147.32}=68.3\%$。

通过成人男子8个身体部位尺寸的协方差阵知： $$ \lambda_{2}=28.4471\\ a_{2}=(0.1849,0.1362,0.2028,-0.0083,-0.2320,-0.9003,-0.1867,0.0831)' $$ 第二主成份$\approx\text{胸围}$。

![image-20241215161959796](https://cdn.jsdelivr.net/gh/SchwertLin/Pic/img/image-20241215161959796.png)

对于成年男子上衣，有： $$ \text{累计贡献率} = \frac{129.0242}{147.32}×100\% = 87.6\% $$

> **Q1**：第一、第二主成份代表性是否足够？
> 
> **Q2**：停止？还是类似地继续寻找更多的主成份？

# 6.1 总体PCA

设$X\sim^pN_p(\mu,\Sigma)$。令$\Sigma$的特征根为$\lambda_1\ge\dots\ge\lambda_p\ge0$，特征根对应的**正则正交特征向量**为$\alpha_1,\dots,\alpha_p$。

令$T = (\alpha_1, \cdots, \alpha_p)$，则$T$是正交阵，且:  
$$ T'\Sigma T=\Lambda, \quad \Lambda = diag(\lambda_1, \cdots, \lambda_p) $$

1.  令$Y = T'X$，$Y=(y_1, \cdots, y_p)'$，则称$Y$为$X$的主成份. 令$\alpha_i = (\alpha_{1i}, \cdots, \alpha_{pi})'$，则:
    
    +   $X$的第$i$主成份: $y_i=\alpha_i'X=\sum_{j = 1}^p \alpha_{ji}x_j$
    +   $X$的第$i$主成份的方差：$Var(\alpha_i'X)=\alpha_i'\Sigma\alpha_i=\lambda_i$，$1\leq i\leq p$。
2.  $Y$的协方差阵为$Cov(Y)=T'\Sigma T=\Lambda$，因此有：
    
    1.  $X$的第$i$个主成份的方差为$Var(y_i)=\lambda_i$，$1\leq i\leq p$。
        
    2.  记$\Sigma = (\sigma_{ij})_{p\times p}$，则$Y$与$X$具有相同的散布程度。 $$ \sum_{i = 1}^p Var(y_i)=\sum_{i = 1}^p \lambda_i=tr(\Sigma)=\sum_{i = 1}^p \sigma_{ii}=\sum_{i = 1}^p Var(x_i) $$
        
    3.  任意两个主成份都相互独立。
        

  
| 定义 | 公式 | 说明 |
| --- | --- | --- |
| 第$k$个主成份$y_k$的贡献率 | $\lambda_k/\sum_{i = 1}^p \lambda_i$ | 表示第$k$个主成份保留总体$X$散布程度信息的比例. |
| 前$k$个主成份$(y_1, \cdots, y_k)$的累计贡献率 | $\sum_{i = 1}^k \lambda_i/\sum_{i = 1}^p \lambda_i$ | 表示前$k$个主成份保留总体散布程度信息的比例. |
| 第$k$个主成分$y_{k}$中变量$x_{j}$的因子负荷量 | $\rho_{y_{k},x_{j}}=\alpha_{jk}\sqrt{\lambda_{k}}/\sqrt{\sigma_{jj}}$ | $\sum_{k = 1}^{p}\rho_{y_{k},x_{j}}^{2}=\sum_{k = 1}^{p}\lambda_{k}\alpha_{jk}^{2}/\sigma_{jj}=1$ |
| 第$k$个主成分$y_{k}$的对于$X$的第$j$个分量$x_{j}$的贡献率 | $\rho_{y_{k},x_{j}}^{2}=\lambda_{k}\alpha_{jk}^{2}/\sigma_{jj}$ | 表示第$k$个主成分保留$x_{j}$离散程度的信息的比例. |
| 前$k$个主成分$(y_{1},\cdots,y_{k})$的对于$X$的第$j$个分量$x_{j}$的累计贡献率 | $\sum_{i = 1}^{k}\rho_{y_{i},x_{j}}^{2}=\sum_{i = 1}^{k}\lambda_{i}\alpha_{ij}^{2}/\sigma_{jj}$ | 表示前$k$个主成分保留$x_{j}$离散程度的信息的比例. |

## 6.1.1 主成分与总体的相关性

记$\Sigma$的第$j$个行向量为$(\sigma_{j1},\cdots,\sigma_{jp})$，$1\leq j\leq p$。

由于$\Sigma\alpha_{k}=\lambda_{k}\alpha_{k}$（$\lambda_k$是$\Sigma$的特征值，$\alpha_k$是$\Sigma$的对应的特征向量,取列向量)，因而有： $$ \sum_{i = 1}^{p}\sigma_{ji}\alpha_{ik}=\lambda_{k}\alpha_{jk} \\ \sum_{i = 1}^{p}\sigma_{ij}\alpha_{ik}=\lambda_{k}\alpha_{jk}\\ Cov(y_{k},x_{j}) = Cov\left(\sum_{i = 1}^{p}\alpha_{ik}x_{i},x_{j}\right)=\sum_{i = 1}^{p}\sigma_{ij}\alpha_{ik}=\lambda_{k}\alpha_{jk} $$ $X$的第$k$个主成分与$X$的第$j$个分量$x_{j}$的相关系数为 : $$ \rho_{y_{k},x_{j}}=\frac{Cov(y_{k},x_{j})}{\sqrt{Var(y_{k})}\sqrt{Var(x_{j})}}=\frac{\lambda_{k}\alpha_{jk}}{\sqrt{\lambda_{k}}\sqrt{\sigma_{jj}}}=\frac{\alpha_{jk}\sqrt{\lambda_{k}}}{\sqrt{\sigma_{jj}}} $$ 称$\rho_{y_{k},x_{j}}$为第$k$个主成分$y_{k}$中变量$x_{j}$的**因子负荷量**。

## 6.1.2 主成分与X分量的复相关系数

令$\rho_{Y,x_{j}}$为$Y$与$x_{j}$的复相关系数，$1\leq j\leq p$，则： $$ \rho_{Y,x_{j}}^{2}=\sum_{k = 1}^{p}\rho_{y_{k},x_{j}}^{2}=\frac{1}{\sigma_{jj}}\sum_{k = 1}^{p}\lambda_{k}\alpha_{jk}^{2},\ 1\leq j\leq p $$ 由$T'\Sigma T=\Lambda$，知$\Sigma = T\Lambda T'$，即有$\sigma_{jj}=\sum_{k = 1}^{p}\lambda_{k}\alpha_{jk}^{2}$，$1\leq j\leq p$。

则主成分$Y$与$X$的分量$x_{j}$的复相关系数$\rho_{Y,x_{j}} = 1$，$1\leq j\leq p$。

这说明主成分中含有分量$x_{j}$的离散程度的全部信息。

事实上，有$X = TY$，即知 : $$ $x_{j}=\sum_{k = 1}^{p}\alpha_{jk}y_{k},1\leq j\leq p $$

## 6.1.3 回到例子

回答我们上述提到的问题：

> **Q1**：第一、第二主成份代表性是否足够？
> 
> **Q2**：停止？还是类似地继续寻找更多的主成份？

![image-20241215162403948](https://cdn.jsdelivr.net/gh/SchwertLin/Pic/img/image-20241215162403948.png)

![image-20241215162416925](https://cdn.jsdelivr.net/gh/SchwertLin/Pic/img/image-20241215162416925.png)

> 第一、二主成分对身高：$95.04\%+2.62\%=97.66\%$
> 
> 第一、二主成分对胸围：$23.45\%+74.9\%=98.35\%$

# 6.2 R主成分分析:处理量纲

主成分分析主要是对随机变量的协方差矩阵进行分析，将向量投影到方差大的方向以获得重要的主成份。

> **Q：变量的量纲影响变量的方差，有必要消除量纲对方差的影响。**
> 
> A：对变量进行标准化处理，即令: $$ X^{}=\text{diag}(\sigma_{11}^{-1/2},\cdots,\sigma_{pp}^{-1/2})X = (\sigma_{11}^{-1/2}x_{1},\cdots,\sigma_{pp}^{-1/2}x_{p})' \\ \text{Cov}(X^{})=\text{diag}(\sigma_{11}^{-1/2},\cdots,\sigma_{pp}^{-1/2})\Sigma\text{diag}(\sigma_{11}^{-1/2},\cdots,\sigma_{pp}^{-1/2}) = R $$ 其中$R$是$X$的相关阵，$X^{}$的主成份与量纲无关。

## 6.2.1 R主成分分析的定义

设$R$的特征根为$\lambda_{1}^{}\geq\cdots\geq\lambda_{p}^{}\geq0$，与这些特征根对应的正则正交特征向量为$\alpha_{1}^{},\cdots,\alpha_{p}^{}$。令$T^{}=(\alpha_{1}^{},\cdots,\alpha_{p}^{})$， $$ Y^{}=(T^{})'X^{}=(T^{})'(\sigma_{11}^{-1/2}x_{1},\cdots,\sigma_{pp}^{-1/2}x_{p})' $$ 则称$Y^{}$为$X$的$R$主成份。

令$Y^{}=(y_{1}^{},\cdots,y_{p}^{})'$，$\alpha_{i}^{}=(\alpha_{1i}^{},\cdots,\alpha_{pi}^{})'$，则称: $$ y_{i}^{}=\alpha_{i}^{}X^{}=\sum_{j = 1}^{p}\alpha_{ji}^{}\sigma_{jj}^{-1/2}x_{j} $$ $y_{i}^{}$为$X$的第$i$个$R$主成份，$1\leq i\leq p$。

  
| 定义 | 公式 | 说明 |
| --- | --- | --- |
| $Y^{}$的协方差阵 | $\begin{align}\text{Cov}(Y^{})&=\Lambda^{}\\&=\text{diag}(\lambda_{1}^{},\cdots,\lambda_{p}^{})\end{align}$ | $\sum^p_{i=1}\lambda_i^=p$ |
| 第$k$个$R$主成份$y_{k}^{}$的贡献率 | $\lambda_{k}^{}/p$ | \-- |
| 前$k$个$R$主成份$(y_{1}^{},\cdots,y_{k}^{})$的累计贡献率 | ${\sum_{i = 1}^{k}\lambda_{i}^{}}/p$ | \-- |
| 第$k$个$R$主成份$y_{k}^{}$中变量$x_{j}$的因子负荷量 | $\alpha_{jk}^{}\sqrt{\lambda_{k}^{}}$ | $\sum_{k = 1}^{p}\lambda_{k}^{}(\alpha_{jk}^{})^{2}=1,\ 1\leq j\leq p$ |
| 前$k$个$R$主成份$(y_{1}^{},\cdots,y_{k}^{})$的对于$X$的第$j$个分量$x_{j}$的累计贡献率 | $\sum_{i = 1}^{k}\lambda_{i}^{}(\alpha_{ij}^{})^{2}$ | \-- |

# 6.3 样本主成分分析(基于观测数据)

假设总体$X\sim N_{p}(\mu,\Sigma)$，其观测样本为$x_{1},\cdots,x_{n}$，则$(\mu,\Sigma)$的极大似然估计为: $$ \hat{\mu}=\bar{x}=n^{-1}\sum_{i = 1}^{n}x_{i}\\ \hat{\Sigma}=S=n^{-1}\sum_{i = 1}^{n}(x_{i}-\bar{x})(x_{i}-\bar{x})' $$ 样本主成份分析也就是基于样本协方差阵$S$的主成份分析，它也等价于某个分布下的总体主成份分析。

**样本主成份的定义** :(使用$S$代替$\Sigma$)

 
| 相关定义 | 说明 |
| --- | --- |
| $S$的特征根 | $\hat{\lambda}_{1}\geq\cdots\geq\hat{\lambda}_{p}\geq0$ |
| 与特征根对应的正则正交特征向量 | $\hat{\alpha}_{1},\cdots,\hat{\alpha}_{p}$ |
| $\hat{Y}$为$X$的样本主成份 | 令$\hat{Y}=\hat{T}'X$，$\hat{Y}=(\hat{y}_{1},\cdots,\hat{y}_{p})'$，其中$\hat{T}=(\hat{\alpha}_{1},\cdots,\hat{\alpha}_{p})$. |
| $X$的第$k$样本主成份($1\leq k\leq p$) | 记$\hat{\alpha}_{k}=(\hat{\alpha}_{1k},\cdots,\hat{\alpha}_{pk})'$，则称$\hat{y}_{k}=\hat{\alpha}_{k}'X=\sum_{j = 1}^{p}\hat{\alpha}_{jk}x_{j}$. |

> $\hat{y}_{k}=\hat{\alpha}_{k}'X$: $\hat{\alpha}_{k}$和$\hat{\lambda}_{k}$分别是$X$的第$k$主成份$y_{k}=\alpha_{k}X$，第$k$主成分系数$\alpha_{k}$和第$k$主成份的方差$\lambda_{k}$的极大似然估计，$1\leq k\leq p$。

相应地，可以得到主成份对总体的贡献率、对总体分量的因子负荷量以及总体分量的贡献率的极大似然估计。

## 6.3.1 经验总体下的总体主成份分析

定义随机向量$X^{}$，它服从离散分布，分布函数为： $$ P(X^{}=x_{i})=\frac{1}{n}, \quad 1\leq i\leq n $$

则$X^{}$的分布就是样本$x_{1},\cdots,x_{n}$的经验分布。

显然有： $$ \begin{align}E(X^{})&=n^{-1}\sum_{i = 1}^{n}x_{i}=\bar{x}\\\\ Cov(X^{})&=E[(X^{}-E(X^{}))(X^{}-E(X^{}))']\\&=n^{-1}\sum_{i = 1}^{n}(x_{i}-\bar{x})(x_{i}-\bar{x})'=S \end{align} $$ **经验总体下主成份的求解** :

  
| 求$X^{}$的主成份 | 主成分 | 说明 |
| --- | --- | --- |
| (1) 求第一主成份 | $\hat{\alpha}_{1}X^{}$ | $\hat{\alpha}_{1}=\underset{\alpha'\alpha = 1}{\arg\max}Var(\alpha'X^{})=\underset{\alpha'\alpha = 1}{\arg\max}\alpha'S\alpha$ |
| (2) 求第二主成份 | $\hat{\alpha}_{2}X^{}$ | $\hat{\alpha}_{2}=\underset{\begin{subarray}{c}\alpha'\alpha = 1\\\alpha'\hat{\alpha}_{1}=0\end{subarray}}{\arg\max}Var(\alpha'X^{})=\underset{\begin{subarray}{c}\alpha'\alpha = 1\\\alpha'\hat{\alpha}_{1}=0\end{subarray}}{\arg\max}\alpha'S\alpha$ |
| (3) 依次求第三到第$p$主成份 | $\hat{\alpha}_{p}X^{}$ | \--- |

因此，$X^{}$的主成份系数与$X$的样本主成份系数是一致的，且: $$ Var(\hat{\alpha}_{i}'X^{})=\hat{\lambda}_{i},\ 1\leq i\leq p $$

# 6.4 样本R主成分分析

> **基于样本相关阵的主成分分析就是样本R主成分分析。**

记: $$ \hat{R} = diag(s_{11}^{-1/2},\cdots,s_{pp}^{-1/2})S \ diag(s_{11}^{-1/2},\cdots,s_{pp}^{-1/2}) $$ 即$\hat{R}$是样本相关阵。基于$\hat{R}$进行主成分分析即可。

此外，令: $$ x_{i}^{} = diag(s_{11}^{-1/2},\cdots,s_{pp}^{-1/2})(x_{i}-\bar{x}), \quad 1\leq i\leq n $$ 那么$x_{1}^{},\cdots,x_{n}^{}$的样本协差阵也是$x_{1},\cdots,x_{n}$的样本相关阵$\hat{R}$。

则对$x_{1}^{},\cdots,x_{n}^{}$进行主成分分析即是样本R主成分分析。

> PS:
> 
> +   (总体)主成分分析与R主成分分析的结论**可能不一致**。
> +   样本主成分分析与样本R主成分分析的结论**可能不一致**。

# 6.5 主成分的统计推断

对实际数据进行的主成份分析时，事先会设定一个主成份贡献率的阈值(1 - δ)。

得到样本的主成份后，可以计算前k个样本主成份的贡献率: $*{i = 1}^{k}* {i} / *{i = 1}^{p}* {i} $

如果: $$ \sum_{i = 1}^{k} \hat{\lambda}_{i} / \sum_{i = 1}^{p} \hat{\lambda}_{i} > (1 - \delta)\\ $$ **是否就可以认为:** $$ \sum_{i = 1}^{k} \lambda_{i} / \sum_{i = 1}^{p} \lambda_{i} > (1 - \delta) ? $$ **A: 需要对协差阵的特征根$*{1}* {p} $进行统计推断。**

> 首先假定$> 0 $，则参数$(,) $的似然函数为: $$ \frac{1}{|\Sigma|^{n/2}} \exp\left\{-\frac{1}{2}tr[\Sigma^{-1}(V + n(\bar{x}-\mu)(\bar{x}-\mu)')]\right\} $$ 由于$= TT' $，即$(*{1},,*{p}) $和$(*{1},,*{p}) $仅与$$有关，其似然函数为 : $$ \begin{align}L(\lambda_{1},\cdots,\lambda_{p},\alpha_{1},\cdots,\alpha_{p})&=\frac{1}{|\Sigma|^{n/2}} \exp\left\{-\frac{1}{2}tr(\Sigma^{-1}V)\right\}\\ &=\frac{1}{|T\Lambda T'|^{n/2}} \exp\left\{-\frac{1}{2}tr(T\Lambda^{-1}T'V)\right\} \\ &= \left(\prod_{i = 1}^{p} \lambda_{i}\right)^{-n/2} \exp\left\{-\frac{1}{2}\left(\sum_{i = 1}^{p} \frac{\alpha_{i}'V\alpha_{i}}{\lambda_{i}}\right)\right\} \end{align} $$ 为简单起见，再假定$*{1}>>*{p}>0 $，即**所有特征根都不等**。
> 
> 此时$*{1},,*{p} $与$*{1},,*{p} $无关。
> 
> 因为由$$的任意性，在给定$*{1},,*{p} $下，正交矩阵$T = (*{1},,*{p}) $也是任意的。
> 
> 事实上，考虑参数的自由度：在$*{1}>>*{p}>0 $下 $$ dim(\Lambda)=p, \quad dim(T)=p^{2}-p-\frac{p(p - 1)}{2} \\ dim(\Lambda)+dim(T)=\frac{p(p + 1)}{2}=dim(\Sigma) $$

## 6.5.1 Fisher信息阵与极大似然估计的渐近正态性

假设$x_{1},,x_{n} $是服从密度函数为$(x,) $的独立样本。 记$ $为$$的极大似然估计，$X^{(n)}=(x_{1},,x_{n}) $。对数似然函数为: $$ l(\theta|X^{(n)})=\sum_{i = 1}^{n} \log \rho(x_{i},\theta) $$ 则Fisher信息阵为: $$ \begin{align} I_{n}(\theta)&=V_{ar\theta}\left[\frac{\partial l(\theta|X^{(n)})}{\partial \theta}\right]\quad\text{（一般性的定义）}\\ &=-E_{\theta}\left[\frac{\partial^{2}l(\theta|X^{(n)})}{\partial \theta^{2}}\right] \\ &=-nE_{\theta}\left[\frac{\partial^{2}}{\partial \theta^{2}}\log \rho(x_{1},\theta)\right]\quad\text{（独立同分布下）}\\ &\triangleq nI(\theta) \end{align} $$ **$ $的渐近正态性(一般情形):** $$ (I_{n}(\theta))^{1/2}(\hat{\theta}-\theta) \stackrel{d}{\rightarrow} N(0,I_{p}) (n\rightarrow\infty) $$ 在独立同分布情形下，有 : $$ \sqrt{n}(\hat{\theta}-\theta) \stackrel{d}{\rightarrow} N(0,I^{-1}(\theta)) (n\rightarrow\infty) $$

## $(\hat{\lambda}_{1},\cdots,\hat{\lambda}_{p})$的渐近分布

有对数似然函数: $$ l(\lambda_{1},\cdots,\lambda_{p},\alpha_{1},\cdots,\alpha_{p})=\sum_{i = 1}^{p}\left(-\frac{n}{2}\log\lambda_{i}-\frac{1}{2\lambda_{i}}\alpha_{i}'V\alpha_{i}\right)\triangleq\sum^p_{i=1}l(\lambda_i,\alpha_i) $$ 因此对任意的$i\neq j$，有: $$ \frac{\partial^{2}l(\theta|X^{(n)})}{\partial\lambda_{i}\partial\lambda_{j}} = \frac{\partial^{2}l(\lambda_{1},\cdots,\lambda_{p},\alpha_{1},\cdots,\alpha_{p})}{\partial\lambda_{i}\partial\lambda_{j}}=0 $$ 那么由Fisher信息阵的结构，知$\hat{\lambda}_{1},\cdots,\hat{\lambda}_{p}$的极限分布是相互独立的正态分布。

**$\hat{\lambda}_{1},\cdots,\hat{\lambda}_{p}$的渐近方差:**

由于$V\stackrel{d}{=}W_{p}(n - 1,\Sigma)$，等价地有 : $$ V\stackrel{d}{=}\sum_{k = 1}^{n - 1}Z_{k}Z_{k}' $$ 其中，$Z_{1},\cdots,Z_{n - 1}$是i.i.d.的正态$N_{p}(0,\Sigma)$随机向量。

因此，对$1\leq i\leq p$，有 : $$ \alpha_{i}'V\alpha_{i}\stackrel{d}{=}\sum_{k = 1}^{n - 1}(\alpha_{i}'Z_{k})^{2} $$ 由于$\alpha_{i}'\Sigma\alpha_{i}=\lambda_{i}$，知$\alpha_{i}'Z_{1},\cdots,\alpha_{i}'Z_{n - 1}$是独立同分布的$N_{1}(0,\lambda_{i})$随机变量。因此 $$ \alpha_{i}'V\alpha_{i}\stackrel{d}{=}\lambda_{i}\chi^{2}(n - 1) $$

**计算$\lambda_{i}$的Fisher信息** : $$ \begin{align}-E_{(\lambda_{i},\alpha_{i})}\left[\frac{\partial^{2}l(\lambda_{i})}{\partial\lambda_{i}^{2}}\right]&=-E_{(\lambda_{i},\alpha_{i})}\left[\frac{n}{2\lambda_{i}^{2}}-\frac{\alpha_{i}'V\alpha_{i}}{\lambda_{i}^{3}}\right]\\ &=-\frac{n}{2\lambda_{i}^{2}}+\frac{(n - 1)\lambda_{i}}{\lambda_i^3}\\ &=\frac{n-2}{2\lambda_{i}^{2}} \end{align} $$ 则$(\hat{\lambda}_{1},\cdots,\hat{\lambda}_{p})$的Fisher信息阵为: $$ I_{n}=diag\left(\frac{n - 2}{2\lambda_{1}^{2}},\cdots,\frac{n - 2}{2\lambda_{p}^{2}}\right) $$ 由极大似然估计的渐近正态性知: $$ I_{n}^{1/2}\left(\begin{array}{c} \hat{\lambda}_{1}-\lambda_{1}\\ \vdots\\ \hat{\lambda}_{n}-\lambda_{n} \end{array}\right)\stackrel{d}{\rightarrow}N(0,I_{p})(n\rightarrow\infty) \\ n\rightarrow \infty,\quad\sqrt{n - 2}\left(\begin{array}{c} \hat{\lambda}_{1}-\lambda_{1}\\ \vdots\\ \hat{\lambda}_{n}-\lambda_{n} \end{array}\right)\stackrel{d}{\rightarrow}N(0,diag(2\lambda_{1}^{2},\cdots,2\lambda_{p}^{2})) $$

> **当$\Sigma$的特征根有重根时**，情况比较复杂。
> 
> 由极大似然估计的渐近正态性可以构造$\lambda_{i}$的渐近置信区间: $$ \hat{\lambda}_{i}\left[1+\sqrt{2/(n - 2)}Z_{1-\beta/2}\right]^{-1}\leq\lambda_{i}\leq\hat{\lambda}_{i}\left[1-\sqrt{2/(n - 2)}Z_{1-\beta/2}\right]^{-1} $$ 也可通过方差齐性变换，导出 : $$ \sqrt{n - 2}(\ln(\hat{\lambda}_{i}^{\sqrt{2}/2})-\ln(\lambda_{i}^{\sqrt{2}/2}))\stackrel{d}{\rightarrow}N(0,1) $$ 可得$\lambda_{i}$的另一个置信水平为$(1-\beta)$的渐近置信区间: $$ \hat{\lambda}_{i}\exp\left\{-\frac{2}{n - 2}Z_{1-\beta/2}\right\}\leq\lambda_{i}\leq\hat{\lambda}_{i}\exp\left\{\frac{2}{n - 2}Z_{1-\beta/2}\right\} $$

## 6.5.2 与主成分分析有关的检验问题

## A.检验问题I

$$ H_0:\lambda_{k + 1}+\cdots+\lambda_p\leq\gamma $$

**检验统计量的构造** - 由$(\hat{\lambda}_1,\cdots,\hat{\lambda}_p)$的渐近正态性，有 : $$ \sqrt{n - 2}\left(\sum_{i = k+1}^{p}\hat{\lambda}_i-\sum_{i = k+1}^{p}\lambda_i\right)\stackrel{d}{\rightarrow}N\left(0,\sum_{i = k+1}^{p}2\lambda_i^2\right) $$ 进而可得 : $$ \frac{\sqrt{n - 2}\left(\sum_{i = k+1}^{p}\hat{\lambda}_i-\sum_{i = k+1}^{p}\lambda_i\right)}{\sqrt{\sum_{i = k+1}^{p}2\hat{\lambda}_i^2}}\stackrel{d}{\rightarrow}N(0,1) $$ 当: $$ \sum_{i = k+1}^{p}\hat{\lambda}_i>\gamma+\sqrt{\frac{\sum_{i = k+1}^{p}2\hat{\lambda}_i^2}{n - 2}}Z_{1-\alpha} $$ 时，拒绝零假设，它犯第一类错误的概率渐近不超过$\alpha$。

## B.检验问题II

**前k个主成分的累计贡献率是否大于给定的值$\delta$?** $$ H_0:\frac{\sum_{i = 1}^{k}\lambda_i}{\sum_{i = 1}^{p}\lambda_i}\leq\delta $$ 考虑如下的累计贡献率统计量的渐近分布 :  
$$ \sqrt{n - 2}\left(\frac{\sum_{i = 1}^{k}\hat{\lambda}_i}{\sum_{i = 1}^{p}\hat{\lambda}_i}-\frac{\sum_{i = 1}^{k}\lambda_i}{\sum_{i = 1}^{p}\lambda_i}\right) $$ 定义如下的累计贡献率函数: $$ f(\lambda_1,\cdots,\lambda_p)=\frac{\sum_{i = 1}^{k}\lambda_i}{\sum_{i = 1}^{p}\lambda_i} $$ 由Cramér定理有: $$ \sqrt{n - 2}(f(\hat{\lambda}_1,\cdots,\hat{\lambda}_p)-f(\lambda_1,\cdots,\lambda_p))\stackrel{d}{\rightarrow}N(0,\nu^2) $$ 其中 : $$ \nu^2=\frac{2\left[\left(\sum_{i = k+1}^{p}\lambda_i\right)^2\left(\sum_{i = 1}^{k}\lambda_i^2\right)+\left(\sum_{i = 1}^{k}\lambda_i\right)^2\left(\sum_{i = k+1}^{p}\lambda_i^2\right)\right]}{\left(\sum_{i = 1}^{p}\lambda_i\right)^4} $$ 事实上，若记$\lambda = (\lambda_{1},\cdots,\lambda_{p})'$,则有： $$ \frac{\partial f(\lambda)}{\partial \lambda_{i}}=\frac{I(1\leq i\leq k)}{\sum_{j = 1}^{p} \lambda_{j}}-\frac{\sum_{j = 1}^{k} \lambda_{j}}{(\sum_{j = 1}^{p} \lambda_{j})^{2}},\ 1\leq i\leq p $$ 因此: $$ \begin{align} v^{2}&=\left(\frac{\partial f(\lambda)}{\partial \lambda}\right)'\text{diag}(2\lambda_{1}^{2},\cdots,2\lambda_{p}^{2})\frac{\partial f(\lambda)}{\partial \lambda}\\ &=2\sum_{i = 1}^{p} \lambda_{i}^{2}\left(\frac{I(1\leq i\leq k)}{\sum_{j = 1}^{p} \lambda_{j}}-\frac{\sum_{j = 1}^{k} \lambda_{j}}{(\sum_{j = 1}^{p} \lambda_{j})^{2}}\right)^{2} \end{align} $$

> $I(1\leq i\leq k)$是指示函数：
> 
> +   $i\le k: I(1\leq i\leq k)=1$
> +   $i\gt k : I(1\leq i\leq k)=0$

将极大似然估计$\hat{\lambda}_1,\cdots,\hat{\lambda}_p$代入$\nu^2$即得估计$\hat{\nu}^2$，  
$$ \hat{\nu}^2=\frac{2\left[\left(\sum_{i = k+1}^{p}\hat{\lambda}_i\right)^2\left(\sum_{i = 1}^{k}\hat{\lambda}_i^2\right)+\left(\sum_{i = 1}^{k}\hat{\lambda}_i\right)^2\left(\sum_{i = k+1}^{p}\hat{\lambda}_i^2\right)\right]}{\left(\sum_{i = 1}^{p}\hat{\lambda}_i\right)^4} $$ 因此有: $$ \frac{\sqrt{n - 2}}{\hat v}\left(\frac{\sum_{i = 1}^{k}\hat{\lambda}_i}{\sum_{i = 1}^{p}\hat{\lambda}_i}-\frac{\sum_{i = 1}^{k}\lambda_i}{\sum_{i = 1}^{p}\lambda_i}\right)\stackrel{d}{\rightarrow}N(0,1) $$ **结论**：当:  
$$ \because\frac{\sqrt{n-2}}{\hat{\nu}} \left( \frac{\sum_{i=1}^k \hat{\lambda}_i}{\sum_{i=1}^p \hat{\lambda}_i} - \delta \right) > Z_{1-\alpha}\\ \therefore\frac{\sum_{i = 1}^{k}\hat{\lambda}_i}{\sum_{i = 1}^{p}\hat{\lambda}_i}\geq\delta+\frac{\hat{\nu}}{\sqrt{n - 2}}Z_{1-\alpha}\\ \therefore\frac{\sum_{i = 1}^{k}\lambda_i}{\sum_{i = 1}^{p}\lambda_i}>\delta $$ 当标准化的统计量大于$Z_{1-\alpha}$时拒绝零假设，它犯第一类错误的概率渐近不超过$\alpha$。

## C.再次回到例子(统计检验)

样本协差阵的特征根从大到小依次为：

   
| $\hat{\lambda}_{1} = 100.5771$ | $\hat{\lambda}_{2} = 28.4471$ | $\hat{\lambda}_{3} = 5.7489$ | $\hat{\lambda}_{4} = 4.4522$ |
| --- | --- | --- | --- |
| $\hat{\lambda}_{5} = 3.1978$ | $\hat{\lambda}_{6} = 2.5854$ | $\hat{\lambda}_{7} = 1.3834$ | $\hat{\lambda}_{8} = 0.9280$ |

设定累计贡献率的阈值$\delta= 0.85$、显著性水平设定为$\alpha = 0.05$

由于$\frac{\sum_{i = 1}^{2}\hat{\lambda}_{i}}{\sum_{i = 1}^{8}\hat{\lambda}_{i}}=87.6\%$，我们把零假设设定为： $$ H_{0}:\frac{\sum_{i = 1}^{2}\lambda_{i}}{\sum_{i = 1}^{8}\lambda_{i}}\leq\delta = 0.85 $$

> 即检验问题Ⅱ：前2个主成分的累计贡献率是否大于给定的值$\delta$？

计算$\hat v^2$: $$ \begin{align}\hat{\nu}^{2}&=\frac{2\left[\left(\sum_{i = 3}^{8}\hat{\lambda}_{i}\right)^{2}\left(\sum_{i = 1}^{2}\hat{\lambda}_{i}^{2}\right)+\left(\sum_{i = 1}^{2}\hat{\lambda}_{i}\right)^{2}\left(\sum_{i = 3}^{8}\hat{\lambda}_{i}^{2}\right)\right]}{\left(\sum_{i = 1}^{8}\hat{\lambda}_{i}\right)^{4}}\\ &=0.0207 \end{align} $$ **计算检验临界值** : 其中$n = 5115$， $$ Z_{1-\alpha}=Z_{0.95}=1.6449\\ C_{r}=\delta+\frac{\hat{\nu}}{\sqrt{n - 2}}Z_{1-\alpha}=0.8533\\ \frac{\sum_{i = 1}^{2}\hat{\lambda}_{i}}{\sum_{i = 1}^{8}\hat{\lambda}_{i}}=0.876 > C_{r}=0.8533 $$ **结论**：拒绝零假设，即认为$\frac{\sum_{i = 1}^{2}\lambda_{i}}{\sum_{i = 1}^{8}\lambda_{i}}>0.85$，两个主成分已满足代表原总体散度的要求。

## 6.5.3 R主成分分析的检验

由于在R主成份分析中，样本相关阵的特征根$\hat{\lambda}_{1}^{},\cdots,\hat{\lambda}_{p}^{}$要满足约束条件$\sum_{i = 1}^{p}\hat{\lambda}_{i}^{}=1$。因此，$\hat{\lambda}_{1}^{},\cdots,\hat{\lambda}_{p}^{}$不再是渐近独立的。

此外，$(\lambda_{1}^{},\cdots,\lambda_{p}^{})$与$(\alpha_{1}^{},\cdots,\alpha_{p}^{})$不再是无关的，因此有关主成份分析的渐近理论对R主成份分析不再成立。
