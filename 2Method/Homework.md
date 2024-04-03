
# Analysis
## Functional Domain 
NCBI: CD-search (conserved domain)
Pfam: search the protein sequence
SMART
Interpro
## Subcellular Locating
TargetP
WoLF PSORT
## Gene Expression, Variation, Disease
GeneCards
GENATLAS
OMIM: Pathogenesis, Allelic Variants
## Phosphopeptide
EPSD
GPS
# Interaction
BioGRID
STRING
HPRD
## Network
Cytoscape
MCODE
## Signal Pathway
KEGG
## Target-Drug relationship
DrugBank
TTD
# Protein Family
直系同源：BLAST
旁系同源
InterPro
## MSA
Clustal Omega
MUSCLE
## Phylogenetic tree
MEGA

# 课堂展示

a quantitatives(数量的) multivariate(多元) model of human dendritic(树状) cell-T helper cell communication

## abstract

dataset generation:

- distinct DC(dendritic cell) conditions – 
- DC communication molecules – 
- CD4 T cells – 
- T helper cytokines

modeling:

- $Y=XB+E$
- $\forall i\in\{1,...,n\},\\\{E_{i,1},...,E_{i,q}\}\sim^{lid}\sim N(0,\sum_q)$
- prediction: DC/T cell molecular associations

validation:

- computional validation:
	- stability selection
	- cross validation
- literature validation:
- systematic experimental validation
- validation of context-depent effects

## 研究方法

1. 往年PPT
2. 论坛
3. 官网
	1. 文献
	2. 算法
4. Wiki
5. 论文

## 概述

cibersort: 一种可以使用基因表达数据来估计混合细胞群中成员细胞类型的丰度分析工具

分工：网页 – R代码 – PPT – pre

### 原理

免疫浸润 – 肿瘤组织内外都有很多免疫细胞 – 判断免疫细胞的组成和比例

- 实测法 – 单细胞测序
- 推测法 – bulk RNA-seq: 使用算法，对复杂的RNA测序表达谱中推断免疫细胞的构成比 – cibersort

基本原理：

- 反卷积 – 冲击响应+输出 – 输入(源信号)
	- 卷积：冲击响应+源信号 – 输出
	- cibersort:
		- 冲击响应 – 参考矩阵：标准单细胞中各类基因的表达量
			- 自变量维度：每个细胞类型
			- 因变量：总表达量
			- 样本点：每个基因
		- 输入 – 加权矩阵：不同细胞亚群水平
		- 输出 – 样本：各类基因组分表达量
- SVR
	- 类比于SVM: 二分类模型 – 分类算法
		- 找到一个超平面能够将数据分类，使其满足到最近的样本点距离最大
	- 实质 – 回归算法(真实值与预测值差距达到最小) – 构建符合样本规律的模型
		- 找到一个超平面，离最远的样本点距离最小 – 回归拟合
		- 样本点：支持向量
- 流程：对样本点采用SVR回归 – 得到 超平面+支持向量参数 – 运算得到样本中最有可能的细胞权重

### 网页实现

1. 准备矩阵
	- 参考矩阵(single cell reference matrix file)：
		- 行：不同基因
		- 列：不同细胞类型，有许多同名列
	- 表达矩阵(Phenotype classes file)
2. 表达矩阵对参考矩阵进行处理 — 签名矩阵
	- signature matrix file — 参考矩阵的处理，签名矩阵的生成
	- 配置：
		- create signature matrix — custom — select input data type: RNA-seq, scDNA-seq, 微阵列
		- 上传矩阵 — 参数配置
			- Kappa：签名矩阵最大条件数，默认为999
			- q-value：错误发现率(FDR)阈值，超过该值的认为显著表达，加入签名矩阵中
			- No. barcode genes：构建签名矩阵时，每种组织/细胞的最小和最大基因数
		- 运行 — 生成签名矩阵
		- 给出签名矩阵热图(可下载txt)
			- 同名列会被合并 — 规范化的签名矩阵
3. 签名矩阵+样本矩阵 — 细胞组分分析结果
	- 样本文件：样本基因表达谱 — 多个样本可以并行分析
		- 列：一个样本
		- 行：不同基因
	- 细胞组分分析：impute cell fractions(签名矩阵和样本的mixture文件) — 运行 — result
	- Result:
		- 行：一个样本
		- 列：一个细胞
		- p-value: 反映所有细胞子集，
		- R: 皮尔森相关系数，将实际的bulk RNA GEP与预测的bulk RNA GEP相比较得出。
		- RMSE: 实际 bulk RNA GEP 与预测的 bulk RNA GEP 的均方根误差
		- $r$：实际值与预测值的皮尔森相关系数
		- $RMSE$：实际值与预测值的均方根误差

CIBERSORTx 工作流涉及多种方法

1. 首先从少量的组织样本中获取不同细胞亚群的基因表达特征
2. 然后该结果系统用于组织样本的细胞丰度和基因表达分析

步骤：

1. 单个细胞或细胞亚群的转录组分析：
	- 获得特定细胞类型的标志基因矩阵，用于区分特定组织类型中特定的细胞子集；
2. 将特征矩阵应用于整个组织的 RNA 表达数据，以推断特定细胞类型的比例；
3. 代表性细胞类型的表达模式；
4. 从多组相关的组织样本中分析每种细胞类型的表达模式

### R代码实现

反卷积算法

- 实际：已知样品各基因表达浓度，又知各细胞类型的表达浓度，从而推测各样品中的细胞丰度 – T = C*P – 已知T和C求P
	- 表达矩阵(expression) – T (gene , sample)
	- 参考矩阵(reference) – C (gene , cell type)
		- 研究免疫浸润的情况下，使用白细胞特征矩阵(LM22)
	- 输出矩阵(result) – P (cell type , sample)
	- 背景噪音 – R
- 内层代码：
	- CoreAlg: SVM分析
	- doPerm: 调用核心函数CoreAlg，实现置换检验 – 产生背景R值
	- Main function: 打包运用到具体例子中

## 代码实现

### CoreAlg

参数传入

```R
#' Core algorithm
#' @param X cell-specific gene expression
#' @param y mixed expression per sample
#' @export
```

细胞特异性基因表达 x – LM22

单个样本的基因表达量 y

返回列表：

- 各种细胞比重(权重向量) w
- 相应模型参数 (RMSE , R)

二维矩阵LM22(m,n) – 将每一行映射到一个n维空间中 – 长度为m的向量

支持向量回归函数: $f(x)=w^Tx+b$

- 回归超平面 – 使靠超平面最远的样本点之间的间隔最小的那个超平面
	- SVR对间隔加以限制：所有的样本点，回归模型预测值与y真实值的偏差必须<=&epsilon;：
		- &epsilon;管道：
			- &epsilon;过小，出现异常点
			- &epsilon;过大，拟合度很差
		- 优化后的SVR不要求包含所有的样本点
			- nu值：不在&epsilon;管道的样本点
- 间隔上边界
- 间隔下边界

代码：

```R
CoreAlg <- function(x,y){
    #1. try different values of nu 调试不同nu值建立三种不同的模型
    svn_itor <- 3

    res <- function(i){
        if(i==1){nus <- 0.25}
        if(i==2){nus <- 0.5}
        if(i==3){nus <- 0.75}
        model<-e1071::svm(x,y,type="nu-regression",kernel="linear",nu=nus,scale=F)
        model
    }
    if(Sys.info()['sysname'] == 'windows') 
        out <- parallel::mclapply(1:svn_itor, res, mc.cores=1) 
    else
        out <- parallel::mclapply(1:svn_itor, res, mc.cores=svn_itor)
    
    #2. do cibersort 对coefs和SV处理得出每种细胞在样本中的比重
    t <- 1
    while(t <= svn_itor){
        weights = t(out[[t]]$coefs) %% out[[t]]$sv #回归直线参数 -- coefs, 确定回归直线的支持向量各个维度值 -- sv
        #此时的参数coefs并不是权重向量，这是由于svm函数会默认使用核函数将所有的输入变量x映射到另一个高维希尔伯特空间中进行后续计算
        #此时参与计算的是希尔伯特特征空间中的向量，因此保存的支持向量是映射到希尔伯特空间中的支持向量，参数coefs是希尔伯特空间中回归直线的斜率向量
        weights[which(weights<0)]<-0
        w<-weights/sum(weights) #对coefs和SV处理，将结果保存在w中
        u <- sweep(x2,MARGIN=2,w,'*')
        k <- apply(u,1,sum)
        nusvm[t] <- sqrt((mean((k-y)^2))) #每个模型预测值和实际值的均方差
        corrv[t] <- cor(k,y) #每个模型预测值和实际值的相关系数
        t <- t+1
    }
    
    #3. pick best model 选取均方根误差RMSE最小的作为最优模型
    rmses <- nusvm
    mn <- which.min(rmses)
    model <- out[[mn]]
    
    #4. get and normalize coefficients 将权重，均方根误差，相关系数保存并输出
    q <- t(model$coefs) %% model$SV
    q[which(q<0)] <- 0
    w <- (q/sum(q))

    mix_rmse <- rmses[mn]
    mix_r <- corrv[mn]

    newList <- list("w" = w, "mix_rmse" = mix_rmse, "mix_r" = mix_r)
}
```

### doPerm

参数传入

```R
#' do permutations
#' @param perm Number of permutations
#' @param X cell-specific gene expression
#' @param y mixed expression per sample
#' @export
```

置换检验，计算p值，产生背景R值

```R
doPerm <- function(perm,X,y){
    itor <-  1
    ylist <- as.list(data.matrix(y))
    dist <- matrix()
#从原来的数据中跟单个样本等长的数据，模拟新样本，进行CoreAlg计算
    while(itor <= perm){
        #print(itor)

        #random mixture sample命令产生模拟样本
        yr <- as.numeric(ylist[sample(length(ylist),dim(x)[1])])

        #standardize mixture  标准化模拟样本
        yr <- (yr - mean(yr))/sd(yr)

        #run CIBERSORT core algorithm
        result <- CoreAlg(X,yr)
        mix_r <- result$mix_r
        
        #store correlation 抽取出相关性系数
        if(itor == 1) {dist <- mix_r}
        else {dist <- rbind(dist,mix_r)}

        itor <- itor+1
    }
    
    #输出R值列表
    newlist <- list("dist" = dist)
}
```

### Main Function

参数传入

```R
#' Main functions
#' @param sig_matrix file path to gene expression from isolated cells
#' @param mixture_file heterogenous mixed expression
#' @param perm Number of permutations doperm中的重复次数
#' @param QN Perform quantile normalization or not (TRUE/FALSE) 要不要进行分数位归一化
#' @export
```

代码：

```R
# 1. 数据预处理
    #read in data 输入数据
    x <- read.table(sig_matrix, header=T, sep="\t", row.names=1, check.names=F)
    y <- read.table(mixture_file, header=T, sep="\t", check.names=F)
    y <- y[!duplicated(y[,1]),]
    rownames(y) <- y[,1]
    y <- y[,-1]
    x <- data.matrix(x)
    y <- data.matrix(y)

    #order matrix row by character order 矩阵按行名字母顺序排序
    x <- x[order(rownames(x)),]
    y <- y[order(rownames(y)),]

    p <- perm #number of permutations

    #anti-log if max < 50 in maxture file 指数运算
    if(max(y) < 50) {y <- 2^y}

    #quantile normalization of mixture file 分位数归一化，先对每个样本中基因表达量进行排序，计算每一个基因在所有样本中的平均值list，把平均值按照原来的基因表达量排序放进去
    if(QN == TRUE){
        tmpc <- colnames(y)
        tmpr <- rownames(y)
        y <- preprocessCore::normalize.quantiles(y)
        colnames(y) <- tmpc
        rownames(y) <- tmpr
    }

    #intersect/filter interesting genes 筛选感兴趣的基因
    xgns <- row.names(x)
    ygns <- row.names(y)
    yintx <- ygns %in% xgns
    y <- y[yintx,]
    xinty <- xgns %in% row.names(y)
    x <- x[xinty,]

    #standardize sig matrix 标准化
    x <- (x-mean(x)) / sd(as.vector(x))

# 2. empirical null distribution of correlation coefficients 求出各个样本的背景相关性系数分布
	if(p > 0) {nulldist <- sort(soPerm(p,x,y)$dist)} #doPerm并保存在nulldist中

# 3. 数据标准化，调用核心函数得到模型参数
    #建立输出变量
	header <- c('Mixture', colnames(x), "P-value", "Correlation", "RMSE")

    output <- matrix()
    itor <- 1
    mixtures <- dim(y)[2]
    pval <- 9999

    #iterate through mixture
    while(itor <= mixtures){
        y <- y[,itor]

        #standardize mixture
        y <- (y - mean(y))/sd(y)

        #run SVR core algorithm
        result <- CoreAlg(x,y)

# 4. 遍历所有样本
        #get results
        w <- result$w
        mix_r <- result$mix_rmse

        #calculate p-value
        if(p > 0) {pval <- 1 - (which.min(abs(nulldist - mix_r))/length(nulldist))}

        #print output 保存到输出变量中
        out <- c(colnames(y)[itor], w, pval, mix_r, mix_rmse)
        if(itor == 1) {output <- out}
        else {output <- rbind(output, out)}

        itor <- itor + 1

    }

## 5. save results 保存结果并输出
	write.table(rbind(header, output), file = "CIBERSORT-Results.txt", sep = "\t", row.names = F, col.names = F, quote = F)

    #return matrix object containing all results
    obj <- rbind(header, output)
    obj <- obj[,-1]
    obj <- obj[-1,]
    obj <- matrix(as.numeric(unlist(obj)), nrow = nrow(obj))
    rownames(obj) <- colnames(y)
    colnames(obj) <- c(colnames(x), "P-value", "Correlation", "RMSE")
    obj
```

## 支持向量机(SVM)

### 线性回归

线性模型：通过属性的线性组合来进行预测的函数，预测实值输出标记

- 一般向量形式$f(\mathbf{x})=\mathbf{w}^T\mathbf{x}+b$
- 最小二乘法 – 试图找到一条直线，使所有样本到直线上的欧氏距离之和最小 – 参数估计

分类任务：找一个单调可微函数，将分类任务的真实标记$y$与线性回归模型的预测值联系起来

- 二分类任务：将产生的预测值实值转为0/1
	- 单位阶跃函数 – 不连续
	- 对数几率函数(logistic function): $y=\frac{1}{1+e^{-z}}$ – Sigmoid函数
	- 变式: $\ln{\frac{y}{1-y}}=\mathbf{w}^T\mathbf{x}+b$
	- 几率：$\frac{y}{1-y}$ – 对数几率
	- 线性判别分析(LDA, Fisher判别) – 将所有的点都投影到回归直线上，使得两类点间隔最大
		- 类间散度矩阵 – $\mu$ – $S_w$ – 奇异值分解   $\mathbf{x}=\frac{\mathbf{x}-\mu}{\sigma}$
		- 类内散度矩阵 – $\Epsilon$(协方差) – $S_b$
		- 广义瑞利商(generalized Rayleigh quotient)
		- 多分类任务 – 全局散度矩阵

### 聚类

分析基因功能：

1. 将样本点都表现为gene表达量的距离点，即距离矩阵，来反映两个基因之间有什么样的距离。
2. 聚类的目的是将不同的基因分到不同的类中，距离是分类的一个依据 – 如何得到距离(距离就反映了所要的表达差距？)

我们是要怎么分类？我们的分类是对不同的表达数据进行分类：

- 变量：
	- 样本
	- gene表达量
	- 细胞类型
- 构建成的特征空间
- $y=2^y$

### SVM

特征空间上间隔最大的线性分类器 – 该线到最近的样本点距离最大 – 二维无法的话，就高维平面

基于训练集$D$ – 样本空间中 – 划分超平面：$\mathbf{w}^T\mathbf{x}+b=0$

- 法向量：$\mathbf{w}$ – 超平面方向

- 位移项：$b$ – 超平面与原点的距离

- 任意点$\mathbf{x}$到超平面$(\mathbf{w},b)$之间的距离：$r=\frac{|\mathbf{w}^T\mathbf{x}+b|}{\|\mathbf{w}\|}$

- 分类结果：
	$$
	\mathbf{w}^T\mathbf{x}_i+b\geq+1,\,\,\mathbf{y_i}=+1;
	\brace
	\mathbf{w}^T\mathbf{x}_i+b\leq-1,\,\,\mathbf{y_i}=-1.
	$$
	
- 支持向量：距离超平面最近的几个训练样本点使式中等号成立

	- 两个异类支持向量到超平面的距离之和为：$\gamma=\frac{2}{\|\mathbf{w}\|}$ – 间隔

	- 最大化分子间隔 – SVM基本型：
		$$
		\min_{\mathbf{w},b}{\frac{\|\mathbf{w}\|^2}{2}}
		\\
		s.t. \,y_i(\mathbf{w}^T\mathbf{x}_i+b)\geq1,\,i=1,2,...,m.
		$$

- 对偶问题：在求解上式获得大间隔划分超平面模型时，对凸二次规划问题求解 – 现成计算包

	- 使用 拉格朗日乘子 $\alpha_i\geq0$
		- 拉格朗日函数 – 求偏导并另偏导为0 – 对偶问题
		- 解出的拉格朗日乘子 – 训练样本$(\mathbf{x}_i,y_i)$ – 要满足KKT条件
		- 训练后，大部分样本不需保留，最终模型只与支持向量有关
	- SMO算法：固定其他参数，仅优化两个参数 – 高效

核函数：从原始空间映射到一个更高维的特征空间，使得样本在特征空间线性可分

- 理论：如果原始空间是有限维(属性有限)，一定存在高维特征空间使样本可分
- 特征向量：$\phi(\mathbf{x})$
- 对偶问题 – 内积：$\phi(\mathbf{x})^T\phi(\mathbf{x})$ – 难以计算
	- 核技巧/核函数：$\kappa(\mathbf{x_i},\mathbf{x_j})=\langle\phi(\mathbf{x_i}),\phi(\mathbf{x_j})\rangle=\phi(\mathbf{x})^T\phi(\mathbf{x})$ – 不必去计算高维，甚至无穷维特征空间中的内积 – 支持向量展式
		- 核矩阵$\mathbf{K}$总是半正定的 – 只要一个对称函数对应的核矩阵半正定，就能作为核函数使用 – 特征空间的好坏对支持向量机很重要
		- 常用核函数：

软间隔：允许某些样本不满足约束

正则化(regularization)：结构风险 – 经验风险 – 经验风险最小化

### SVR

所有样本点到这个超平面的距离最小，为得到一个  $f(\mathbf{x})=\mathbf{w}^T\mathbf{x}_i+b$  回归模型，使$f(x)$与$y$尽可能接近

- 假设我们能够容忍预测值与真实输出之间有$\epsilon$的偏差，且仅当差别绝对值大于$\epsilon$时才计算
- 考虑特征映射形式以及对偶问题，SVR公式可表示为：$f(\mathbf{x})=\sum_{i=1}^m(\widehat{\alpha}_i-\alpha_i)\kappa(\mathbf{x},\mathbf{x}_i)+b$

## CIBERSORTx

### 理论

反卷积：

SVR：

1. 自变量维度：签名矩阵的每个细胞类型
2. 因变量：每个样本的总表达量
3. 样本点：每个基因

### 算法



## CIBERSORT

### presentation

produceType_avgFiles.R

```
function: typeAvgFiles()

#read the signature matrix file and put each cell type values in a separate file. 
从签名矩阵中，根据细胞类型分类成单个文件
#Then, it calculaes the average value (between samples) for each cell type and return each in a separate file.


```

calculateAdjPval.R

```
function: pvalCalculation()

#read the separated file for each cell type, number of probes x number of samples, 
and calculate the pairwise adjusted p-value between cell types and return the ones for each cell type 
in a separate file (PvalB, PvalG, ...)
```

calculateEffectSize.R

```
function: effectSize()

#read the files with the average values for each cell types, and return the effect size matrixes for them
```

produceSigMat

```
function: makeSigMat

#read the Pvalue, effectSize and average value files.

#check the threshold for Pvalues and effect size apirwise between cell types for each probe

#every probe which passes both threshold will be save in signature matrix with its average (between samples)
values (between samples)
```

Merge_Mix_SigMat.R

```
# extract the signature matrix probes and their values from mixture Matrix 
(example: LM22, merge ExampleMixtures-GEPs ), to be used for modeling
```

svr.R

```
# Read the signature matrix and the mixture data (for the probes from signature matrix), 
and build the model using e1071 package.

(scale = F, type = "nu-regression")
```

nnlm.R

```
# Read the signature matrix and the mixture data (for the probes from signature matrix), 
and build the model using nnls package.
```

comPlotType

```
# reads the observed data and the predicted data from a single file (format important) amd 
make the scatterplot of predicted versus observed for each cell type.
```

 

 ## 展示

1. CIBERSORTx开发自CIBERSORT。
2. CIBERSORT算法在**反卷积算法的运用于细胞推断**这一领域具有重要的意义，它运用支持向量回归(SVR)得到回归模型：$f(\mathbf{x})=\mathbf{w}^T\mathbf{x}_i+b$，我们引用2015年发布的CIBERSORT的R包(v1.03)，
	1. **CIBERSORT**
		1. 利用自带signature文件**LM22** –基本准确，但会忽略一些特殊表型
	2. **CIBERSORTx**
		1. 通过**单细胞****RNA-seq(scRNA-seq)数据**构建**专属signature
		2. 各免疫细胞marker基因
		3. 能够推测**各免疫细胞特征基因表达谱**
		4. **单细胞参考表达矩阵**（Single cell reference matrix file）（行名为基因名，列名为细胞名；用途：制作标签矩阵Signature matrix file）
		5. **标签矩阵**（Signature matrix file）（行名为基因名（更少），列名为细胞名（归纳好），用途：为混池矩阵（Mixture file)服务，相当于LM22）
		6. **混池矩阵**（Mixture file）（你需要计算免疫细胞比例的bulk测序，行名为基因名，列名为样本名，就是普通的表达矩阵）