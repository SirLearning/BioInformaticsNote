# 基础知识
## 软件安装
三类程序：
 - 二进制可执行程序：下载软件包解压后可全路径调用
	 - sratoolkit和ncbi的blast软件
 - 语言代码
	 - C源码：./configure,make,make install
	 - python：模块依赖的问题，建议直接用conda
 - 系统/语言自带软件中心安装器：apt-get，yum，cpan，cran，brew, pip,conda，docker
	 - pip：pip install --index-url https://pypi.douban.com/simple cnvkit deeptools HTSeq 
	 - conda：也需要设置镜像加速
		 - 安装：
			 - wget https://repo.continuum.io/miniconda/Miniconda2-latest-Linux-x86_64.sh
			 - sh Miniconda2-latest-Linux-x86_64.sh
		 - 安装之后运行source激活conda，或者直接添加到环境变量，然后 source  ~/.bashrc 激活环境变量
		 - conda安装软件管理：
			 - conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free
			 - conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/conda-forge
			 - conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/bioconda
			 - conda config --set show_channel_urls yes
			 - conda config --show
			 - conda install -y -c bioconda homer
			 - conda install -y -c bioconda 等任何软件，安装之前先搜索了解软件本身
必装软件
 - 质量控制工具：fastqc, fastx_toolkit，cutadapt，TrimGalore，RSeQC或者RNA-SeQC,qualimap,skewer，NGScheckmate
 - 比对工具： bwa,bowtie2,hisat2,subjunc,STAR 
 - 找变异：GATK, Platypus, VarScan, LoFreq,FreeBayes, SNVer, SAMtools, VarDict,cnvkit,sequenza
 - 包括计数的： bedtools, htseq-counts, FeatureCounts , salmon
 - 差异分析的R包：limma, DEseq2,edgeR
 - 其它：deeptools
## 实验技术
生物芯片：分类，原理，历史
 - 主要的芯片平台
	 - 按照公司来区分：affymetrix，agilent和illumina，罗氏
	 - 按照应用来区分，表达芯片，基因分型芯片，拷贝数芯片
	 - 其它定制化芯片
测序技术：分类，原理，历史
 - 主要的测序平台： Illumina、SOLID、Roche 454、lon Torrent、Pacific Biosciences、纳米孔技术
## 数据存储
国际数据中心：NCBI, ENSEMBL, UCSC 
数据格式：fastq, fasta, sam, bam, vcf, gff, gtf, bed, MAF
参考基因组、基因组注释：
 - 人体基因：数量，分类，基因结构
 - genecard
 - TCGA
 - ENCODE
 - GTEx
 - 基因集注释数据库：GO terms/Pathway (KEGG, BIOCARTA,Reactome)  MSigDB
高级分析： WGCNA  , COX回归等生存分析 ，LASSO回归等机器学习
# RNA-seq数据分析

  - 基因表达的量化和比较

    - 普通分析，就是差异基因，GO/KEGG等数据库注释，PPI网络

    - 高级分析，包括WGCNA,GSEA,时序分析，RNA编辑，依赖于课题设计实际情况

  - 表达数量性状基因座

  - 单细胞RNA-seq

  - 融合基因

  - 基因变异

  - 长的非编码RNA

  - 非编码小RNA

- 了解RNA-seq项目设计的一般原则

  参考 2016的：RNA-seq数据分析指南 https://mp.weixin.qq.com/s/JMKBVxwDwXUcDSaMDdujYg 

  - 推荐100~200M的PE75以上的reads，重复大于6，经费紧张的话3个也行

  - 根据测序策略及各个分组是否有重复来实战

    - SE50 无重复

    - PE150 有重复

    - 等其它

- 了解一些实战导读

  - https://f1000research.com/articles/4-1070/v1 

  - https://f1000research.com/articles/5-1438/v1 

  - https://www.bioconductor.org/help/workflows/rnaseqGene/ 

  - 一个RNA-seq实战-超级简单-2小时搞定！http://www.bio-info-trainee.com/2218.html 

  - 一个植物转录组项目的实战 http://www.bio-info-trainee.com/2809.html

- 目前主流是表观调控和多组学

  这个大家查看我的生物信息学文献阅读笔记

  - 多组学通常就是DNA和RNA一起测序的项目

    - 比如 2016台湾发表的OSCC数据

    - 2018的TNBC的小鼠模型的数据

    - PNAS在线发表MS1的图位克隆工作，在克隆Ms1的过程中，有使用RNAseq和DNAseq。原始测序数据存放在NCBI上，编号为SRP113349 

  - RNA-seq和ChIP-seq组合（后续单独视频课程讲解）

  - RNA-seq和ATAC-seq组合

- 数据处理的流程

  主要代码都是在：https://www.jianshu.com/p/a84cd44bac67  原创10000+生信教程大神给你的RNA实战视频演练 

  - 数据资源下载，参考基因组及参考转录组，基因注释文件

  - 质控，需要fastqc及multiqc，trim-galore
    - 或者很多其它软件 trimmomatic, cutadapt, qualimap等等

  - 比对
    - 很多软件：star, hisat2,bowtie2,tophat,bwa,subread，优先选择STAR或者hisat2

  - 计数
    - 软件也很多：featureCounts,htseq, bedtools ,deeptools salmon ，优先选择featureCounts

  - normalization 归一化（统计学+数学知识背景）

    - Total Count (TC)

    - Upper Quartile (UQ)

    - Median (Med)

    - the DESeq normalization implemented in the DESeq Bioconductor package

    - Trimmed Mean of M values (TMM) implemented in the edgeR Bioconductor package

    - Quantile (Q)

    - the Reads Per Kilobase per Million mapped reads (RPKM) normalization, FPKM,TPM

  - 差异分析等

    - 主要是导入R里面使用R包DEseq2或者edgeR分析，也可以选择limma的voom算法

    - 可以参考我GitHub的示例：https://github.com/jmzeng1314/GEO/tree/master/airway_RNAseq 

- 比较salmon等无比对流程的转录本定量

  - 注意salmon等无比对流程不一定可靠，至少不是金标准，谨慎使用哈

- 植物转录组实战演练

  - 一个植物转录组项目的实战 http://www.bio-info-trainee.com/2809.html
    - 主要的难点在于ID转换，以及后续对感兴趣的基因集进行功能数据库注释

  - 如果是无参考基因组的RNA-seq，会更加麻烦，涉及到转录本组装，功能定义

- 其它应用方向如何自学

  - circRNA数据分析流程

    - circRNA科普

      - 相比于普通RNA（链状RNA），circRNA不具有5' 末端帽子和3' 末端poly(A)尾巴，它以共价键连接首尾，形成封闭环状结构。

      - 这一结构使它不易被核酸外切酶RNaseR降解，故而比RNA更加稳定。

      - 目前认为，circRNA是由前体RNA（pre-mRNA）通过反向剪接反应（back-splicing）这一特殊的选择性剪接产生的。

      - circRNA多数源于外显子（exon），少部分由内含子（intron）直接环化形成，一般来说circRNA具有高度的保守性。

    - 先看文章及综述，比如：

      - 综述

        - Biogenesis of Circular RNAs （Cell, September 25, 2014）
          - 解circRNA的产生机制

        - The biogenesis and emerging roles of circular RNAs.（Nat Rev Mol Cell Biol, 2016 Apr）
          - 介绍了circRNA的生成机制以及在真核生物转录组中的作用机制。

        - Detecting circular RNAs: bioinformatic and experimental challenges （Nat Rev Genet. 2016 Oct 14） 
          - 检测circRNA的过程中可能会遇到哪些问题，以及如何处理。

      - 文章：Novel Role of FBXW7 Circular RNA in Repressing Glioma Tumorigenesis  https://doi.org/10.1093/jnci/djx166 

        - 主要材料与方法

          - 样本
            - 10个病理诊断的胶质母细胞瘤样本及其配对的邻近正常脑组织。

          - 实验验证方法
            - Northern blotting, Sanger sequencing, antibody, and liquid chromatograph Tandem Mass Spectrometer；Lentivirus-transfected and qPCR.

          - 数据来源
            - 去核糖体RNA测序，Illumina Hiseq 2500；

          - 程序及参数
            - Bowtie2；TopHat2： 20 mers；find_circ：at least two unique back-spliced reads in one sample；

        - 结果

          - 通过测序数据总共鉴定到31145条circRNA，其中6442能够匹配到circBase数据库，并使用RefSeq数据库进行功能注释。

          - 作者将差异基因分析最显著的候选者匹配到circRNADb数据库，找到一条来源于FBXW7基因外显子3和外显子4环化的novel_circ_022705。

          - 确认对象后，作者首先鉴定预测的序列为一条差异表达的circRNA，方法如下：

            - PCR结合RNase-R及Sanger sequencing；

            - q-PCR；

            - Northern blotting using a junction-specific probe；

            - 结合siRNA的FISH analysis确定了其亚细胞定位；

        - Circ-FBXW7的翻译能力评估

          - 在circRNADb预测信息显示，其包含185aa蛋白其高度保守的ORF，作者首先通过双荧光素酶载体系统验证其是否存在IRES来启动翻译。

          - 结果显示，circ-FBXW7 IRES能够促进5‘-cap 依赖的翻译途径。为了验证在人类细胞中circ-FBXW7的翻译，作者移动 (move) 接头及ORF的终止密码子将FLAG序列添加到两边，阴性对照删除下游侧翼序列 (linear-FL-FBXW7-AG). 

          - 在293T细胞中，对照发现FLAG标签抗体仅在circ-FBXW7-FLAG-和FBXW7-FLAG染色细胞中检测到约22kDa 蛋白，表明circ-FBXW7-FLAG载体被翻译；而通过“FBXW7-185aa” 抗体反应发现，在空白对照及线性FL-FBXW7Ag转染细胞中检测内源性FBXW7185aa，且circ-FBXW7-FLAG-和FBXW7-FLAG染色细胞中过表达。随后使用液相分析其氨基酸序列，发现其由 “spanning junction ORF”组成，进一步说明了该蛋白由circ-FBXW7编码。

        - 参考：https://vip.biotrainee.com/d/772-circ

    - circRNA数据分析一般流程

  - miRNA数据分析流程

    - 先看文章及综述，比如：

      - 第一篇：Diagnosticand prognostic implications of microRNA prfiling in prostate carcinoma发表于2010年[1]，影响因子：2017：7.36

        - 研究对象是人体组织，即前列腺癌（prostate carcinoma），实验手段是miRNA芯片测序，外加RT-qPCR验证，研究的是miRNA作为疾病诊断指标的可行性。文章书写结构如下所示：

          - 实验材料与方法：患者与组织样本

          - RNA提取：

          - MiRNA芯片测序

          - MiRNA的RT-qPCR验证，验证采用Taqman法。

          - 处理数据

          - 结果（Results）与讨论。

        - 评论：如果有患者样本，测序还是很快的。

      - 第二篇：Deepsequencing reveals differential expression of microRNAs in favorable versusunfavorable neuroblastoma[2]发表于2010年，影响因子10

        - 主要内容是NGS测序neuroblastoma的miRNA，数据分析。文章结构如下：

          - Introduction

          - Materials and methods

            - a)      Sample preparation and RNAisolation

            - b)     Small RNA library generationand sequencing

            - c)      Sequence processing and mapping

            - d)     Normalization of read counts

            - e)      MiRNA RT-qPCR

            - f)       Statistical testing and clusteranalysis

          - RESULTS

          - Discusstion

      - 第三篇：MicroRNAexpressions associated with eosinophilic meningitis caused by Angiostrongyluscantonensis infection in a mouse model[3]发表于2014年，影响因子2.4

        - 小鼠组织miRNA测序，数据分析，RT-qPCR验证，文章结构如下所示：

          - Introduction

          - Methods

            - 样本制备（动物）

            - 构建小RNA文库以及测序Construction of small RNA libraries and deep sequencing

            - 差异miRNA分析

            - 差异miRNA的靶基因富集

            - 功能验证

      - 第四篇：Integratedanalysis of microRNA and mRNA expression profiles in abdominal adipose tissuesin chickens[4]
        - 时间：2015，期刊：SC
          - 鸡腹部脂肪组织，miRNA测序，mRNA-seq，miRNA阈值取为fold-change> 1.5 or < 0.67

      - 第五篇：The porcine microRNA transcriptomeresponse to transmissible gastroenteritis virus infection

        - 时间：2015，Plos one[5]

        - 方法：样本，测序，数据分析

      - 第六篇：MicroRNA profiling of the bovinealveolar macrophage response to Mycobacterium bovis infection suggests pathogensurvival is enhanced by microRNA regulation of endocytosis and lysosometrafficking

        - 时间：2015期刊：Tuberculosis，影响因子：2.8

        - 方法；肺泡巨噬细胞感染结核杆菌，miRNA测序，RT-qPCR验证，溶酶体转运，细胞系过表达，靶基因验证。测序+功能验证。

      - 第七篇：Differential microRNA expressionprofiling of mesothelioma and expression analysis of miR-1 and miR-214 inmesothelioma

        - 时间：2016年，影响因子：2.6

        - 细胞株的miRNA表达谱，用RT-qPCR验证了几个miRNA，用双荧光素酶和WB验证了miRNA的靶基因。

      - 第八篇：Wu, C.X., et al. (2017). "Microrna Expression Profiling of Macrophage Line Raw264.7 Infected by Candida Albicans." Shock 47(4): 520-530.
        - 发表于2017年，影响因子3.0。主要思路就是白念珠菌感染RAW264.7细胞，测miRNA的表达谱，用RT-qPCR进行验证，再用miRNA mimics与inhibitor进行功能验证，最后用WB来对靶基因进行验证。

    - miRNA数据分析一般流程
      - 

    - TCGA数据库的miRNA-seq表达矩阵下游分析
      - 参考 学徒带你7步3251行代码+300行注释完成TCGA数据库挖掘实战全文复现：https://cloud.tencent.com/developer/article/1605620

  - lncRNA-seq数据分析流程

  - 全转录组数据分析流程

  - 全长转录组数据分析流程

  - 单细胞转录组分析流程

- 为什么说这样的课程意义不大

  - 1-课程介绍

  - 2-开启WSL

  - 3-颜值也是生产力

  - 4-基本设置

  - 5-安装bioconda

  - 6-安装常用生物软件

  - 7-RNAseq分析案例

  - 8-下载数据

  - 9-hisat比对与stringTie重构转录本

  - 10-ballgown差异表达分析及可视化

- 下游分析

  - PPI网络细节
    - https://w.url.cn/s/APtoCmt

  - 其它高级分析

- 可视化

  - IGV等浏览器

  - ggplot2+ggpubr包

# WES数据分析

- 在学徒配备的Linux服务器里面安装软件（越多越好）

  - 前提是听完了Linux基础和软件安装课程

  - 参考 生物信息学常见1000个软件的安装代码！ http://www.biotrainee.com/thread-856-1-1.html

  - 软件安装在我看来分成3类：

    - 第一就是二进制可执行程序，直接下载软件包解压后就可以全路径调用啦！
      - 常见的有sratoolkit和ncbi的blast软件，进入下载链接可以看到同一款软件有针对多个不同系统的下载文件，非常齐全。
        - 需要仔细搜索找到下载链接，比如 ftp://[ftp.ncbi.nlm.nih.gov/blast/executables/blast+/LATEST/](http://ftp.ncbi.nlm.nih.gov/blast/executables/blast+/LATEST/) 

    - 第二就是所有的语言代码啦，比如perl,R,python,java,matlab,ruby,C等等

      - 其中C源码就是./configure,make,make install，也有的就是make，取决于readme，这个也是报错最多的，一般就是没有权限，缺库，很头疼。

      - 然后perl和python软件呢，主要就是模块依赖的问题，实在解决不了的问题，建议直接用conda

      - R包，java软件非常简单了。

      - matlab软件，你要是在windows界面用到还好，想去linux用，也折腾好几个星期。

      - ruby其它我没有用过啦。

    - 最后就是系统或者语言自带的各种软件中心安装器啦，apt-get，yum，cpan，cran，brew, pip,conda，docker 等等

      - pip安装需要设置镜像加速：pip install --index-url https://pypi.douban.com/simple cnvkit deeptools HTSeq 

      - conda 特别好用，值得用心学，也需要设置镜像加速

        - wget https://repo.continuum.io/miniconda/Miniconda2-latest-Linux-x86_64.sh

        - sh Miniconda2-latest-Linux-x86_64.sh

        - 上面的代码就可以安装conda了，安装过程需要选择几个yes，安装之后运行source激活conda即可。

        - 或者直接添加到环境变量，然后 source  ~/.bashrc 激活环境变量

        - 如果有了conda，以后安装软件就可以用它管理

          - conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free

          - conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/conda-forge

          - conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/bioconda

          - conda config --set show_channel_urls yes

          - conda config --show

          - conda install -y -c bioconda homer

          - conda install -y -c bioconda 等任何软件，安装之前先搜索了解软件本身。

        - conda就可以学习很久

      - 都可以通过设置镜像来加速

  - 仔细体会网页版工具和命令行版本的区别，比如 blast和blat工具，学会如何学习新的软件的操作
    - 一定要阅读：https://mp.weixin.qq.com/s/oQgFcDaKrh5qwOEglnCwwA 

  - 必装软件

    - 质量控制工具：fastqc, fastx_toolkit，cutadapt，TrimGalore，RSeQC或者RNA-SeQC,qualimap,skewer，NGScheckmate
      - 参考：生信技能树»生信技能树›生信基础›测序原理-数据格式-数据库›要充分了解你的测序数据--论QC的重要性  http://www.biotrainee.com/thread-324-1-1.html 

    - 比对工具： bwa,bowtie2,hisat2,subjunc,STAR 

    - 包括找变异的：GATK, Platypus, VarScan, LoFreq,FreeBayes, SNVer, SAMtools, VarDict,cnvkit,sequenza

      - 参考资料：

        - 找SNV(SNP)工具大比拼

          - 文章地址：https://www.ncbi.nlm.nih.gov/pubmed/29945233

          - 脚本地址：https://imigitlab.uni-muenster.de/published/appreci8/tree/master/Scripte

        - 

    - 包括计数的： bedtools, htseq-counts, FeatureCounts , salmon 等

    - 差异分析的R包：limma, DEseq2,edgeR
      - 参考资料，文章： https://www.ncbi.nlm.nih.gov/pubmed/24813215

    - 其它工具：deeptools等

  - 要求

    - 分门别类总结，软件涉及到的生物信息学数据格式，要求的input，得到的output，开发语言

    - 每个软件都需要自己总结md的使用文档

    - 录制至少3个软件使用小视频
- 生信基础知识掌握（终身学习）

  - 生物芯片和测序技术的分类，原理及历史，需要自行查找归纳总结

    - 主要的测序平台

      - 1.5.1 Illumina

      - 1.5.2 SOLID

      - 1.5.3 Roche 454

      - 1.5.4 lon Torrent

      - 1.5.5 Pacific Biosciences

      - 1.5.6 纳米孔技术

    - 主要的芯片平台

      - 按照公司来区分：affymetrix，agilent和illumina，还有罗氏

      - 按照应用来区分，表达芯片，基因分型芯片，拷贝数芯片

      - 其它定制化芯片

  - 3大国际数据中心的了解，NCBI,ENSEMBL,UCSC 

    - 了解每个数据中心的子数据库单元

    - 了解数据上传的4个地方，NCBI的GEO和SRA, EBI的ENA和arrayexpress

      - https://www.ebi.ac.uk/ena

      - https://www.ebi.ac.uk/arrayexpress/

      - https://www.ncbi.nlm.nih.gov/geo/

      - https://www.ncbi.nlm.nih.gov/sra 

  - 数据格式的整理和熟记，包括fastq,fasta,sam,bam,vcf,gff,gtf,bed,MAF~~
    - 参考：http://www.biotrainee.com/thread-42-1-1.html

  - 参考基因组的熟悉及其基因组注释新文件下载及摸索

  - 从基因开始理解生物信息学

    - 人体基因数量，分类，基因结构等等

    - genecard 数据库

    - 熟记部分基因
      - GF生长因子及其受体家族系列

  - 组学技术应用的第一篇文章以及最新综述文章收集整理

  - 各个组学数据分析的结题报告的阅读及整理

  - 数据库的收集整理，包括 

    - 遗传变异资源

      - 参考： http://snpeff.sourceforge.net/download.html

      - http://annovar.openbioinformatics.org/en/latest/user-guide/download/ 

      - https://asia.ensembl.org/info/docs/tools/vep/script/vep_cache.html

    - TCGA

    - ENCODE

    - GTEx

    - 基因集注释数据库：GO terms/Pathway (KEGG, BIOCARTA,Reactome)  MSigDB，主要理解基因集的定义
- 练习GEO数据库的表达芯片数据处理

  - 列表1：

    - GSE63067

    - GE37031

    - GSE20950

    - GSE26339

    - GSE15773

    - GSE30122

    - GSE23343

    - GSE21785

    - GSE1009

    - GSE15653

    - GSE25724

    - GSE20966

  - 列表2

    - GSE21933

    - GSE33532

    - GSE44077

    - GSE74706

    - GSE25097

    - GSE45267

    - GSE57957

    - GSE62232

    - GSE110147

    - GSE24206

    - GSE49072

    - GSE90713

    - GSE75415

    - GSE19750

    - GSE14922

    - GSE12368

    - GSE16515

    - GSE28735

    - GSE15471

    - GSE18670

    - GSE41368

    - GSE20966

    - GSE25724

    - GSE38642

    - GSE8569

    - GSE21933

    - GSE33479

    - GSE33532

    - GSE40275

    - GSE62113

    - GSE74706

    - GSE18842

    - GSE19804

    - GSE43458

    - GSE62113

    - GSE6222

    - GSE41804

    - GSE51401

  - 高级分析了解一下： WGCNA  , COX回归等生存分析 ，LASSO回归等机器学习

  - 参考：我在2016的总结帖：http://www.bio-info-trainee.com/2087.html  

  - 要求：至少完成3个以上的GSE数据分析及rmarkdown的报告！

  - 作业：

    - Figure 1: TRAF4-mediated ubiquitination of NGF receptor TrkA regulates prostate cancer metastasis

    - 这个paper里面的：https://www.jci.org/articles/view/96060/figure/1  复现

# ChIp-seq数据分析

- 生物信息学背景知识

  - 需要掌握linux系统基础操作，以及R语言

    - 生信分析人员如何系统入门R(2019更新版) https://mp.weixin.qq.com/s/xOT4QGQsBMwu6R38AE9Y6A

    - 生信分析人员如何系统入门Linux(2019更新版) https://mp.weixin.qq.com/s/2RqjIWEARgMmk3h_sAYtUw

  - 生信工程师入门最佳指南(附赠长达74小时的视频指导) 
    - https://mp.weixin.qq.com/s/o_tmsXCYEvA4-J_8MS7HEw

  - 生信基础

    - 山东大学 生物信息学https://www.bilibili.com/video/av22086086

    - 生物信息学：导论与方法(北京大学) http://bilibili.com/video/av10042290

    - 争取掌握生信基础100讲：https://mp.weixin.qq.com/s/Gr_0H4-GaTYkgUkbNHcMcg

- 表观组学的背景知识

  - 2016年Nature Methods年度技术：表观转录组分析（Epitranscriptome analysis）

    - http://www.nature.com/nmeth/focus/moy2016/index.html

    - DNA/RNA/protein 都是可以被修饰的

    - NGS与转录：https://hwoihann.github.io/farnorth/definition/2017/09/29/basicNGS-centralDogma-transcription.html 

    - 示例文献：用肿瘤组织做ChIP-seq、ATAC-seq + RNA-seq + DNA羟甲基化 

      - https://genome.cshlp.org/content/early/2017/10/05/gr.222794.117 

      - 自产数据：11个RNA-seq，2个ATAC-seq，以及2个hmc ChIP-seq，即hmC-seal，再结合ENCODE已经产生了胰腺癌的组蛋白修饰数据。

  - 我对表观的18个疑问,  http://www.biotrainee.com/thread-845-1-1.html 

  - 2016 年 8 月清华大学颉伟研究员在复旦大学「表观基因组学暑期国际讲习班」中的报告 
    - https://mp.weixin.qq.com/s/yxwGQYMW172QKpGxAEf05g

  - 其它生物学背景知识支持（需要追踪最新文献）

- ChIP-seq测序建库技术背景知识

  - 各种测序建库技术

    - ChIP-Seq，蛋白质修饰

    - MeDIP-Seq，DNA修饰

    - WGBS，DNA修饰

    - ATAC-seq

    - MBD-Seq

    - RNA甲基化免疫共沉淀技术（MeRIP)

    - 氧化-重亚硫酸盐测序（oxBS-Seq) 

    - TET辅助重亚硫酸盐测序（TAB-Seq）

    - m6A-Seq

    - RRBS(Reduced Representation Bisulfite Sequencing) 是WGBS的简化版

  - 什么是ChIP-seq测序建库技术

    - ChIP即染色质免疫共沉淀技术(Chromatinimmunopre-cipitation, ChIP)，它是在生理状态下, 利用甲醛将细胞内的DNA与蛋白质交联(Crosslink)，从而形成复合物，然后经细胞裂解、细胞核收集和裂解, 分离染色体, 通过超声或酶处理将染色质随机切割, 再通过抗原抗体的特异性识别反应沉淀此复合体，从而特异性地富集目的蛋白结合的DNA片段，通过对目的片断的纯化与检测，从而获得与该蛋白结合的DNA的信息。

    - ChIP-seq是将染色质免疫共沉淀与二代高通量测序相结合的技术，它将ChIP获得的DNA片段进行高通量测序，捕捉到细胞内动态的、瞬时的蛋白质与DNA之间的相互结合作用，一次性获取与目的蛋白相结合的DNA序列、确定蛋白的结合分布和精确的结合位点以及结合基序等大量信息。

    - ChIP-seq的应用主要包括两个方面：

      - 一方面是DNA序列上转录因子结合位点(Binding sites)的识别, 如启动子、增强子等各种顺式作用元件(Cis-actingelement)的识别;

      - 另一方面主要应用在表观遗传学领域, 包括研究基因组DNA甲基化、组蛋白修饰和核小体定位等。

    - 若ChIP-seq同时结合转录组测序，则可以帮助得到目的蛋白对全细胞基因表达的调控模式，大幅提高对目的蛋白的功能认识。这种在 DNA－蛋白质相互作用研究方法上的重大突破，极大的推进了基因表达调控（转录因子）与表观遗传学（组蛋白修饰）的发展。

  - ChIP-seq实验环节

    - 知识点很多，建议翻译：https://www.takarabio.com/learning-centers/next-generation-sequencing/faqs-and-tips/chip-seq-faqs 内容，配套PPT图文并茂的讲解更容易看懂。

    - 1）将活体细胞交联，将细胞核内的染色质分离出来，并用超声波打断成小片段（通常0.2-1kb），

    - 2）用所研究的蛋白特异性抗体将目的蛋白及其结合的DNA片段免疫共沉淀下来，

    - 3）将蛋白质-DNA复合物解交联并纯化DNA片段，

    - 4）在DNA片段两端加测序接头构建DNA测序文库。

  - ChIP-seq实验细节注意

    - 参考文献：Keji Zhao, etal,ChIP-Seq: Technical Considerations for Obtaining High Quality Data.NatImmunol . ; 12(10): 918–922. doi:10.1038/ni.2117. https://www.ncbi.nlm.nih.gov/pubmed/21934668 

    - 1.怎么判断抗体满足ChIP要求？
      - 通常每个公司的抗体说明都标有级别（grade），ChIP级。如果没有，通常的规则是ChIP-PCR分析阳性control是阴性control的5倍以上的抗体认为是到达了ChIP级。

    - 2.如果没有商业化的kit怎么办？
      - 表达的表位标记的蛋白也可以。最经常使用的标签包括HA，Flag，Myc和V5。除了表位的抗体，所述靶蛋白也可以标记有生物素受体序列，其可以与生物素经由生物素连接酶在体内或体外进行标记。

    - 3.多少细胞数合适？
      - 10^6到10^7个细胞才能保证最终得到10到100ng ChIPed DNA。一般10^6可以满足高丰度蛋白（如RNA polymerase II）和局部组蛋白修饰（如H3K4me3）的ChIP。如果是低丰度的转录因子蛋白和其他组蛋白修饰则需要10^7个细胞。

    - 4.用什么作为Control？

      - 关于control是问得最多，也是最困惑的一个问题。

      - 不推荐IgG，原因是：第一，大多数的IgG抗体不是来源于转录因子或特定组蛋白抗体同一动物的免疫前血清。第二，IgG通常pull down非常少的DNA，这样导致在后期的建库过程中PCR Cycles 数增加，导致不能达到作为control去除背景噪音的目的（会缺失和放大部分信息）。

      - 因此比较而言，Input更适合作为control。首先Input的建库量够，这样建库过程不需要over-amplifed，bias小。其次，最后测序得到的数据更均匀，以及全基因组覆盖度会更好。有人提到deletion 或者 RNAi knockdown目标转录因子的细胞同时做ChIP-Seq作为control更好。

    - 5.是否需要生物重复？
      - 有人建议需要生物重复，但是从目前我经历的项目来看，生物重复性不太好。还有人推荐用不同公司的抗体来做生物重复，这就需要考虑到经费的问题。

    - 6.关于超声处理
      - 超声没有什么特别的，需要注意的是超声处理在含有SDS的缓冲液中可能会破坏蛋白质－蛋白质和蛋白质－DNA相互作用。但是含有SDS的缓冲液能增加超声的效率，适应与DNA紧密结合的转录因子的ChIP-Seq。最近遇到一个老师，他的项目是一个转录因子跟不同的Parters蛋白结合，再binding到相关的区域，行使调控功能。这种情况就不建议用含有SDS的缓冲液了。

    - 7.关于测序数据量
      - 大部分人认为20 Mb 是个比较适合选择，然后取决于物种。

- 收集整理近10年的ChIP-seq数据分析及应用的综述

- 阅读超过5个公司的ChIP-seq数据分析结题报告

- 根据综述提取ChIP-seq数据分析的主干，绘制流程图，并且安装对应的软件

- 根据文章提取ChIP-seq数据分析的侧枝，了解更多的扩展分析，并且安装对应的软件

- 了解组蛋白修饰和转录组因子结合的ChIP-seq数据区别

- 通过实例了解如何使用ChIP-seq并且结合RNA-seq来研究一个特定的TF

  - 上皮-间质转化(epithelial-to-mesenchymal transition,EMT)是肿瘤侵袭和转移的首要步骤。Zeb1EMT的关键转录因子之一,它与多种癌症的发生发展有关，但在胶质母细胞瘤（GBM ）中Zeb1具体调节哪些基因并不清楚。

  - 首先，要想研究转录因子ZEB1在全基因组范围的结合情况，作者做了Zeb1的ChIP-seq，发现它在4430个基因上有高达6879个结合峰。

  - 虽然有这么多的结合，但并非都产生调控作用。Zeb1在GBM中是高表达的，作者使用shRNA敲低Zeb1，72h后观察基因的表达变化，发现200个基因下调，98个基因上调。

  - 作者将ChIP-seq和表达谱进行联合分析，确认这些基因的变化是否受到Zeb1的直接调控(韦恩图)，结果发现Zeb1的结合与多个基因的上下调均显著相关。

  - Zeb1直接抑制的基因（如Myo6, Shroom3, Pard6b,Nrxn3 ）GO富集到上皮细胞分化等，Zeb1直接激活的基因（如Itgb1, Nrp2, Prex1 ,S100B ）GO富集到糖蛋白代谢过程等。

  - 为了研究Zeb1的结合特性，作者也对motif进行了分析，发现Zeb1大量结合E-box序列（CAGGTG ）和HMG-box 序列（ACAAAG ）

  - 已有研究证明Zeb1直接结合基因的E-box并起到抑制表达的作用。

  - 在这里作者将目光聚焦到另一个motif——HMG motif，作者选择受Zeb1正向调控的基因Nrp2和Prex1深入研究，发现Lef1，Tcf3和Tcf4等因子，被招募到基因Nrp2和Prex1的调控区域的HMG motif ，与Zeb1发挥协同调控作用。

  - 在胶质母细胞瘤中，Zeb1不直接结合HMG motif，而是与Lef/Tcf因子一起被招募到该调控区域，并促进Prex1等基因表达，Prex1表达上调促进胶质母细胞瘤侵袭、影响患者生存期缩短

  - 参考文献：Pedro Rosmaninho et al, Zeb1 potentiates genome‐wide gene transcription with Lef1 to promote glioblastoma cell invasion, The EMBO Journal (2018). DOI: 10.15252/embj.201797115

  - http://emboj.embopress.org/content/early/2018/06/12/embj.201797115 

- 通过实例了解如何使用ChIP-seq来研究组蛋白修饰位点

  - 文章题目：小鼠胚胎干细胞中SETDB1独立调节H3K9三甲基化过程中发育相关基因PRC2活性，杂志： Genome research, 2015，IF=11.3

  - SETDB1是一种促进H3K9 甲基化修饰的组蛋白甲基转移酶。

  - 作者首先用ChIP-seq对H3K9me3做了4个重复，结合前人的SETDB1的ChIP-seq 实验数据进行比对，得到了两种SETDB1的peaks位点：solo peaks和ensemble peaks。ensemble peaks位点附近有H3K9me3峰值，而solo peaks附近没有。

  - 对solo peaks位点靶基因进行GO分析，发现大部分基因富集在神经发育调节功能中，而这部分基因又与核心蛋白复合体（PRC2）相互关联。

  - PRC2结合位点附近一般伴随着丰富的H3K27me3修饰，H3K27me3修饰会抑制SETDB1修饰H3K9me3。通过SETDB1敲除，发现H3K27me3减少，神经分化得到促进。

- 了解ChIP-seq测序数据分析一般流程

  完整代码在：https://www.jianshu.com/p/1384173c353b

  - 1）下机数据预处理和过滤

  - 2）比对到参考基因组

  - 3）确定与目的蛋白结合的DNA以及其结合区域

  - 4）对单个样品的蛋白结合峰进行分析，包括结合峰相关基因的注释、GO分析KEGG通路富集分析和motif分析，

  - 5）对多个样品可进行差异结合峰分析，包括差异结合峰相关基因的注释、GO分析、KEGG通路富集分析和motif分析，

  - 6）如果能够结合配套的RNA-seq或lncRNA-seq数据，还能对目的蛋白的调控机制做进一步的深入分析。

- ChIP-seq测序数据分析实战演练

  完整代码在：https://www.jianshu.com/p/1384173c353b

  - sra-tools：下载测序数据

  - fastqc,multiqc,trim_galore 测序数据的质量控制

  - bowtie,bowtie2,bwa 比对到参考基因组

  - MACS2,homer 找到IP的结合位点，坐标bed文件

  - deeptools 一些可视化

  - meme/homer motif  计算motif序列
    - https://mp.weixin.qq.com/s/PVHCiqhzoW3DsvdsVQIKJg

  - annotation(R包，ChIPpeakAnno，ChIPseeker)

  - 高阶分析

    - peaks差异分析

    - peaks对应的基因的富集分析

  - 结合其它组学