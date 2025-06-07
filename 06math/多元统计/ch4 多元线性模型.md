# 4.0 一元线性模型

假设有自变量$x=(x_{(1)},\cdots,x_{(k)})'\in R^k$，因变量$y\in R^1$。

一元线性模型的定义： $$ y = x'\beta+\epsilon $$ 其中，$\beta = (\beta_1,\cdots,\beta_k)'\in R^k$是模型参数， $\epsilon$是随机误差，$E(\epsilon|x) = 0$。

$x'\beta$是$y$对$x$的线性回归: $$ E(y|x)=E(x'\beta+\epsilon|x)=x'\beta + E(\epsilon|x)=x'\beta\\ y=x_{(1)}\beta_1+\cdots + x_{(k)}\beta_k+\epsilon $$

## 4.0.1 模型参数的估计

假设有$n$组观测$(x_1,y_1),\cdots,(x_n,y_n)$。 最小二乘法即最小化误差平方和（Residual Sum of Squares, RSS, 我们的目标函数）： 
$$ RSS({\beta})=\sum_{i = 1}^{n}(y_i - x_i'\beta)^2 $$
$$ \hat\beta =\arg\min_{\beta\in R^k} RSS(\beta) $$ 记$Y=(y_1,\cdots,y_n)'\in R^n$，$X=(x_1,\cdots,x_n)'$是$n\times k$的矩阵， $\epsilon = (\epsilon_1,\cdots,\epsilon_n)'\in R^n$。

+   则对这组观测，模型可表示为 $Y = X\beta+\epsilon$。
+   则$\beta$的最小二乘法估计为 $\hat{\beta}=(X'X)^{-1}X'Y$。

> $$ \begin{align} RSS(\beta) &=(Y-X\beta)'(Y-X\beta)\\ &=Y'Y-Y'X\beta-(X\beta)'Y+(X\beta)'(X\beta)\\ &=Y'Y-2\beta'X'Y+\beta'X'X\beta\\\\ \frac{\partial{RSS(\beta) }}{\partial\beta}&=-2X'Y+2X'X\beta=0\\ X'X\beta&=X'Y\\ \hat\beta&=(X'X)^{-1}X'Y \end{align}\\ $$

**模型的应用**：

1.  对未来的设计变量$x$，可以预测相应的因变量$y$：$\hat{y}=x'\hat{\beta}$。
2.  当自变量为单变量时，为了控制未来的因变量$y$， 可以约束自变量的取值范围。

# 4.1 多元线性模型

> 相当于x和y由一个值变为一个向量. 此时x在$\mathbb{R}^k$空间，y在$\mathbb{R}^p$空间.

假设有自变量$x=(x_{(1)},\cdots,x_{(k)})'\in R^k$，因变量$y=(y_{(1)},\cdots,y_{(p)})'\in R^p$。

$y$与$x$的关系可表示为如下$p$个一元线性模型： $$ y_{(i)} = x'\beta_i+\epsilon_{(i)} $$ $1\leq i\leq p$， 其中，$\beta_1,\cdots,\beta_p\in R^k$是每个子线性模型的参数， $\epsilon_{(i)}$是每个因变量对应的随机误差，$E(\epsilon_{(i)}|x) = 0$，$1\leq i\leq p$。

记$B = (\beta_1,\cdots,\beta_p)$是$k\times p$的模型参数矩阵， $\epsilon = (\epsilon_{(1)},\cdots,\epsilon_{(p)})'$是误差向量。 那么，$y$与$x$的关系可表示为: $$ y' = x'B+\epsilon' $$ 假设有$n$组观测$(x_1,y_1),\cdots,(x_n,y_n)$。 记$Y=(y_1,\cdots,y_n)'$，$X=(x_1,\cdots,x_n)'$，$e = (\epsilon_1,\cdots,\epsilon_n)'$。

> x 和 y 由向量转变为矩阵，原先只是在$\mathbb{R}^k,\mathbb{R}^p$空间，现在在$\mathbb{R}^{nk},\mathbb{R}^{np}$空间。

多元线性模型的**定义**如下： $Y = XB + e$，

其中:

1.  $Y$是$n\times p$阶观测的随机矩阵，$n\geq p$；
2.  $X$是已知的$n\times k$阶设计矩阵，$n\geq k$，$rank(X)=r\leq k$； (3)
3.  是$k\times p$阶的未知回归系数矩阵；
4.  $e$是$n\times p$阶不可观测的随机误差矩阵。

若记 : $$ \begin{align} Y&=\begin{pmatrix}y_{(11)}&y_{(12)}&\cdots&y_{(1p)}\\y_{(21)}&y_{(22)}&\cdots&y_{(2p)}\\\vdots&\vdots&\ddots&\vdots\\y_{(n1)}&y_{(n2)}&\cdots&y_{(np)}\end{pmatrix}=\begin{pmatrix}y_1'\\y_2'\\\vdots\\y_n'\end{pmatrix}=(Y_{(1)},\cdots,Y_{(p)})'\\ X&=\begin{pmatrix}x_{(11)}&x_{(12)}&\cdots&x_{(1k)}\\x_{(21)}&x_{(22)}&\cdots&x_{(2k)}\\\vdots&\vdots&\ddots&\vdots\\x_{(n1)}&x_{(n2)}&\cdots&x_{(nk)}\end{pmatrix}=\begin{pmatrix}x_1'\\x_2'\\\vdots\\x_n'\end{pmatrix}\\ e&=\begin{pmatrix}\epsilon_{(11)}&\epsilon_{(12)}&\cdots&\epsilon_{(1p)}\\\epsilon_{(21)}&\epsilon_{(22)}&\cdots&\epsilon_{(2p)}\\\vdots&\vdots&\ddots&\vdots\\\epsilon_{(n1)}&\epsilon_{(n2)}&\cdots&\epsilon_{(np)}\end{pmatrix}=\begin{pmatrix}\epsilon_1'\\\epsilon_2'\\\vdots\\\epsilon_n'\end{pmatrix}=(\epsilon_{(1)},\cdots,\epsilon_{(p)})' \end{align} $$ 则模型 $Y = XB + e$ 化为 $y_{(ij)} = x_i'\beta_j+\epsilon_{(ij)}$，$1\leq i\leq n$，$1\leq j\leq p$。

我们假定$\varepsilon$服从正态分布，只在特别情况下会说明只假定一、二阶矩存在(有界)的情形。

> **Q: 一阶矩、二阶矩？**
> 
> A: **矩（moment）**是用来描述随机变量分布特性的数字量度。
> 
> +   一阶矩：均值、$E$$X$$=\mu$
> +   二阶矩：方差、协方差：$Var(X)=E$$(X-E(X))^2$$, Cov(X,Y)=E$$(X-E(X))(Y-E(Y))$$$

假设$\varepsilon\sim N_{n\times p}(0,\Sigma\otimes I_n)$，其中误差协方差阵$\Sigma$是未知的$p$阶正定矩阵。 由$e'=(\varepsilon_{1},\cdots,\varepsilon_{n})$，知$\varepsilon_{1},\cdots,\varepsilon_{n}$独立同分布，且$\varepsilon_{1}\stackrel{d}{~}N_{p}(0,\Sigma)$。 $e\sim N_{n\times p}(0,\Sigma\otimes I_n)$，则$Y\sim N_{n\times p}(XB,\Sigma\otimes I_n)$。 则有 : $$ y_{i}^{\prime}=x_{i}^{\prime}B+\varepsilon_{i}^{\prime}\sim N_{p}(x_{i}^{\prime}B,\Sigma), 1\leq i\leq n $$

> 由于 $y_i' = x_i' B + \varepsilon_i'$，这里的 $x_i' B$ 是一个常数向量（因为给定了自变量 $x_i'$ 和回归系数 B），而 $\varepsilon_i'$ 是一个多维正态随机向量。

那么模型 $Y = XB + e$ 可以理解为 : $$ \begin{cases} E(Y)=XB\\ {Y的行向量}y_{1}^{\prime},\cdots,y_{n}^{\prime}是相互独立的正态向量，同协方差阵\Sigma,\Sigma>0. \end{cases} $$ 记$Y=(Y_{(1)},\cdots,Y_{(p)}),B = (\beta_{1},\cdots,\beta_{p}),e=(\varepsilon_{(1)},\cdots,\varepsilon_{(p)})$，则有: $$ Y_{(j)}=X\beta_{j}+\varepsilon_{(j)},\quad 1\leq j\leq p $$ 即模型$Y = XB + e$可以分解为$p$个一元线性模型，这$p$个一元线性模型有相同的设计矩阵$X$。

不难得出$\beta_{j}$的最小二乘估计为 $\hat{\beta}_{j}=(X^{\prime}X)^{-}X^{\prime}Y_{(j)}$，$1\leq j\leq p$。

若$rank(X)=k$，则$(X^{\prime}X)^{-}=(X^{\prime}X)^{-1}$.

> $(X^{\prime}X)^{-}$表示Moore-Penrose伪逆、当X满秩的时候伪逆=真逆）

进而有$B$的最小二乘估计为 $\hat{B}=(\hat{\beta}_{1},\cdots,\hat{\beta}_{p})=(X^{\prime}X)^{-1}X^{\prime}(Y_{(1)},\cdots,Y_{(p)})=(X^{\prime}X)^{-1}X^{\prime}Y$。

> **Q: 设计矩阵？**
> 
> A: **设计矩阵（Design Matrix）** 是回归分析中的一个重要概念，用于表示回归模型中自变量（或特征）和观测数据之间的关系。对于多元回归模型 $Y = X B + e$，设计矩阵 X 存储了所有观测点的自变量值。具体来说：
> 
> +   Y 是因变量的观测矩阵，表示所有观测点和因变量的值。
> +   X 是设计矩阵，包含所有观测点的自变量（或特征）值，通常是一个 $n \times k$的矩阵，其中：
>     +   n 是观测点的数量（样本数量）。
>     +   k 是自变量的数量（包括常数项，如果有的话）。

## 例1: p维的正态分布

设$Y^{\prime}=(y_{1},\cdots,y_{n})$是来自$N_{p}(\mu,\Sigma)$的样本，$\Sigma>0$。则 $$ \begin{cases}E(Y) = XB,\\Y的行向量y_{1}^{\prime},\cdots,y_{n}^{\prime}是相互独立的正态向量，协方差阵\Sigma,\Sigma>0,\end{cases} $$ 其中，设计矩阵$X = 1_{n},\ B=\mu^{\prime}$。

## 例2: 多元方差分析

设有$k$个相互独立的总体$Y_{j}\stackrel{d}{\sim}N_{p}(\mu_{j},\Sigma)$，$k\geq2$。 $y_{j1},\cdots,y_{jn_{j}}$是来自总体$Y_{j}$的样本，$1\leq j\leq k,\ \Sigma>0$。记$n=\sum_{j = 1}^{k}n_{j}$ .

这相当于如下的多元线性模型 : $$ \begin{cases}E(Y) = XB,\\Y的行向量y_{1}^{\prime},\cdots,y_{n}^{\prime}是相互独立的正态向量，协方差阵\Sigma,\Sigma>0,\end{cases} $$ 其中， $X=\begin{pmatrix}1_{n_{1}}&0&\cdots&0\\0&1_{n_2}&\cdots&0\\\vdots&\vdots&\ddots&\vdots\\0&0&\cdots&1_{n_{k}}\end{pmatrix}$是$n\times k$阶对角分块矩阵， $B=\begin{pmatrix}\mu_{1}^{\prime}\\\mu_2'\\\vdots\\\mu_{k}^{\prime}\end{pmatrix}$是$k\times p$阶矩阵。

# 4.2 充分统计量

由等价模型知，Y的行向量$y_{1}^{\prime},\cdots,y_{n}^{\prime}$相互独立，且$y_{i}\stackrel{d}{\sim}N_{p}(x_{i}^{\prime}B,\Sigma)$，$1\leq i\leq n$。

那么有Y的密度函数为 : $$ \begin{align\*} f(Y|B,\Sigma)&=\prod_{i = 1}^{n}\frac{1}{(2\pi)^{p/2}|\Sigma|^{1/2}}\exp\left\{-\frac{1}{2}(y_{i}-x_{i}^{\prime}B)^{\prime}\Sigma^{-1}(y_{i}-x_{i}^{\prime}B)\right\}\\ &=\frac{1}{(2\pi)^{np/2}|\Sigma|^{n/2}}\exp\left\{\frac{1}{2}\text{tr}$$(Y - XB)\Sigma^{-1}(Y - XB)^{\prime}$$\right\}\\ &=\frac{1}{(2\pi)^{np/2}|\Sigma|^{n/2}}\exp\left\{\frac{1}{2}\text{tr}$$(Y - XB)^{\prime}(Y - XB)\Sigma^{-1}$$\right\}\\ &=\frac{\exp\left\{-\text{tr}(B^{\prime}X^{\prime}XB\Sigma^{-1})\right\}}{(2\pi)^{np/2}|\Sigma|^{n/2}}\exp\left\{\frac{1}{2}\text{tr}(Y^{\prime}Y\Sigma^{-1}-2B^{\prime}X^{\prime}Y\Sigma^{-1})\right\} \end{align\*} $$ 显然Y的分布是指数族分布，**$(Y^{\prime}Y,X^{\prime}Y)$是参数$(B,\Sigma)$的充分统计量。**

注意到，Y的密度还可以写为: $$ \begin{align} f(Y|B,\Sigma)&=\frac{1}{(2\pi)^{np/2}|\Sigma|^{n/2}}\exp\left\{\frac{1}{2}\text{tr}$$(Y - XB)^{\prime}(Y - XB)\Sigma^{-1}$$\right\} \\ &=\frac{1}{(2\pi)^{np/2}|\Sigma|^{n/2}}\exp\left\{-\frac{1}{2}\text{tr}$$Y^{\prime}(I_{n}-X(X^{\prime}X)^{-1}X^{\prime})Y\Sigma^{-1}$$\right\}\\ &-\frac{1}{2}\text{tr}\left$$((X^{\prime}X)^{-1}X^{\prime}Y - B)^{\prime}(X^{\prime}X)((X^{\prime}X)^{-1}X^{\prime}Y - B)\Sigma^{-1}\right$$ \end{align} $$ 可见$( (X^{\prime}X)^{-1}X^{\prime}Y, Y^{\prime}(I_{n}-X(X^{\prime}X)^{-1}X^{\prime})Y)$也是$(B,\Sigma)$的充分统计量。 平方和分解公式 : $$ \begin{align}(Y - XB)^{\prime}(Y - XB)&=Y^{\prime}(I_{n}-X(X^{\prime}X)^{-1}X^{\prime})Y\\ &+(X^{\prime}X)^{-1}X^{\prime}Y - B)^{\prime}X^{\prime}X((X^{\prime}X)^{-1}X^{\prime}Y - B)\end{align} $$

> 下面的这种用于X列非满秩的情况、没有逆，只能使用伪逆。

## 情形1：$rank(X)=k$ X列满秩

## 性质4.1.1

1.  $(X^{\prime}X)^{-1}X^{\prime}Y\stackrel{d}{\sim}N_{k\times p}(B,\Sigma\otimes(X^{\prime}X)^{-1})$；
2.  $Y^{\prime}(I_{n}-X(X^{\prime}X)^{-1}X^{\prime})Y\stackrel{d}{\sim}W_{p}(n - k,\Sigma)$；
3.  $(X^{\prime}X)^{-1}X^{\prime}Y$与$Y^{\prime}(I_{n}-X(X^{\prime}X)^{-1}X^{\prime})Y$相互独立。

> **(1) 证明**：由于$Y\stackrel{d}{\sim}N_{n\times p}(XB,\Sigma\otimes I_{n})$，即$vec(Y)\stackrel{d}{\sim}N_{np}(XB,\Sigma\otimes I_{n})$。 又有 : $$ vec((X^{\prime}X)^{-1}X^{\prime}Y)=vec((X^{\prime}X)^{-1}X^{\prime}YI_{p})=(I_{p}\otimes(X^{\prime}X)^{-1}X^{\prime})vec(Y)\\\\ \begin{align\*} E$$vec((X^{\prime}X)^{-1}X^{\prime}Y)$$&=(I_{p}\otimes(X^{\prime}X)^{-1}X^{\prime})E$$vec(Y)$$\\ &=(I_{p}\otimes(X^{\prime}X)^{-1}X^{\prime})vec(XB)\\ &=vec(((X^{\prime}X)^{-1}X^{\prime})(XB)I_{p})\\ &=vec(B)\\\\ Cov$$vec((X^{\prime}X)^{-1}X^{\prime}Y)$$&=(I_{p}\otimes(X^{\prime}X)^{-1}X^{\prime})Cov$$vec(Y)$$(I_{p}\otimes(X^{\prime}X)^{-1}X^{\prime})^{\prime}\\ &=(I_{p}\otimes(X^{\prime}X)^{-1}X^{\prime})(\Sigma\otimes I_{n})(I_{p}\otimes(X^{\prime}X)^{-1}X^{\prime})^{\prime}\\ &=\Sigma\otimes(X^{\prime}X)^{-1} \end{align\*} $$ 故知$vec((X^{\prime}X)^{-1}X^{\prime}Y)\stackrel{d}{\sim}N_{kp}(vec(B),\Sigma\otimes(X^{\prime}X)^{-1})$，即(1)成立。
> 
> **(2) 证明**：由于$Y = XB + e$，有 ： $$ Y^{\prime}(I_{n}-X(X^{\prime}X)^{-1}X^{\prime})Y = e^{\prime}(I_{n}-X(X^{\prime}X)^{-1}X^{\prime})e $$ 由误差向量的独立同正态分布性知$e^{\prime}\stackrel{d}{\sim}N_{p\times n}(0,I_{n}\otimes\Sigma)$，而且不难知道$I_{n}-X(X^{\prime}X)^{-1}X^{\prime}$是秩为$n - k$的幂等阵。 由第二章关于随机矩阵二次型的性质5的(1)知 ： $$ Y^{\prime}(I_{n}-X(X^{\prime}X)^{-1}X^{\prime})Y\stackrel{d}{\sim}W_{p}(n - k,\Sigma) $$ 即性质(2)成立。
> 
> **(3) 证明：**又由第二章关于随机矩阵二次型的性质5的(3)知 ： $$ e^{\prime}(I_{n}-X(X^{\prime}X)^{-1}X^{\prime})e与(X^{\prime}X)^{-1}X^{\prime}e独立\\ (X^{\prime}X)^{-1}X^{\prime}Y = B+(X^{\prime}X)^{-1}X^{\prime}e $$ 知$(X^{\prime}X)^{-1}X^{\prime}Y$与$Y^{\prime}(I_{n}-X(X^{\prime}X)^{-1}X^{\prime})Y$独立.

## 情形2: $rank(X) = r < k$

## 性质4.1.1的推论

1.  $(X'X)^- X'Y \stackrel{d}{\sim} N_{k\times p}((X'X)^- X'XB, \Sigma \otimes (X'X)^- X'X(X'X)^-)$;
    +   (1')$ X(X'X)^- X'Y N_{np}(XB, X(X'X)^- X')$;_
    +   (1'') 对$n × s$阶的矩阵C, $L = X'C$, 则 $L'(X'X)^- X'Y \stackrel{d}{\sim} N_{s\times p}(L'B, \Sigma \otimes L'(X'X)^- L)$;
2.  $Y'(I_n - X(X'X)^- X')Y \stackrel{d}{\sim} W_p(n - r, \Sigma)$;
3.  $(X'X)^- X'Y$与$Y'(I_n - X(X'X)^- X')Y$相互独立.

# 4.3 参数估计

参数(B, Σ)的似然函数为(去掉常数) ： $$ L(B, \Sigma|Y) = |\Sigma|^{-n/2} \exp \big\{ -\frac{1}{2} \text{tr} \left$$ Y'(I_n - X(X'X)^{-1}X')Y\Sigma^{-1} \right$$ \\ -\frac{1}{2} \text{tr} \left$$ ((X'X)^{-1}X'Y - B)' (X'X) ((X'X)^{-1}X'Y - B) \Sigma^{-1} \right$$ \big\} $$ 易知B的极大似然估计为 : $$ \hat{B} = (X'X)^{-1}X'Y $$ 注意到平方和分解 :  
$$ (Y - XB)'(Y - XB) = Y'(I_n - X(X'X)^{-1}X')Y\\ + ((X'X)^{-1}X'Y - B)'X'X((X'X)^{-1}X'Y - B)\\\\ (Y - X\hat{B})'(Y - X\hat{B}) = \min (Y - XB)'(Y - XB) $$ 即$\hat{B}$也是$B$的最小二乘估计。

**$\hat{B}$的分布** :

当$\text{rank}(X)=k$时，由性质4.1.1(1)知， $$ \hat{B} = (X'X)^{-1}X'Y \stackrel{d}{\sim} N_{k\times p}(B, \Sigma \otimes (X'X)^{-1}) $$ 即$\hat{B}$是$B$的无偏估计，且$\text{Cov}(\text{vec}(\hat{B})) = \Sigma \otimes (X'X)^{-1}$。

当$\text{rank}(X)<k$时，由性质4.1.1的推论(1'')知， $$ L'\hat{B} = L'(X'X)^{-1}X'Y \stackrel{d}{\sim} N_{s\times p}(L'B, \Sigma \otimes L'(X'X)^{-1}L) $$ 其中$L = X'C$。则$L'\hat{B}$是$L'B$的无偏估计，其协差阵为$\Sigma \otimes L'(X'X)^{-1}L$。

将$\hat{B}$代入似然函数，有: $$ L(\hat{B}, \Sigma|Y) = |\Sigma|^{-n/2} \exp \left\{ -\frac{1}{2} \text{tr} \left$$ Y'(I_n - X(X'X)^{-1}X')Y\Sigma^{-1} \right$$ \right\} $$ 因此，Σ的极大似然估计为 $$ \hat{\Sigma} = \frac{1}{n} Y'(I_n - X(X'X)^{-1}X')Y $$ 再将$\hat{B}$和$\hat{\Sigma}$代入似然函数，有: $$ \max_{B, \Sigma} L(B, \Sigma|Y) = |\hat{\Sigma}|^{-n/2} \exp \left\{ -\frac{n\rho}{2} \right\} = |Y'(I_n - X(X'X)^{-1}X')Y|^{-n/2} \left( \frac{n}{e} \right)^{np/2} $$ 由性质4.1.1的推论(2)知， $$ Y'(I_n - X(X'X)^{-1}X')Y \stackrel{d}{\sim} W_p(n - r, \Sigma)\\ \tilde{\Sigma} = \frac{1}{n - r} Y'(I_n - X(X'X)^{-1}X')Y $$ 易知$E(\tilde{\Sigma})=\Sigma$，即$\tilde{\Sigma}$是$\Sigma$的无偏估计。

由性质4.1.1的推论(3)知，$\tilde{\Sigma}$与$\hat{B}$相互独立。

## 最小二乘基本定理

## 第一基本定理

令$R_{0}^{2}=\min_{B}(Y - XB)'(Y - XB)$，则 $$ R_{0}^{2}\stackrel{d}{\sim}W_{p}(n - r,\Sigma) $$ 其中$\text{rank}(X)=r$。

## 第二基本定理

在$H'B = 0$的约束条件下，令 $$ R_{H}^{2}=\min_{H'B = 0}(Y - XB)'(Y - XB) $$ 其中$H$是$k\times s$的矩阵，$s\leq k$。

那么有：

+   1.  $R_{H}^{2}\stackrel{d}{\sim}W_{p}(n - m,\Sigma)$，其中，$m=\text{rank}(X_{H})$，$X_{H}=X(I_{k}-H(H'H)^{- 1}H')$；  
        
+   2.  $R_{H}^{2}-R_{0}^{2}\stackrel{d}{\sim}W_{p}(r - m,\Sigma)$；
+   3.  $R_{0}^{2}$与$R_{H}^{2}-R_{0}^{2}$相互独立；
+   4.  $\frac{\vert R_{0}^{2}\vert}{\vert R_{H}^{2}\vert}\stackrel{d}{\sim}\Lambda_{p,n - r - m}$。

> **(i)证明**：由广义逆的性质知$H'B = 0$的通解是$B=(I_{k}-H(H'H)^{-1}H')\Theta$，其中$\Theta$是任意的$k\times p$阶矩阵。则在$H'B = 0$的约束下模型转换为 $$ Y = X_{H}\Theta+\varepsilon $$ 其设计矩阵为$X_{H}$，$\text{rank}(X_{H})=m\leq r$。
> 
> 由第一基本定理知： $$ \begin{align} R_{H}^{2}&=\min_{H'B = 0}(Y - XB)'(Y - XB)=\min_{\Theta}(Y - X_{H}\Theta)'(Y - X_{H}\Theta)\\ &=Y'(I_{n}-X_{H}(X_{H}'X_{H})^{-1}X_{H}')Y\\ &\stackrel{d}{\sim}W_{p}(n - m,\Sigma) \end{align} $$ **(ii)-(iv) 证明：**因为： $$ \begin{align} R_{H}^{2}&=\min_{H'B = 0}(Y - XB)'(Y - XB)\geq\min_{B}(Y - XB)'(Y - XB)=R_{0}^{2}\\\\ &\begin{cases} R_{H}^{2}=\varepsilon'(I_{n}-X_{H}(X_{H}'X_{H})^{-1}X_{H}')\varepsilon\\ R_{0}^{2}=\varepsilon'(I_{n}-X(X'X)^{-1}X')\varepsilon\end{cases} \end{align} $$ 由第二章关于随机矩阵二次型的性质5的(2)知: $$ R_{H}^{2}-R_{0}^{2}\stackrel{d}{\sim}W_{p}(r - m,\Sigma) $$ 且$R_{0}^{2}$与$R_{H}^{2}-R_{0}^{2}$相互独立。进而有 : $$ \frac{\vert R_{0}^{2}\vert}{\vert R_{H}^{2}\vert}=\frac{\vert R_{0}^{2}\vert}{\vert R_{0}^{2}+(R_{H}^{2}-R_{0}^{2})\vert}\stackrel{d}{\sim}\Lambda_{p,n - r - m} $$ 即(ii)-(iv)得证。

**特殊情况**

若$\text{rank}(X)=k$，$H$是秩为$s$的$k\times s$阶矩阵，则$X_{H}=X(I_{k}-H(H'H)^{-1}H')$的秩为$m = k - s$。因此有：

+   1.  $R_{H}^{2}\stackrel{d}{\sim}W_{p}(n-(k - s),\Sigma)$；
+   2.  $R_{H}^{2}-R_{0}^{2}\stackrel{d}{\sim}W_{p}(s,\Sigma)$；
+   3.  $R_{0}^{2}$与$R_{H}^{2}-R_{0}^{2}$相互独立；
+   4.  $\frac{\vert R_{0}^{2}\vert}{\vert R_{H}^{2}\vert}\stackrel{d}{\sim}\Lambda_{p,n - k,s}$。

## 第三基本定理

将$Y$和$X$分别剖分为: $$ Y= \begin{pmatrix} \mathbf{Y}_1 \\ \mathbf{Y}_2 \end{pmatrix}, \quad X= \begin{pmatrix} \mathbf{X}_1 \\ \mathbf{X}_2 \end{pmatrix},\quad Y: \begin{pmatrix} m \times p \\ (n - m) \times p \end{pmatrix}, \quad X: \begin{pmatrix} m \times k \\ (n - m) \times k \end{pmatrix} $$ 假设$X_{1}$的秩为$r_{1}$，并令$R_{1}^{2}=\min_{B}(Y_{1}-X_{1}B)'(Y_{1}-X_{1}B)$，则有 $$ \frac{\vert R_{1}^{2}\vert}{\vert R_{0}^{2}\vert} \stackrel{d}{\sim} \Lambda_{p,m - r_{1},n - m - r + r_{1}} $$

> **证明**：由于有  
> $$ \begin{align} R_{0}^{2}&=\min_{B}(Y - XB)'(Y - XB)=Y'(I_{n}-X(X'X)^{-1}X')Y \\ &\stackrel{d}{\sim} W_{p}(n - r,\Sigma)\\ \\ R_{1}^{2}&=\min_{B}(Y_{1}-X_{1}B)'(Y_{1}-X_{1}B)=Y_{1}'(I_{m}-X_{1}(X_{1}'X_{1})^{-1}X_{1}')Y_{1} \\ &\stackrel{d}{\sim} W_{p}(m - r_{1},\Sigma) \end{align} $$ 由于: $$ (Y - XB)'(Y - XB)=(Y_{1}-X_{1}B)'(Y_{1}-X_{1}B)+(Y_{2}-X_{2}B)'(Y_{2}-X_{2}B) $$ 所以$R_{0}^{2}\geq R_{1}^{2}$。又$R_{1}^{2}=Y'AY=\epsilon'A\epsilon$，其中: $$ A=\left(\begin{array}{cc} I_{m}-X_{1}(X_{1}'X_{1})^{-1}X_{1}' & 0 \\ 0 & 0 \end{array}\right) $$ 由随机矩阵二次型的性质知，$R_{0}^{2}-R_{1}^{2} \stackrel{d}{\sim} W_{p}(n - m - r + r_{1},\Sigma)$，且$R_{1}^{2}$与$R_{0}^{2}-R_{1}^{2}$相互独立。进而有 : $$ \frac{\vert R_{1}^{2}\vert}{\vert R_{0}^{2}\vert}=\frac{\vert R_{1}^{2}\vert}{\vert R_{1}^{2}+(R_{0}^{2}-R_{1}^{2})\vert} \stackrel{d}{\sim} \Lambda_{p,m - r_{1},n - m - r + r_{1}} $$

# 4.4 线性假设检验

**检验问题1**  
$$ H_{0}:H'B = 0,\quad v.s.\quad H_{1}:H'B\neq0 $$ 其中$H$是$k\times s$的矩阵。

检验问题的似然比为 : $$ \lambda=\frac{\max_{H'B = 0,\Sigma}L(B,\Sigma|Y)}{\max_{B,\Sigma}L(B,\Sigma|Y)} $$ 由已知 : $$ \max_{B,\Sigma}L(B,\Sigma|Y)=\vert Y'(I_{n}-X(X'X)^{-1}X')Y\vert^{-n/2}\left(\frac{n}{e}\right)^{np/2} $$ 由已知，在约束$H'B = 0$下，多元线性模型$(\*)$转化为: $$ Y = X_{H}\Theta+\epsilon $$ 因此有： $$ \max_{H'B = 0,\Sigma}L(B,\Sigma|Y)=\max_{\Theta,\Sigma}L(\Theta,\Sigma|Y) $$ 其中$L(\Theta,\Sigma|Y)$是多元线性模型$(\*\*)$的似然函数。

同样利用已知，可以推得： $$ \max_{\Theta,\Sigma}L(\Theta,\Sigma|Y)=\vert Y'(I_{n}-X_{H}(X_{H}'X_{H})^{-1}X_{H}')Y\vert^{-n/2}\left(\frac{n}{e}\right)^{np/2} $$ 进而得 ：  
$$ \max_{H'B = 0,\Sigma}L(B,\Sigma|Y)=\vert Y'(I_{n}-X_{H}(X_{H}'X_{H})^{-1}X_{H}')Y\vert^{-n/2}\left(\frac{n}{e}\right)^{np/2} $$

# 4.5 均值子集的线性假设检验

# 4.6 多元线性回归模型

## 4.6.1 参数估计

## 4.6.2 假设检验

# 4.7 变量选择-逐步回归方法

## 4.7.1 预报因子的逐步回归选取方法

## 4.7.2 因变量的逐步回归选取方法

## 4.7.3 其他的变量选择方法

# 4.8 多元线性模型的均值置信域和预测域

## 4.8.1 均值置信域

## 4.8.2 预测域

# 4.9 重复测量模型

## 4.9.2 方差分析

## 作业

线性模型$$Y=XB+e$$, 其中$$X$$列满秩, $B=(\beta_1,\dots,\beta_p)$. 给出下面检验问题的检验方案： $$ H_0:\beta_1=\dots=\beta_p,\quad v.s.\quad H_1:\beta_1,\dots,\beta_p不全相等 $$

**答案：** $$ G=\begin{pmatrix} 1&&&0\\ -1&1&&\\ &\ddots&\ddots&\\ 0&&-1&1 \end{pmatrix}\\ $$
