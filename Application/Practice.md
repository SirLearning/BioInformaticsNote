# RNA-seq 数据分析

1. 基因表达的量化和比较
	- 普通分析，就是差异基因，GO/KEGG等数据库注释，PPI网络
	- 高级分析，包括WGCNA,GSEA,时序分析，RNA编辑，依赖于课题设计实际情况
2. 表达数量性状基因座
3. 单细胞RNA-seq
4. 融合基因
5. 基因变异
6. 长的非编码RNA
7. 非编码小RNA

RNA-seq项目设计的一般原则
- 目前主流是表观调控和多组学
	 - 多组学通常就是DNA和RNA一起测序的项目
- 数据处理的流程
	1. 质控，需要fastqc及multiqc，trim-galore 
		 -  其它软件 trimmomatic, cutadapt, qualimap等等
	2. 比对：star, hisat2,bowtie2,tophat,bwa,subread，优先选择STAR或者hisat2
	3. 计数：featureCounts,htseq, bedtools ,deeptools salmon ，优先选择featureCounts
	4. normalization 归一化（统计学+数学知识背景）
		 - Total Count (TC)
		 - Upper Quartile (UQ)
		 - Median (Med)
		 - the DESeq normalization implemented in the DESeq Bioconductor package
		 - Trimmed Mean of M values (TMM) implemented in the edgeR Bioconductor package
		 - Quantile (Q)
		 - the Reads Per Kilobase per Million mapped reads (RPKM) normalization, FPKM,TPM
	5. 差异分析：导入R里面使用R包DEseq2或者edgeR分析，也可以选择limma的voom算法
	6. 比较salmon等无比对流程的转录本定量：注意salmon等无比对流程不一定可靠，至少不是金标准，谨慎使用

circRNA数据分析流程：
- circRNA概念：
	- 相比于普通RNA（链状RNA），circRNA不具有5' 末端帽子和3' 末端poly(A)尾巴，它以共价键连接首尾，形成封闭环状结构。
	- 这一结构使它不易被核酸外切酶RNaseR降解，故而比RNA更加稳定。
	- 目前认为，circRNA是由前体RNA（pre-mRNA）通过反向剪接反应（back-splicing）这一特殊的选择性剪接产生的。
	- circRNA多数源于外显子（exon），少部分由内含子（intron）直接环化形成，一般来说circRNA具有高度的保守性。
	- Biogenesis of Circular RNAs （Cell, September 25, 2014）
	- 了解circRNA的产生机制：The biogenesis and emerging roles of circular RNAs.（Nat Rev Mol Cell Biol, 2016 Apr）
		 - circRNA的生成机制以及在真核生物转录组中的作用机制。
	- 检测circRNA：Detecting circular RNAs: bioinformatic and experimental challenges （Nat Rev Genet. 2016 Oct 14） 
		- Novel Role of FBXW7 Circular RNA in Repressing Glioma Tumorigenesis 
- 主要材料与方法
	 - 样本：10个病理诊断的胶质母细胞瘤样本及其配对的邻近正常脑组织
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

miRNA数据分析流程
1. 文章及综述
2. TCGA数据库的miRNA-seq表达矩阵下游分析
3. lncRNA-seq数据分析流程
4. 全转录组数据分析流程
5. 全长转录组数据分析流程
6. 单细胞转录组分析流程

# WES数据分析

- 数据库： 
	- 遗传变异资源
	- TCGA
	- ENCODE
	- GTEx
	- 基因集注释数据库：
		- GO terms/Pathway (KEGG, BIOCARTA,Reactome)  
		- MSigDB
- GEO数据库的表达芯片数据处理
- 高级分析： WGCNA  , COX回归等生存分析 ，LASSO回归等机器学习
- GSE数据分析

# ChIp-seq数据分析

建库技术：
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

ChIP-seq测序建库技术：
- 染色质免疫共沉淀技术(Chromatinimmunopre-cipitation, ChIP)：在生理状态下, 利用甲醛将细胞内的DNA与蛋白质交联(Crosslink)，从而形成复合物，然后经细胞裂解、细胞核收集和裂解, 分离染色体, 通过超声或酶处理将染色质随机切割, 再通过抗原抗体的特异性识别反应沉淀此复合体，从而特异性地富集目的蛋白结合的DNA片段，通过对目的片断的纯化与检测，从而获得与该蛋白结合的DNA的信息。
	- 将染色质免疫共沉淀与二代高通量测序相结合的技术，它将ChIP获得的DNA片段进行高通量测序，捕捉到细胞内动态的、瞬时的蛋白质与DNA之间的相互结合作用，一次性获取与目的蛋白相结合的DNA序列、确定蛋白的结合分布和精确的结合位点以及结合基序等大量信息。
- 应用：
	- 一方面是DNA序列上转录因子结合位点(Binding sites)的识别, 如启动子、增强子等各种顺式作用元件(Cis-actingelement)的识别;
	- 另一方面主要应用在表观遗传学领域, 包括研究基因组DNA甲基化、组蛋白修饰和核小体定位等。
- 实验：
	1. 将活体细胞交联，将细胞核内的染色质分离出来，并用超声波打断成小片段（通常0.2-1kb），
	2. 用所研究的蛋白特异性抗体将目的蛋白及其结合的DNA片段免疫共沉淀下来，
	3. 将蛋白质-DNA复合物解交联并纯化DNA片段，
	4. 在DNA片段两端加测序接头构建DNA测序文库。
- 数据分析流程：
	1. 下机数据预处理和过滤
	2. 比对到参考基因组
	3. 确定与目的蛋白结合的DNA以及其结合区域
	4. 对单个样品的蛋白结合峰进行分析，包括结合峰相关基因的注释、GO分析KEGG通路富集分析和motif分析
	5. 对多个样品可进行差异结合峰分析，包括差异结合峰相关基因的注释、GO分析、KEGG通路富集分析和motif分析
	6. 如果能够结合配套的RNA-seq或lncRNA-seq数据，还能对目的蛋白的调控机制做进一步的深入分析
- 工具：
	- sra-tools：下载测序数据
	- fastqc,multiqc,trim_galore 测序数据的质量控制
	- bowtie,bowtie2,bwa 比对到参考基因组
	- MACS2,homer 找到IP的结合位点，坐标bed文件
	- deeptools 一些可视化
	- meme/homer motif  计算motif序列
	- annotation(R包，ChIPpeakAnno，ChIPseeker)

高阶分析：
- peaks差异分析
- peaks对应的基因的富集分析
- 结合其它组学