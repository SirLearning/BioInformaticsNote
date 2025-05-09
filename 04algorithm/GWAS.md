
GWAS是对基因型和表型之间的关联分析，实际上还是统计方法，采用的是混合线性模型。

# 混合线性模型

本文档主要对混合线性模型的数学基础进行说明。

对于混合线性模型，我现在有以下几个问题：
- 线性模型计算时的**最小二乘法**在这里运用的是否为我们常用的模式？所谓的最小一乘法是什么？
- 为何线性模型混合之后就可以很好地解释？难道各变量之间都是靠线性的方式来加和的吗？

# 特殊的GWAS

ANCHOR：将特定基因组区段根据不同 ancestry component 来进行的GWAS
- 其R代码已经开源：[MyersGroup/ANCHOR: An statistical approach leveraging segments of distinct ancestries within individuals to estimate similarity in underlying causal effect sizes between groups, using an existing PGS](https://github.com/MyersGroup/ANCHOR)

