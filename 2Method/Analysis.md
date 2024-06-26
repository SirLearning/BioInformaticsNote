# 基因组分析

## *k-mer* analysis

k-mer
- 概念：substrings of length k contained within a biological sequence
	- 将reads迭代分成包含k个碱基的序列：长度为L的reads可以分成L-K+1个k-mers
- 作用：评估基因组特征，即作为一种Marker
	- 从头组装前的基因组

k-mer analysis
- 

## 高级分析 

WGCNA  , COX回归等生存分析 ，LASSO回归等机器学习

# 测序分析

## Genome assembly and annotation

3D genome	

- 有些基因一维离的远，三维离的近
- HiC-seq
	- HiC作用：

## Exome-Seq

家系遗传病

成本较低，数据量少很多

生物芯片 – 外显子芯片 – 富集外显子

- 系统生物学
- 多个探针加到一个片子上，用荧光等来检测

## ChIP-seq

核小体

实验流程

- formaldehyde
- sonication – shear
- antibody
- cross-links reversed
- build library – sequencing
	- 找到相关位置 – 两端测序

data analysis workflow:

- quality control – fasta, fastq
	- FastQC
- read mapping – sam, bam
	- Bowtie
	- BWA
- peaks calling – bed, wig, bigwig
	- 双峰，中间的
	- MACS2
	- SPP
- visualization
	- IGV
- repetitive regions
- annotation
	- ChIPpeakAnno – R包
	- ChIPseeqer
	- CEAS
	- GREAT
	- RegProtential
	- motif scan/MDSeqpos/meme

测序片段比较短

## ATAC-seq

assay for transposase accessible chromatin, DNA转座酶、高通量测序、染色体的可进入性

利用转座酶研究染色质可及性的高通量测序技术

表观遗传学研究技术

# 组学分析

## 基因组分析

组学 > 基因组

- 基因组内容

  - 基因组结构

    

    Promoter Exon intron
    ORF (Open Reading Frame): 从AUG（起始密码子）开始，至stop codon终止
    Codon Usage: CAI

    - 基因组大小

      - 基因组测序
        鸟枪法

      - 基因组拼装

        

        - 重复序列带来干扰

    - 基因数

      - 生物复杂性

        蛋白质组的多样性和复杂性
        1.转录后层面，mRNA剪切，拼接异构体
        2.蛋白质层面，蛋白质序列上一个或多个位点上发生翻译后修饰

        - 基因型到表型

      - 基因预测

        - 直接（序列高度匹配）
          同一或近缘物种中，与EST，cDNA, 蛋白质等序列完美或近似完美的匹配

        - 间接（基于统计学）

          1.序列比对(Homology)
          2.从头预测(ab initio)

          - HMM model![img](https://api2.mubu.com/v3/document_image/a46f70ad-6cbe-4fb8-ba8f-891c7db9de24-12251550.jpg)
            GENIE数据集

          - 可变剪切预测
            将EST, cDNA序列比对到基因组上

          - 部分有向图算法（POA）

  - mRNA

    转录后层面

    - mRNA Spiling
      - isform

  - 蛋白质

    翻译后修饰

    - Phosphorylation![img](https://api2.mubu.com/v3/document_image/888db341-f499-4d32-a1f0-3ffed4392003-12251550.jpg)

    - Ubiquitination![img](https://api2.mubu.com/v3/document_image/b0bad36d-897c-4662-b5a4-cf76b2569188-12251550.jpg)

    - Sumoylation![img](https://api2.mubu.com/v3/document_image/a21b14df-2359-4b9a-afa3-dcf3b355f82d-12251550.jpg)

    - Palmitoylation![img](https://api2.mubu.com/v3/document_image/2c7f10a2-ec25-44b2-b68b-15229ce54787-12251550.jpg)

    - Acetylation![img](https://api2.mubu.com/v3/document_image/06fc8c66-1251-4b8e-9271-6a00c8cb2e9a-12251550.jpg)

  - 相互作用网络

    P-P相互作用网络

    - 相互作用的数据质量，网络拓扑结构![img](https://api2.mubu.com/v3/document_image/40ed060f-9598-48b4-a892-00463d950f46-12251550.jpg)

    - Cytoscape
      网络构建和分析工具

    - 细胞信号通路
      工具：KEGG
      G1/S检验点：有调控方向

  - 基因/蛋白质的功能预测

    - 一级序列的比较：

      相似的序列具有相似的功能

      - 同源序列的鉴定：
        不同物种中的直系、旁系同源物的预测

      - BLAST

    - 保守的功能结构域：

      保守的功能

      - 常用工具：

        Interpro
        http://www.ebi.ac.uk/interpro/
        Pfam
        http://pfam.sanger.ac.uk/
        SMART
        http://smart.embl.de/
        PROSITE
        http://www.expasy.org/prosite/
        ProDom
        http://prodom.prabi.fr/prodom/current/html/home.php
        CDD
        http://www.ncbi.nlm.nih.gov/Structure/cdd/wrpsb.cgi

        - Interpro
          整合多个功能结构域的数据库，灵敏度高，可能有假阳性

        - Pfam
          手工收集结构域，蛋白质家族分类，计算速度较慢，准确性较高

        - SMART
          根据蛋白质三级结构获得结构域信息，准确性较高

    - 细胞亚定位分析

      - 信号肽(signal peptides)
        Nuclear export sequences (NES)
        Nuclear localization sequences (NLS)

      - TargetP
        根据蛋白质序列N端氨基酸组成预测细胞亚定位

      - SubLoc
        首次将SVM算法应用于细胞亚定位预测

      - PSORT
        k-nearest neighbor算法

    - 三级结构的比较：

      1.相似的结构具有相似的功能，催化反应通路的分子机制相似
      ​2.序列相似性：不显著！

      - 泛素（Ubiquitin）![img](https://api2.mubu.com/v3/document_image/039af3fd-e238-4eb5-a556-9c1bb7392143-12251550.jpg)
        主要负责蛋白质的降解

      - SUMO![img](https://api2.mubu.com/v3/document_image/8cd33a12-c720-4b42-bf08-507fbed42f7d-12251550.jpg)
        小的类泛素蛋白质，基因转录& 信号通路

      - 序列相似性：~20%

    - 蛋白质相互作用的预测

      - 技术

        - 酵母双杂交（Yeast two-hybrid, Y2H）只能筛选可溶性蛋白质

          

          

          1.GAL4-DBD-bait (hybrid 1)
          2.GAL4-AD-prey(hybrid 2; single or library)
          3.bait-prey相互作用: GAL4激活报告基因

          - Split-ubiquitin yeast two-hybrid

            

            1.两个膜蛋白分别与泛素分子的C端片段(“Cub”, 35–76) 和N端片段("Nub", 1–34) 连接
            2.Cub与转录因子融合，并且可被泛素蛋白酶切割
            3.bait–prey相互作用，泛素分子被切割，转录因子核内诱导报告基因表达

            - 膜蛋白的相互作用筛选

        - 亲和纯化/质谱![img](https://api2.mubu.com/v3/document_image/cf0ab30d-3210-4d81-a5bc-7ab57ce40de6-12251550.jpg)

        - 网络分析![img](https://api2.mubu.com/v3/document_image/00637ec5-600f-465d-9020-220c3638636d-12251550.jpg)
          Hub节点、拓扑结构、参数

        - 介数中心性（Betweenness centrality）![img](https://api2.mubu.com/v3/document_image/fa065a53-a702-43f3-b33f-f50bd2b41f24-12251550.jpg)

      - 工作

        - Biocuration & Literature mining

        - 基因组信息（genomic context method）
          Gene fusion and fission
          Conservation of gene order/bidirectional pairs
          Phylogenetic profile
          关联序列特征(Correlated sequence signatures)
          mRNA co-expression

        - Interolog

          

          

          

          直系同源的相互作用

          - 相互作用数据整合
            - PPI数据整合![img](https://api2.mubu.com/v3/document_image/4715df3f-0593-434f-9e10-de7e42547e4d-12251550.jpg)
              三种PPI数据：实验验证、Interolog、预测的PPI

        - Conservation of gene order/ bidirectional pairs

          - Gene order pairs![img](https://api2.mubu.com/v3/document_image/94eab0e0-730f-49bf-bcb6-da3ff5bccad1-12251550.jpg)

          - Bidirectional transcribed gene pairs![img](https://api2.mubu.com/v3/document_image/e2d6e717-1142-4a22-a2af-0e12b6e8fced-12251550.jpg)

        - Phylogenetic profiles![img](https://api2.mubu.com/v3/document_image/191185fe-b974-43d1-9f23-7b0bc5e33288-12251550.jpg)

        - 相关序列标记（Correlated sequence signatures）

          - PID model（最大似然性法）![img](https://api2.mubu.com/v3/document_image/b418d4cf-cb46-4844-8aea-24e0eaff833e-12251550.jpg)![img](https://api2.mubu.com/v3/document_image/55568ef0-6068-4553-95c5-20618247589f-12251550.jpg)
            faster and more convenient

          - PIDC model![img](https://api2.mubu.com/v3/document_image/9581d1dd-5211-4ccc-8aa7-09d7c51d307f-12251550.jpg)

        - 计算

          - P(Imn = 1)![img](https://api2.mubu.com/v3/document_image/cdb21082-c5c4-49e8-860e-c1941ef9255d-12251550.jpg)
            训练

          - Conserved co-expression![img](https://api2.mubu.com/v3/document_image/2800f351-fe2c-4ef6-9152-c5e7232bacc5-12251550.jpg)

        - 方法整合

          - 贝叶斯算法![img](https://api2.mubu.com/v3/document_image/518957df-d110-47e1-a59a-4e808be136ff-12251550.jpg)

          - STRING

          - PrePPI

            - 准确性比高通量实验高

            - 根据三级结构能够预测蛋白质相互作用界面
              1.PRKD1 and PRKCE
              2.EEF1D and VHL

      - 工具

        - DIP
          2000年，David Eisenberg研究组

        - MINT
          2002年，Molecular INTeraction

        - IntAct

        - BioGRID

        - Rosetta Stone
          Gene fusion/fission

        - InWeb_IM/InBioMap™
          实验+interolog

        - IID
          实验验证、Interolog、预测的PPI

- 非编码区

  - 功能元件

    - 启动子

      promoter > module > transcription factors(TF)

      - regulatory modules

      - regulatory motifs

    - 转录因子

      - Gal4p

      - Kruppel

    - 其他

      - Exon

        - exon splicing enhancer (ESE) 

        - exon splicing silencer (ESS)

  - 非编码RNA

    transfer RNA (tRNA)
    ribosomal RNA (rRNA)
    snoRNAs
    microRNAs
    siRNAs
    piRNAs: 与piwi相互作用的RNA
    long ncRNAs: Xist
    circRNAs

    - RNA二级结构

      

      - 显示方式

    - RNA能量

      Doug Turner的能量法则

      - 稳定性

        - 动态规划算法

          

          最大碱基配对（找出可能的路径）

          - RNA链与自身对比

            - 存在碱基配对则增加分数

            - 加入分歧的影响
              考虑所有k值

    - tRNA & rRNA

    - snoRNAs

      Small nucleolar RNAs
      介导其他RNA分子的化学修饰

      - 甲基化

    - microRNA / miRNA

      一种非编码小的RNA (~21–23 bp)，通过Dicer剪切其前体RNA (~70-90) 所得;
      miRNA以RNA-蛋白质复合物的形式，在动物和植物的细胞中广泛的表达，也称为miRISCs;

      能够促使与miRNA序列同源的靶基因的mRNA的降解 / 翻译的抑制

      - pri-miRNAs（发夹环）

        

        - Drosha & Dicer

          

          - Drosha切割位点(箭头)
            - Pri-miRNA被Drosha切割

          - Dicer切割位点(三角)
            - pre-miRNA被Dicer切割

          - 结构域（都具有RNase III 和dsRNA结合结构域）![img](https://api2.mubu.com/v3/document_image/af852695-be31-4ba8-8da5-4f1a01da4dcf-12251550.jpg)
            RIII, RNase III 催化结构域
            D, dsRNA 结合结构域
            PRORICH, proline-rich结构域
            RS-RICH, arginine/serine rich结构域

        - Exportin 5 (Exp5) 将miRNA装运到胞质中

      - miRNAs的多样性
        The miRBase Sequence Database

      - miRNAs的计算鉴定
        - MiRscan

      - miRNAs在发育中的调控作用及底物

        

        - lin-4 和let-7 miRNAs调控线虫发育的时间点
          在线虫的幼虫发育期，lin-4下调LIN-14和LIN-28蛋白质的浓度，从而一方面阻止后期发育，一方面促进幼虫的发育

      - 不完美配对

      - miRNA底物的计算发现

        miRanda网站

        - 位于基因的3’ UTR（untranslated region）区域，与成熟的miRNA互补
          植物：序列互补程度高
          动物：互补程度低

        - 靶序列特征
          长度较短(~21 nt)
          G-U配对
          错配和空位(bulges)
          假阳性高

        - 准确性
          mRNA UTR的二级结构

        - 特性

          - 保守性

            miRNA靶序列在不同物种中保守

            - 与miRNA的5’端匹配更好

          - 成簇性
            倾向于聚集成簇

      - Targetscan
         给定一个在多物种中保守的miRNA及相应的直系同源UTR区域
         miRNA seed: 7nt
         延伸每一条seed并发现最佳能量
         计算Z值
         排序结果，获得Ri值
         保留Zi>Zc和Ri<Rc的结果

  - 转座子（Transposon）![img](https://api2.mubu.com/v3/document_image/607dd67c-168f-40ee-b706-a1fd2d96fb82-12251550.jpg)
    在基因组中能够移动位置的DNA序列

  - 重复片段

  - 伪基因（Pseudogene）

- 基因组注释

  - 基因组序列的拼装

  - 基因预测

  - 可变剪切的预测

  - 非编码的功能元件的预测


## miRNA组学分析

miRNA

- miRBase – database
- 通过物种搜索
- 作用机制：
	- 结合nRNA 3’端UTR – 抑制表达
	- 完全匹配结合mRNA – 切割，类似RNAi
- 参与生物体生长、发育、衰老、疾病和死亡的调节
- question:![image-20221124140325679](C:/Users/%E9%83%91%E8%BE%BE/AppData/Roaming/Typora/typora-user-images/image-20221124140325679.png)

miRNA-seq/smRNA-seq

- smRNA:
- small RNA-seq经常用于鉴定miRNA的表达
- pipline:
	- 准备smRNA
	- sequencing
		- single read (SR)
		- paired end (PE)
	- data analysis
	- tools
		- quality
			- question:![image-20221124142427585](C:/Users/%E9%83%91%E8%BE%BE/AppData/Roaming/Typora/typora-user-images/image-20221124142427585.png)
		- trim
		- alignment to genome
			- map to genome
			- common alignment conventions
			- remove other non-coding RNA
		- map to mirna_precursor
		- miRNA expression
			- RPM
			- RPKM
			- numReads
			- geneLength
			- totalNumReads
		- differential expression analysis
			- 标准化方法
			- 差异基因检测
		- novel miRNA discovery

miRNA

- expression
- SNP (single-nucleotide polymorphism)
	![image-20221124144552457](C:/Users/%E9%83%91%E8%BE%BE/AppData/Roaming/Typora/typora-user-images/image-20221124144552457.png)
- Target prediction
	- seed – binding site
	- 结合最小自由能
	- question:
		![image-20221124144954761](C:/Users/%E9%83%91%E8%BE%BE/AppData/Roaming/Typora/typora-user-images/image-20221124144954761.png)
- disease databases

annotation – TAM

miRNA & lncRNA

## TCGA

the cancer genome atlas 癌症基因组图谱

- 人类20多种癌症中全基因组图谱改变中所需的研究框架
- 合作机构：
	- national cancer institute (NCI) 美国国立癌症研究所
	- national human genome research institute (NHGRI) 美国国立人类基因组研究所
- 部门：
	- TSS – 临床数据
	- BCR – 技术类型数据
	- DCC – 数据协调中心
	- GCCs/GSCs – 鉴定中心/测定中心
- 数据组织形式：barcode
- 数据发布：genomic data commons (GDC平台)

data type:

- clinical data
- images
- microsatellite instability (MSI)
- sequening:
	- DNA/miRNA/mRNA/total RNA
- protein expression
- array-based expression
- DNA methylation
- copy number

data level: raw/processed/segmented(interpreted)/summary(regions of interest ROI)

低水平测序数据 – CGHUB

## TCGA

肿瘤相关，是一个项目组织: 癌症基因组计划

团队组成：

- TSS
- BCR
- DCC
- GCCs/GSCs

barcode: 定义病人样本

GDC: 数据发布平台

数据类型：

- raw – fastaq
- processed – sam(测序), fam
- se/int
- ROI

# 测序分析

## Functional Enrichment Analysis

questions:
![image-20221124161610713](C:/Users/%E9%83%91%E8%BE%BE/AppData/Roaming/Typora/typora-user-images/image-20221124161610713.png)

Enrichment Analysis: statistically比较一个gene set和background

- 分类：
	- genomics, proteomics – 对一个物种的全部注释
	- microarrays – 对一个gene set的全部注释\
	- RNA-seq data analysis – 特定组织中的基因长度趋势效果
- gene list:
	- identifier
	- method
- workflow:
	- 后端注释数据库 annotation database
	- data mining：要输入一个gene list
		- algorithms – annotation – diff.discovery ideas
			- sources
		- 数据检验 statistics：
			- hypergeometric
			- binomial
			- &chi;<sup>2</sup> (chi-square)
			- Fisher’s exact test
			- &Zeta;
			- Kolmogorov-Smirnov
			- Permutation
	- 结果 – GO terms

question:
![image-20221124164456876](C:/Users/%E9%83%91%E8%BE%BE/AppData/Roaming/Typora/typora-user-images/image-20221124164456876.png)

## GEO SRA

### GEO

gene expression omnibus – NCBI基因表达数据库

数据组织方式：

- platform(GPLxxx)/samples(GSMxxx)/series(GSExxx)
- dataset(GDSxxx)/profile(表达谱)

cluster

tools:

- GEO2R

### sequence read archive (SRA)

throughput sequencing data

共享有史以来所有用户的测序数据

## 单细胞测序

单细胞技术：研究胚胎发育中早期细胞变化

- 背景
- 需求 – 癌细胞混合物
	![image-20221124185339862](C:/Users/%E9%83%91%E8%BE%BE/AppData/Roaming/Typora/typora-user-images/image-20221124185339862.png)

### 10&times;genomics高通量单细胞技术

微流控技术: 自动化分选平台 – 单细胞转录组测序，自动完成：

- 分选细胞 – 分析注释 – 特定细胞亚群marker基因
	- 自动化分选：一次10000个细胞，对成活率有要求
		- 10&times;Genomics: 凝胶珠、油滴
		- single tube – smart-seq2
	- 单细胞转录组分析
- 建库

Single rube – 传统技术

### 单细胞获取+测序技术

单细胞获取：

- 有限稀释 limiting dilution
- 显微操作 micromanipulator
- 激光显微切割 LCM
- 流式细胞分选 FACS
- 微流控 microfluidics

amplification – genome

- multiple displacement amplification (MDA)
- multiple annealing and looping-based amplification cycles (MALBAC)

全转录组测序

- 单细胞全基因组测序 scWGS
- 单细胞外显子测序 scWES

- 扩增
- biopic

分析：

- 表达量分析/差异表达分析/聚类分析/功能分析
- mRNA/lncRNA差异分析/靶标预测及分析
- circRNA差异分析/circRNA来源分析
- 对primary tumors的单细胞测序分析：
	1. somatic(体细胞) mutation calling
	2. population analysis
	3. progression inferring (key genes)
		- key mutation
		- evolution analysis – Bladder Cancer (BTCC)

### 临床应用

diagnose 早期诊断 – invasive

prognosis 预后(预测后果)

个性化治疗

- target-drugs design
- cocktail treatment

动态监测

- tumor “stem cell” detection

肿瘤组学治疗分析：

- 遗传算法
- center – 找到血液中/脑脊液中的肿瘤因子
- 愈后
- 检测
- 试管婴儿胚胎单细胞检测 – 植入前遗传学诊断PGD

# 肿瘤组学分析GSCA

## 癌症数据分析平台

肿瘤组学数据

- 公共数据 – TCGA
	![image-20221124193118027](C:/Users/%E9%83%91%E8%BE%BE/AppData/Roaming/Typora/typora-user-images/image-20221124193118027.png)
	- GSCA workflow:
		1. gene set expression
			- gene set mRNA表达数据+cancer type – GSVA score
		2. gene set nutation
		3. immune
		4. TNM stage
	- cell cycle pathway
		- GSCA – mutation
	- oncomine
- 自测数据 – 肿瘤转录组数据
	- 肿瘤免疫分析
		![image-20221124193205611](C:/Users/%E9%83%91%E8%BE%BE/AppData/Roaming/Typora/typora-user-images/image-20221124193205611.png)
		- T cell receptor (TCR)
		- CharActerzing TCR reperToires (CATT)
	- 表达调控分析
		![image-20221124193227609](C:/Users/%E9%83%91%E8%BE%BE/AppData/Roaming/Typora/typora-user-images/image-20221124193227609.png)
		- human transcription factor (TF)
		- FFLtool – analyze with gene list
		- specifically expressed gene (SEG)

筛选关键分子 – 验证 – 功能研究

- 细胞系筛选 GEDS(gene expression display server)
- 细胞系鉴定 CCLA(cancer cell line authentication)

癌症DB/研究中心

- ICGC：癌症联盟
- GTEx: 正常死亡器官组学分析

Tumor immunology – 有一些没有响应 – 提高

免疫细胞疗法：

- 单细胞分析/每个免疫 – 费时费力
- T细胞亚型
# 分子进化与系统发育分析

生物学家：We have a dream…
Tree of Life: 重建所有生物的进化历史并以系统树的形式加以描述
梦想走进现实：How?
最理想的方法：化石！——零散、不完整
比较形态学和比较生理学：确定大致的进化框架——细节存很多的争议
第三种方案：分子进化

- 概念

  1964年，Linus Pauling提出分子进化理论
  基本假设：核苷酸和氨基酸序列中含有生物进化历史的全部信息

  - 研究目的

    - 物种间生物系统、发生的关系
      从物种的一些分子特性出发，构建系统发育树（tree of life），增进对物种分类的研究

    - 大分子功能与结构的分析：
      同一家族的大分子，具有相似的三级结构及生化功能，通过序列同源性分析，构建系统发育树，进行相关分析，进一步研究蛋白质的功能预测

    - 进化速率分析：
      例如，HIV的高突变性；哪些位点易发生突变？

- 理论基础

  - 进化模式

    - DNA突变：

      

      替代，插入，缺失，倒位

      - HIV protease: 高突变性![img](https://api2.mubu.com/v3/document_image/21b6c562-fcae-47da-ab69-52e64acb7de2-12251550.jpg)
        Ka/Ks >> 1, 强的正选择压力，具有很高的可突变性

    - 核苷酸替代：![img](https://api2.mubu.com/v3/document_image/0463ba2d-ca87-41e6-8c13-cc1469244924-12251550.jpg)
      转换（Transition）：嘌呤被嘌呤替代，或者嘧啶被嘧啶替代
      颠换（Transversion）：嘌呤被嘧啶替代，或者嘧啶被嘌呤替代

    - 基因复制：

      多基因家族的产生以及伪基因（Pseudogene）的产生

      - 单个基因复制![img](https://api2.mubu.com/v3/document_image/e1888d48-8c0c-4cd0-9048-c0d5a3a5529f-12251550.jpg)

      - 染色体片断复制![img](https://api2.mubu.com/v3/document_image/4c0b1826-30ec-48f4-94b9-1beed019392a-12251550.jpg)

      - 基因组复制![img](https://api2.mubu.com/v3/document_image/8b3ef985-c7f9-4f94-92d4-e4b7e0b317f1-12251550.jpg)
        研究结果：克鲁雄酵母中的同源基因数量与酿酒酵母相比为1：2

  - 同源性分析->功能相似性

    - 同源性

      Ortholog（直系同源序列）：两个基因通过物种形成的事件而产生，或源于不同物种的最近的共同祖先的两个基因，或者两个物种中的同一基因，一般具有相同的功能
      Paralog（旁系同源序列）：两个基因在同一物种中，通过至少一次基因复制的事件而产生
      Xenolog（异同源序列）：由某一个水平基因转移事件而得到的同源序列
      Convergent evolution（趋同进化）: 通过不同的进化途径获得相似的功能，或者功能替代序列

      - 直系同源序列 vs. 旁系同源序列![img](https://api2.mubu.com/v3/document_image/01ed3d2c-0165-4a67-b025-7269dd3b5cc1-12251550.jpg)

      - 异同源序列![img](https://api2.mubu.com/v3/document_image/936fc2ad-9922-4508-81ab-276640ec68df-12251550.jpg)

      - Convergent evolution（趋同进化）:![img](https://api2.mubu.com/v3/document_image/c42935d0-ca28-458e-9d57-3997b1013285-12251550.jpg)![img](https://api2.mubu.com/v3/document_image/13d32bb4-5dee-41d6-85d7-348795bb3f4d-12251550.jpg)
         通过不同的进化途径获得相似的功能，或者功能替代序列

  - 密码子（codon）：

    在随机或者无自然选择的情况下，各个密码子出现频率将大致相等

    - 密码子偏好：

      各个物种中，编码同一氨基酸的不同同义密码子的频率非常不一致

      - 可能的原因：
        密码子对应的同功tRNA丰度的不同–反密码子（Anticondon）

      - 大肠杆菌RNA聚合酶![img](https://api2.mubu.com/v3/document_image/d4fbafde-0c05-4138-9b6e-54cb1f2fcd01-12251550.jpg)
        密码子偏好非常明显；
        ​例如
        同为编码Phe的同义密码子UUU和UUC，二者出现的次数显著不等，UUU (15次)，UUC (44次)；
        编码Arg的四个密码子CGU, CGC, CGA, CGG, 出现次数分别为：89，46，1，0.
        提示：对应CGG的同功tRNA可能不存在！

      - tRNA & Anticodon![img](https://api2.mubu.com/v3/document_image/cc5caa8a-1218-4db9-8f44-6746f2a6b18c-12251550.jpg)
        每一个密码子，对应一个tRNA
        tRNA通过Anticodon来识别codon,联系mRNA和氨基酸序列的合成
        密码子的使用偏好：由密码子对应的tRNA的进化及丰度来决定

    - 标准密码子![img](https://api2.mubu.com/v3/document_image/11426ac9-a330-41b5-ae99-2132220925f4-12251550.jpg)

  - 碱基出现的频率

    假如：每个核苷酸位点上的替代是随机发生的，则A,T,C,G出现的频率应该大致相等

    - 实际情况：DNA受到自然选择的压力，各个位点的碱基出现频率并不相等
      需要解决的问题：
      每个位点上受到什么样的选择压力？
      各个位点的碱基频率反映了什么样的规律？

    - 表征/统计的方法：
      计算G+C的含量，并进行比较

- 分子进化理论

  阳性选择，适应性进化，达尔文进化：
  DNA分子显著出现非同义替代，改变编码蛋白质的氨基酸组成，并产生新的功能
  阴性选择，净化选择：
  DNA分子的同义替代显著，较少改变蛋白质的氨基酸组成，其原来的功能高度保守
  中性进化（木村资生，Motoo Kimura）：
  同义替代与非同义替代比例相当，突变不好不坏，不改变或轻微改变蛋白质的功能

  - 学术名词

    - 同义替代 vs. 非同义替代![img](https://api2.mubu.com/v3/document_image/ad4330f0-4036-4cd3-8d84-72c28173e682-12251550.jpg)

    - 编码区 vs. 非编码区

      编码区：DNA上编码功能性的基因的部分
      非编码区：或称基因组序列，绝大部分无功能

      - 选择压力：
        编码区：阳性选择1%；中性进化80%；阴性进化19%
        非编码区：~100%的中性进化

      - 编码区：密码子

        对于同义的密码子，第一位少部分可以允许不同，例如，编码Ser的六个密码子：TCT, TCC, TCA, TCG, AGT, AGC
        第二位必须相同
        第三位绝大多数可以不同-> 近似随机

        - 结论
          第一位：阴性进化占大部分，中性进化占小部分
          第二位：阴性进化
          第三位：阴性进化占小部分，中性进化占大部分

        - 推论
          密码子第三位的碱基出现概率接近基因组序列的碱基频率
          第二位的碱基出现频率与基因组序列的基础频率相差最大

      - 基因组GC含量![img](https://api2.mubu.com/v3/document_image/52e955d4-013e-487d-ad6b-b2cefe4d4f85-12251550.jpg)
        细菌基因组的GC含量：25%~75%

  - 密码子偏好的应用及计算

    基本假设：在高表达的基因中，密码子的选择，更倾向于使用“优化”的同义密码子

    - 推论
      推论1：给定一个物种的一些高表达的基因，我们可以估算优化的同义密码子的分布
      推论2：接着，我们可以对给定的一个未知基因的序列进行密码子分布的分析，预测该基因的表达量！
      推论3：对于一个表达量很低的基因，我们是否能够通过将少量的密码子改变成优化密码子，从而显著提高基因的表达量？

    - 相对密码子使用频率（relative synonymous codon usage, RSCU）

      

      定义：观测到的某一同一密码子的使用次数，除以“期望”的该密码子出现次数

      - 相对适应性（the relative adaptation）![img](https://api2.mubu.com/v3/document_image/2f9a0609-b17c-4ae8-ba7b-529a854a17fa-12251550.jpg)
        该同义密码子的观察值，除以编码该氨基酸的同义密码子的最大值

      - 大肠杆菌& 酵母![img](https://api2.mubu.com/v3/document_image/a2c5c3e4-613b-45c7-a333-09c8263c1916-12251550.jpg)

    - CAI: codon Adaptation Index

      

      - 大肠杆菌的rpsU![img](https://api2.mubu.com/v3/document_image/e1e8abe7-0bf5-4d94-b4f2-5448c295af39-12251550.jpg)

      - 大肠杆菌和酵母：部分基因的CAI![img](https://api2.mubu.com/v3/document_image/f2342a6b-dd3c-4cdd-95c8-899e8c701ac3-12251550.jpg)

      - 异源基因：在其他物种中的CAI![img](https://api2.mubu.com/v3/document_image/131f6383-adc5-42d2-af2a-8cac7b8e13fe-12251550.jpg)

  - 氨基酸序列的进化演变

    分子进化的分析：基于氨基酸序列的分析早于DNA序列
    优势：氨基酸序列更为保守，对年代跨度大的进化分析有帮助；数学模型较DNA远为简单

    - p-distance![img](https://api2.mubu.com/v3/document_image/f7334e70-d5cd-4ccf-b39d-d236ee0e64d2-12251550.jpg)

    - PC：泊松校正

      基本假设：
      ​ 序列差异的百分比（p）与分歧时间t的关系：t较短的时候，回复突变较少，两者大致成线性关系；当t较大时，回复突变增多，二者成非线性关系
       令γ为某一位点每年的氨基酸替代率，并假设所有位点的γ都相同

      - 泊松分布应用

        

        - 祖先序列未知

          

          不知道当前的序列从何演化而来

          - 结果![img](https://api2.mubu.com/v3/document_image/804e4b6f-36e0-457e-a733-e9afbf96e5a9-12251550.jpg)

    - p-距离vs. 泊松距离![img](https://api2.mubu.com/v3/document_image/92c0dc15-86d9-4003-b568-312a14916e97-12251550.jpg)

  - DNA序列的进化演变

    基因组上存在着多种多样的DNA区域，例如蛋白质编码区，非编码区，内含子，侧翼区，重复片断以及插入序列等
    本章考虑蛋白质与RNA的编码区的DNA序列的进化演变模型

    - 两条DNA序列的差异

      

      长度为n、不同的碱基对为nd的DNA序列

      - 核苷酸的改变：![img](https://api2.mubu.com/v3/document_image/32e32006-3abd-4d59-b82f-3b4a02589f85-12251550.jpg)
        转换P、颠换Q，则p=P+Q
         当p较小时，如果核苷酸替代是随机发生的，Q=2P。通常转换比颠换出现频率高；

    - 核苷酸替代数的估计![img](https://api2.mubu.com/v3/document_image/213e28e6-a218-408e-ba7f-0845b41cbed2-12251550.jpg)

    - 进化模型

      - Jukes-Cantor法

        - 条件

          

          

          - 因此，差分方程为：![img](https://api2.mubu.com/v3/document_image/63b96919-aaa0-46fd-92bd-a69a22fa0425-12251550.jpg)![img](https://api2.mubu.com/v3/document_image/e09cd4eb-78d5-4632-9a6f-360f9b8e2312-12251550.jpg)![img](https://api2.mubu.com/v3/document_image/fea5930a-fe32-4cbf-afd2-2b8595baab7f-12251550.jpg)

      - Kimura两参数法![img](https://api2.mubu.com/v3/document_image/4b164505-05bc-4574-a272-2700a6158b3a-12251550.jpg)
        对于实际数据，转换替代速率通常高于颠换速率；因此，每年每个位点转换替代率为α，颠换替代率2β

    - 同义与非同义的核苷酸替代

      同义替代：编码区的DNA序列，核苷酸的改变不改变编码的氨基酸的组成
      非同义替代：核苷酸改变，从而改变编码氨基酸的组成

      - Ka/Ks

        

        Ka：每个非同义位点的非同义替代数目
        Ks：每个同义位点的同义替代数目
        PAML, MEGA等工具：计算Ka/Ks及统计显著性

        - 分析
          Ka/Ks ~ 1: 中性进化
          Ka/Ks << 1: 阴性选择，净化选择
          Ka/Ks >> 1: 阳性选择，适应性进化
          多数基因为中性进化，约1%的基因受到阳性选择->决定物种形成、新功能的产生

      - 统计显著性的检验
        Fisher’s Exact Test

      - 计算方法：

        进化通径法
        Kimura两参数法
        采用密码子替代模型的最大似然法

        - 进化通径法：Nei-Gojobori

          

          首先需要考虑：潜在的同义（S）和非同义位点数（N）
          基本假设：所有核苷酸的替代率相等

          - 潜在的同义和非同义位点数的估计![img](https://api2.mubu.com/v3/document_image/64cf26d4-111a-4f26-a185-1f6d8cbda428-12251550.jpg)

          - 整个序列的同义与非同义估计![img](https://api2.mubu.com/v3/document_image/17992396-36be-4075-9df4-be900b6dc30e-12251550.jpg)

          - 进化通径![img](https://api2.mubu.com/v3/document_image/594292b2-1eed-4d1c-a7da-ab1d85f9d74e-12251550.jpg)![img](https://api2.mubu.com/v3/document_image/ba2a0886-3b81-4332-ad84-0797a1022701-12251550.jpg)
            Sd与Nd的计算

          - Nei-Gojobori的改进版本![img](https://api2.mubu.com/v3/document_image/0a4c2fda-2c7e-4cac-aae9-919806289edf-12251550.jpg)![img](https://api2.mubu.com/v3/document_image/281e9833-fb71-47aa-b323-e0d50d7a1ca7-12251550.jpg)
             Nei-Gojobori的原始版本假设四种核苷酸之间的替代是随机的
             实际情况中：转换变化率应该比颠换变化率高，并且第三位上发生转换变化常常是同义的。因此这种情况下，估算的S将比Nei-Gojobori所估计的数值大

    - 系统发育树的构建（分子进化树/分子进化分析）

      通过进化树的构建，分析分子之间的起源关系，预测分子的功能
      ​

      - 术语

        

        - 树

          - 类型![img](https://api2.mubu.com/v3/document_image/89620f93-b3c9-4c56-ad5f-e1736a547064-12251550.jpg)
            以上三种类型的系统发育树表示相同的分支状况，相同的进化关系

          - 树只代表分支的拓扑结构![img](https://api2.mubu.com/v3/document_image/f7f41014-8c77-4fb5-81f1-e3cd6471249b-12251550.jpg)

          - 无根树，有根树，外围支

            

            - 无根树和有根树：潜在的数目![img](https://api2.mubu.com/v3/document_image/7771b5ff-c1e3-4243-90c5-fe2d4145d70f-12251550.jpg)
              Taxa增多，计算量急剧增加，因此，目前算法都为优化算法，不能保证最优解

      - 系统发育树重建分析步骤
        1.多序列比对（自动比对，手工校正）
        2.选择建树方法以及替代模型
        3.建立进化树
        4.进化树评估

      - 系统发育树重建的基本方法（建树方法）：

        最大简约法（Maximum Parsimony，MP）
        ​距离法（Distance-based methods）
        ​最大似然性法（Maximum Likelihood，ML）
        ​贝叶斯方法（Bayesian method）

        - 最大简约法(MP)

          理论基础为奥卡姆剃刀（Ockham）原则：计算所需替代数最小的那个拓扑结构，作为最优树
          在分析的序列位点上没有回复突变或平行突变，且被检验的序列位点数很大的时候，最大简约法能够推导获得一个很好的进化树

          - 优缺点
            优点：不需要在处理核苷酸或者氨基酸替代的时候引入假设（替代模型）
            缺点：分析序列上存在较多的回复突变或平行突变，而被检验的序列位点数又比较少的时候，可能会给出一个不合理的或者错误的进化树推导结果

          - 信息位点(Informative sites)

            

            

            至少在2个taxa中保守
            至少存在2个不同碱基/氨基酸
            每个不同碱基/氨基酸至少出现2次

            - 分析
              Position 5, 7, 9为信息位点
              基于position 5的三个MP树:
              Tree 1长度1，Tree 2 & 3长度2
              Tree 1更为简约：总长：4；Tree 2长5；Tree 3长6
              计算结果：MP tree的最优结果为tree 1

        - 距离法

          又称距离矩阵法，首先通过各个物种之间的比较，根据一定的假设（进化距离模型）推导得出分类群之间的进化距离，构建一个进化距离矩阵。进化树的构建则是基于这个矩阵中的进化距离关系

          - 简单的距离矩阵

            

            - 通过距离矩阵建树的方法

              常见有：
              Fitch-Margoliash Method (FM法): 对短支长非常有效
              Neighbor-Joining Method (NJ法/邻接法):求最短支长，最通用的距离方法
              Unweighted Pair Group Method (UPGMA法)

              - Fitch-Margoliash方法(FM法)![img](https://api2.mubu.com/v3/document_image/c2b39148-bcc5-4d01-ac9e-aa1250c4e54b-12251550.jpg)![img](https://api2.mubu.com/v3/document_image/22e20856-8585-45ed-9318-c4d17372e4de-12251550.jpg)![img](https://api2.mubu.com/v3/document_image/a8f3fb52-7827-4d94-9e88-b1b7d0eb125b-12251550.jpg)![img](https://api2.mubu.com/v3/document_image/ad48855d-4113-4759-bdf4-7b314b95d271-12251550.jpg)![img](https://api2.mubu.com/v3/document_image/fe5da4a3-9806-4e70-b4e0-e659661224b9-12251550.jpg)![img](https://api2.mubu.com/v3/document_image/51e4dd40-ae33-470b-a576-385b153c6bb5-12251550.jpg)

              - NJ/邻接法

                

                与FM方法非常类似

                - 找到距离最近的两个点

                  

                  - 计算A, B的分支长度![img](https://api2.mubu.com/v3/document_image/3950ea46-b359-4a8d-bc5e-5fff96135a6d-12251550.jpg)

              - UPGMA法![img](https://api2.mubu.com/v3/document_image/0149bc0a-4ee1-4bf1-a736-1f498a554e10-12251550.jpg)![img](https://api2.mubu.com/v3/document_image/393cc494-9519-4c97-adf5-f1c5ce608134-12251550.jpg)![img](https://api2.mubu.com/v3/document_image/1f48f264-ee12-4b6a-a342-77f7d7ac1bc5-12251550.jpg)![img](https://api2.mubu.com/v3/document_image/6ec90157-959f-436f-ab3b-fbbd410844b3-12251550.jpg)

        - 最大似然法(ML)

          对于每个树，我们需要确定4个分支的长度
          最大化似然性Pr[ Data|H, M],该函数包含16 +16 +16项，每一项是5个概率的乘积
          最大似然法非常耗费时间
          NP-hard问题：太多树需要考虑

          - 基于似然性（likelihood）的推断![img](https://api2.mubu.com/v3/document_image/3b32015c-f65e-49b9-88cc-2c73f55d593d-12251550.jpg)
            硬币两个面，正面(H)，背面(T)
            六次投掷后：HHHHTT
            正面出现的概率p，背面出现的概率1-p
            当p=0.67时，概率函数达到最大值
            因此，正面出现的概率可能是0.67

          - 方法内容

            

            寻找树H包含k个叶节点，从而最大化条件概率
            L=Pr[Data|H, M]
            L即为在模型M下的似然性(likelihood)

            - 似然性的计算![img](https://api2.mubu.com/v3/document_image/39ac8ed4-3402-486a-a02f-bc1a80bd94ec-12251550.jpg)![img](https://api2.mubu.com/v3/document_image/e5cb3181-f03c-4190-b54a-2935133db391-12251550.jpg)

        - 贝叶斯方法(BayesianMethod)

          考虑我们有一个比对A (data)，包含k条序列S1, S2, … Sk

          如何确定先验概率分布？
          Markov Chain Monte Carlo (MCMC)
          数据采样，建立先验的概率分布
          如果先验概率是均匀分布，则贝叶斯方法等同于最大似然性方法
          计算时间比最大似然性方法更久
          ​

          - 先验概率分布（prior probability distribution）已知

            

            所有树的概率分布，且需要独立于数据本身

            - 贝叶斯理论对给定树T计算概率

              

              - 树的后验概率(posterior probability)![img](https://api2.mubu.com/v3/document_image/dcd5cebc-af5f-4bfa-a9e8-b09bdb1035fc-12251550.jpg)
                即Pr[T|Data]，是根据给定数据所观测到该树的概率

        - 建树方法总结![img](https://api2.mubu.com/v3/document_image/5eb08fd8-c54b-4c46-8613-2c7db77e558b-12251550.jpg)

        - 建树一般原则![img](https://api2.mubu.com/v3/document_image/e8762c52-63e5-4ef0-8575-76fccb9d9839-12251550.jpg)
          可靠的待分析数据
          准确的多序列比对
          选择合适的建树方法：
          序列相似程度高，NJ, MP首选
          序列相似程度较低，ML, 贝叶斯首选
          序列相似程度太低，无意义
          一般采用两种及以上方法构建进化树，无显著区别可接受

      - 选择外围支(Outgroup)
        选择一个或多个已知与分析序列关系较远的序列作为外围支
        外围支可以辅助定位树根
        外围支序列必须与剩余序列关系较近，但外围支序列与其他序列间的差异必须比其他序列之间的差异更显著

      - 自展法(Bootstrap Method)![img](https://api2.mubu.com/v3/document_image/77f37049-c817-4946-966f-0f4d4cce572d-12251550.jpg)
        用来分析进化树的可靠性
        从排列的多序列中随机有放回的抽取某一列，构成相同长度的新的排列序列
        重复上面的过程，得到多组新的序列
        对这些新的序列进行建树，再观察这些树与原始树是否有差异，以此评价建树的可靠性

    - 实际数据中

      同义替代与非同义替代的速率不同
      不同的基因/蛋白质，其进化的速率不同
      然而，对于特定的基因，具有一定的、恒定的进化速率

      - 基因同义替代与非同义替代的速率![img](https://api2.mubu.com/v3/document_image/33c9fce7-0cf2-415f-8d10-bfcd109570e8-12251550.jpg)

      - 速率恒定的证据：血色素![img](https://api2.mubu.com/v3/document_image/61193907-8adc-4360-b265-f6d66e5c8fc3-12251550.jpg)

    - 分子钟假设

      序列之间的遗传差异的数量是自分化以来的时间的函数
      分子变化的速率相当稳定，可以用来预测分化的时间

      - 进化时间的估计

        物种分化时间有化石证据

        - 遗传距离d的计算：
          氨基酸序列：p-距离，d-距离
          DNA序列：Jukes-Cantor距离，Kimura距离

        - 物种分歧点：
          使用考古数据确定共有祖先，确定分化时间T

        - 计算分子的分化/进化的速率：
          r=d/2T

        - 对新的序列，计算分化时间：
          Tnew=dnew/2r

# 高通量DNA测序：生物信息学的挑战

Base calling: 根据图像识别碱基
序列读段回贴到参考序列上
全基因组的组装
基因型（Genotype）和SNP的识别
RNA-Seq数据分析：检测基因表达、可变剪接异构体等
Chip-Seq数据中的Peak finding，以及受调控基因的回贴

- 工作

  - Pyrosquencing![img](https://api2.mubu.com/v3/document_image/7ed692c3-86a1-428b-96dd-03e1e1d6899e-12251550.jpg)![img](https://api2.mubu.com/v3/document_image/3382413a-e023-48fe-b58a-fe1c39642ad0-12251550.jpg)
    Roche 454

  - Sequencing by synthesis![img](https://api2.mubu.com/v3/document_image/a69bb27f-b596-4eb3-815f-bc18cfb4ae9b-12251550.jpg)
    Illumina Genome Analyzer

  - 全基因组测序![img](https://api2.mubu.com/v3/document_image/904e0841-ba23-4660-aa74-807c499dc79e-12251550.jpg)

  - 从头测序（De novo sequencing）

    新的物种/品系
    短读段组装中的挑战：重复片段

    - 突发事件的基因组学（Emergency Genomics）
      SARS病毒、禽流感、猪流感、新冠病毒…

    - 古代DNA（Ancient DNA）
      楼兰女尸，罗马军团，长沙马王堆，曹操墓…
      猛犸，乳齿象，恐龙

  - 基因组
    - 重要动植物

  - 宏基因组（Metagenomics）
    发现环境中，或者疾病样本中所有的物种
    人类微生物组（Human Microbiome）
    口腔、肠道、皮肤的疾病vs. 健康微生物的群落
    全基因组测序
    多物种转录本的完全检测
    微生物群落中遗传变异的深度采样
    耐药
    毒素生成

  - 读段如何拼装成基因组？![img](https://api2.mubu.com/v3/document_image/70367a13-5486-4d3f-8bf1-5836ae00f087-12251550.jpg)

  - 重测序（Resequencing）

    基因型和突变的发现

    - 当前测序工作很大一部分主要是针对已有基因组物种的重测序
      单个人的基因组（1000 Genomes Project）
      模式生物：寻找遗传突变（Genetic variation）和拷贝数变异（Copy number variation）等

    - 挑战：
      将数百万个短片段（Reads）快速的回贴到参考基因组上，并估算错误率
      准确的发现SNPs和indels

  - 1000 Genomes Project
    四个种群的179个人的全基因组测序
    两组母亲-父亲-孩子的高覆盖度基因组测序
    七个种群的697个人的外显子测序

  - 深度测序（Deep Sequencing）
    发现或者定量罕见的序列变异
    单个患者体内的HIV突变多样性
    肿瘤样本中的突变
    物种的单核甘酸多样性

- 生物信息学挑战

  Base calling: 根据图像识别碱基
  序列读段回贴到参考序列上
  全基因组的组装
  基因型（Genotype）和SNP的识别
  RNA-Seq数据分析：检测基因表达、可变剪接异构体等
  Chip-Seq数据中的Peak finding，以及受调控基因的回贴

  - 碱基识别（Base calling）

    

    从图像中识别碱基，组成序列

    - 数据格式：FASTQ

      FASTQ格式的序列一般包含四行
      第一行由‘@’开始，后面跟着序列的描述信息
      第二行是序列
      第三行由‘+’开始，后面也可以跟着序列的描述信息
      第四行是第二行序列的测序质量分值（quality values）

      - 质量评价分值Q（Quality values）![img](https://api2.mubu.com/v3/document_image/d92ddb5c-0b63-4daf-8d02-005ec4d12301-12251550.jpg)![img](https://api2.mubu.com/v3/document_image/e9fc562e-de74-4bfd-8da2-e629323bf66c-12251550.jpg)

- 读段

  - 读段回贴

    - Genotyping![img](https://api2.mubu.com/v3/document_image/35ff032c-b990-4bfa-8484-d3940ec485e9-12251550.jpg)

    - RNA-seq, ChIP-seq, Methyl-seq![img](https://api2.mubu.com/v3/document_image/de804f28-1b24-4033-a242-7616ffe77bd6-12251550.jpg)

  - 读段映射
    - 瓶颈：“最优的”比对结果？![img](https://api2.mubu.com/v3/document_image/06f45d78-8064-4302-a7af-6a88b38ee570-12251550.jpg)
      准确性vs. 速度vs. 运算空间

  - 读段比对

    - Short Read Alignment
      给定参考序列和一系列读段
      每个读段：发现至少一个“好的”局部比对

    - “好的”比对![img](https://api2.mubu.com/v3/document_image/eebe03d4-60d8-41d3-a3e8-c515f55a8b60-12251550.jpg)
      错配越少越好
      质量低的碱基错配率高
      质量高的碱基错配率低

- 索引（Indexing）

  

  基因组和读段数据规模太大：不能直接用动态规划算法
  索引是必须的: BANANA$

  - 人类基因组的索引规模![img](https://api2.mubu.com/v3/document_image/026a543e-5411-4d91-ad25-62f28dbeebb9-12251550.jpg)
    合适的索引大小对计算性能很重要
    大的索引：需要更多的内存空间

  - 应用

    - SOAP（Short oligonucleotide alignment program）

      2008年，华大基因

      - “Seed and hashlook-up table”![img](https://api2.mubu.com/v3/document_image/ecd26ba3-25cc-43c4-b22c-5033ec8a4629-12251550.jpg)
        先搜索种子序列：完全匹配
        再根据索引匹配剩余序列
        允许最多两个错配或空位(gap)

      - 种子序列（seed）：
        酵母：L=12Mb，S=10bp, 200 Mb RAM
        人类：L=3Gb，S=12 bp, 14Gb RAM

  - Burrows-Wheeler Transform (BWT)

    

    1994年，Michael Burrows和David Wheeler发明。
    数据压缩算法（bzip2）
    聚类相似的字符：输出能够更容易压缩，相同的字符在一起
    每一轮将最后一列的字符移到第一列
    输出：矩阵的最后一列

    - BWT vs. 后缀数组（Suffix array, SA）![img](https://api2.mubu.com/v3/document_image/0005797c-074b-4f3e-b02d-81b2cefeb1a0-12251550.jpg)

    - Transform

      - T-ranking: 给T中每一个字符赋值（Rank）![img](https://api2.mubu.com/v3/document_image/4ddf4846-b1ed-4620-88ef-efb0e9d7f452-12251550.jpg)

      - BWT(T)的可逆性

        

        - Last first mapping：![img](https://api2.mubu.com/v3/document_image/a762e180-a849-4f5f-882a-8f44a19dde74-12251550.jpg)
          最后一列第ith个出现的字符，是第一列第ith个出现的字符

    - Run-length encoding
      可逆的数据压缩算法
      WWWWWWWWWWWWBWWWWWWWWWWWWBBBWWWWWWWWWWWWWWWWWWWWWWWWBWWWWWWWWWWWWWW -> 12W1B12W3B24W1B14W
      a c a a c g -> 1a1c2a1cg

    - Move-to-front transform![img](https://api2.mubu.com/v3/document_image/770be092-d1fd-4e74-a602-3443fedab4e6-12251550.jpg)
      数据编码的方式
      字符->数字，“Recently used symbols”
      可逆转换：从后往前

  - FM索引（FM Index）

    Full-text index in Minute space（极小空间里的全文索引）
    基于BWT转换前后的字符建立的矩阵

    - 索引的核心部分: F, L![img](https://api2.mubu.com/v3/document_image/c441c1ec-c5ec-4bbd-b481-8559b4536b88-12251550.jpg)
      F可以用数字来代替，例如300, 400, 500, 600，可以表示A300, C400, G500, T600
      L可以被压缩

    - 基于FM索引的精确匹配

      

      - 重复利用规则

        

        用BWT(T)在T中匹配字符串Q

        - 渐进顺序

          

          

          top& bot限制搜索的范围

          - 读段在参考序列的位置

            比对结束后，确定读段在参考序列上的位置

            - 方案1：![img](https://api2.mubu.com/v3/document_image/2f9fd092-dcef-4ae8-bbd4-fa5eb816869e-12251550.jpg)
              从当前位置一直回读到文本的起始

            - 方案2：![img](https://api2.mubu.com/v3/document_image/55c8c68d-3e72-462f-a3ac-1feda00d2764-12251550.jpg)
              将全部的后缀数组载入到内存，直接从数组中找到参考序列上的起始位置

            - 混合方案：![img](https://api2.mubu.com/v3/document_image/0d546a44-8229-4757-a593-346fbf1857f0-12251550.jpg)
              保留部分后缀数组的内容–“Sample”

    - FM索引的检查点

# 转录组与转录调控分析

- 定义

  - 转录组 (Transcriptome)
    细胞内所有RNA 分子，包括mRNA, rRNA, tRNA和其他非编码 (non-coding) RNA

  - 转录调控 (Transcriptional regulation)
    基因调控 (Gene regulation)

- 基因表达分析

  - 快照(Snapshot)
    所有基因的RNA表达水平
    提供大量数据

  - 观察基因表达随生长时期、环境变化的变化（上调或下调）

  - 相同条件下，表达变化的基因可能在功能上有关联

  - 从共表达的基因中找调控模块

  - 表达模式来表征异常的基因调控
    癌症诊断

- 研究技术

  - 转录组

    - 单个实验中检测整个转录组

    - 微阵列/基因芯片（Microarray）

      基于DNA杂交。
      ​

      - 1987，根据免疫测定的 (immunoassay)

      - 1995，高通量、点阵以及Northern 杂交

        - 同时测定细胞内数千个基因的表达情况

        - 将mRNA 反转录成cDNA，与芯片上的探针杂交

        - 最终将被基于测序的方法取代

      - 芯片的体积非常小
        适用微量样品的检测

      - 基因表达情况的定量分析
        将样品中的DNA/RNA 标上荧光标记，可以定量检验基因的表达水平

      -  其他类型的芯片

        - 组织芯片

        - 蛋白质芯片

      - 基因芯片的密度
        100-1 million DNA 探针/1cm^2

      - 基因芯片技术的类型

        - 按技术手段、探针类型分类

          - Short oligonucleotide arrays，短寡核苷酸阵列
            Affymetrix

          - cDNA arrays，cDNA阵列
            Brown/Botstein

          - Long oligo array，长寡阵列
            Agilent

          - Serial analysis of gene expression，基因表达的连续分析
            SAGE

        - 按实验要求分类

          - 单通道 (Single Channel)
             一次检验一种状态

          - 双通道 (Dual Channel)
            差异表达基因的筛选

        - DNA芯片

          - cDNA microarrays

            将500~5,000bp 的cDNA固载到介质上 ( 例如玻璃) 
            ​Stanford 开发设计，通常为双通道

            -  DNA连接到固态载体

              玻璃、塑料或尼龙

              - spotter
                Robot spotter，Commercial DNA spotter

            - 差异表达基因的筛选

            - 点样后的cDNA Microarrays

            - 基因表达的数据

          - DNA chips

            将寡核苷酸探针 (20~80-mer) 合成到芯片上
            ​Affymetrix

            - 寡聚核苷酸链 (Oligonucleotide)
              一般长度为20~25bp
              每个基因设计10~40个不同的寡聚核苷酸链

            -  每个基因寡聚核苷酸链的选择
              在基因组上是唯一的
              不发生重叠

            - GeneChip 的制备
              刻 硅芯片：光刻 (photolithography)
              每次合成一个碱基

          - 铺瓦芯片 (Tiled microarray)

            高度覆盖基因组的某个区域，或整个基因组；
            设计的探针能够覆盖序列上的每一个碱基对；
            一般不包括重复序列；

            - 探针大小和间隔决定芯片的解析度 (Resolution)

          - ChIP-chip

            ChIP：染色质免疫共沉淀，Chromatin immunoprecipitation

            - 蛋白质与DNA 的结合
              转录因子；
              修饰的组蛋白

        - 数据标准化处理

          

          - 图像处理

            - 栅格化
              确定点位置

            - 图像分割（Segmentation）
              点与背景的分离

            - 抽提亮度
              各个像素亮度的均值 (mean) 或中位数(median)

            - 背景校正
              局部或全局

          - 基因表达的定量![img](https://api2.mubu.com/v3/document_image/0720e193-77b4-43ea-b58c-26ceea50f9bd-12251550.jpg)

        - 误差分析

          - 图像分析

          - 扫描

          - DNA 杂交过程
            温度
            时间
            混合均匀程度

          - 探针的标记

          - RNA 的抽提

          - 加样

    - 基于高通量测序

      - RNA-Seq

      - Small RNA-Seq

  - 转录调控

    - 蛋白质-DNA相互作用

    - CHIP-chip芯片

    - 基于高通量测序

      - ChIP-Seq

      - Methyl-Seq

  - 转录组学

    - cDNA芯片

    - 辅瓦芯片（Tiling array）

    - mRNA-Seq