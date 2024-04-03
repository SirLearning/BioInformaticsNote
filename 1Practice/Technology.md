# 序列测定

## 初代测序

Herbert Boyer (1972)

Chemical sequencing：Maxam-Gilbert (1977)
- 碱基识别系统：
	- G系统：pH 8.0 ：硫酸二甲酯 → G → m7G →C8~N9断裂 →脱G
	- A + G系统：pH 2.0 ：哌啶甲酸（pidine）→ 嘌呤环 N质子化→脱嘌呤
	- C系统：1.5 mol/L NaCl C + 肼（hydrazine）→ 脱C
	- T + C系统：肼(hydrazine) → 打开嘧啶环 →重新5C环化→脱嘧啶
- 流程：
	1. 用限制性内切酶把DNA切成100—200 bp 测序片段
	2. 用碱性磷酸化酶处理，消除5‘末端上的磷酸
	3. 在5‘-OH端标记32P，用多核苷酸磷酸激酶催化，标记片段变性为单链
	4. 化学试剂在特定碱基位置降解单链DNA，产生一组长度不等的DNA片段
	5. 经电泳和放射性自显影后，从4个反应系统统一阅读， 待测DNA的全部核苷酸序列就可直接读出

双脱氧链终止法测定单链DNA序列 (Dideoxy sequencing method)：Sanger (1977)
- 原理：DNA聚合酶用单链DNA作为模板，以双脱氧核苷三磷酸作底物，将其聚合到新生寡核苷酸链的3‘-末端，从而终止其延伸反应
- 流程：
	1. 获得单链DNA模板，克隆并扩增待测DNA片段，使其变性
	2. 选择与DNA单链互补的短链引物，将引物用放射性同位素标记
	3. 引物先同单链模板复性，在四个反应管中分别加入待测DNA单链模板、互补引物分子、四种dNTP、DNA聚合酶 (Klenow 酶)以及不同的ddNTP
	4. 进行聚合反应 ，DNA新生链延长，当掺入ddNTP时，聚合反应终止
	5. 在聚丙烯酰胺凝胶或琼脂糖凝胶中电泳，根据X底片对凝胶曝光所显的条带位置，读出 DNA序列

全自动DNA测序：实现了凝胶电泳、初始数据获取、碱基阅读等步骤自动化
- 1980s，Leroy Hood发展了为4种终止核苷酸碱基标定不同荧光颜色的方法，改进了测序技术
- 设计原理：采用荧光标记DNA片段，并用激光激活的荧光探测系统，检测序列反应的分离产物，读出电泳条带所示的碱基顺序
- 分离产物的两种基本方法：
	- 单荧光标记四泳道法
	- 四标记单泳道法：ABI公司（美国应用生物系统公司）开发
		1. 用4种不同的荧光标记物标记4个反应的引物，4个反应在一个泳道中电泳分离
		2. 每个反应产物用不同颜色的荧光标记进行区分，再用计算机将经过荧光探头的不同颜色顺序转变成测序信息
		3. 这种同一泳道的分离避免了泳道间差异对测序的影响
- 仪器变化：
	1. 377测序仪、Megabace，3700、3730测序仪：毛细管电泳（根据分子量区分单个碱基）
	2. Solexa测序仪：捕捉每个cluster上不同的荧光信号
- 自动测序仪：四种颜色，直接阅读四种碱基
	- Model 370A DNA Sequencing System
	- ABI (Applied Biosystems, Inc) 370

## 二代测序

技术难点：
- 需要高分辨率图像处理系统
- 原始数据的图像规模：TB级（ABI-SOLID > Solexa >  454）

illumina/Solexa：
- 最早由Solexa开发设计，现在是Illumina的子公司
- Sequencing by synthesis
- Hiseq

Roche 454：2005年底，焦磷酸测序法
1. Genome Sequencer 20 System/GS FLX+ System：开创边合成边测序(sequencing by synthesis) 的先河
2. 文库构建：
	   1. 借助基因工程技术，将A和B接头（3’和5’端具有特异性）连接到DNA片段上
	   2. 接头也将用于后续纯化、扩增和测序步骤，变性处理回收单链的DNA（sstDNA），具有A、B接头的单链DNA片段组成了样品文库
3. 乳液PCR：
	1. 一个DNA片段＝一个磁珠：单链DNA文库被固定在特别设计的DNA捕获磁珠上；每一个磁珠携带了一个独特的单链DNA片段
	2. 磁珠结合的文库被扩增试剂乳化，形成油包水的混合物，这样就形成了只包含一个磁珠和一个独特片段的微反应器
	3. 乳液PCR扩增：每个独特的片段在自己的微反应器里进行独立扩增。整个片段文库的扩增平行进行，对于每一个片段而言，扩增后产生了几百万个相同的拷贝
	4. 随后，乳液混合物被打破，扩增的片段仍然结合在磁珠上
	5. 磁柱放入 PicoTiter 板进行测序：
		1. 一个磁珠=一条读长：携带DNA的捕获磁珠随后放入“Pico Titer Plate”（PTP）板中，进行后继的测序；PTP孔的直径（29 um）只能容纳一个磁珠（20 um）
		2. 将PTP板放置在GS FLX中，测序开始；放置在四个单独试剂瓶里的四种碱基，依照T、A、C、G的顺序依次循环进入PTP板，每次只进入一个碱基；如发生碱基配对，就会有一分子的光信号；由此一一对应，就可准确、快速确定待测模板的碱基序列，释放一个焦磷酸
		3. 焦磷酸在ATP硫酸化酶和萤光素酶的作用下，经过合成反应和化学发光反应，最终将萤光素氧化成氧化萤光素，同时释放出光信号
		4. 释放的光信号实时被高灵敏度CCD相机捕获，有一个碱基和测序模板进行配对，就会捕获

ABI-SOLiD：SOLID
- GA与Solexa：最早由Solexa研发，后illumina收购Solexa
	- 型号：GAI -> GAII -> GAIIx -> HiSeq2000
	- 产量: 1G -> 35G -> 85G -> 200G
- 流程：
	1. 文库制备：将基因组DNA打成几百个碱基（或更短）的小片段，在片段两个末端加上接头(adapter)
	2. 产生DNA簇：利用专利芯片，其表面连接有一层单链引物；DNA片段变成单链后通过与芯片表面的引物碱基互补被一端“固定”在芯片上。另外一端（5’或3’）随机和附近的另外一个引物互补，也被“固定”住，形成“桥(bridge)“。反复30轮扩增，每个单分子得到扩增，成为单克隆DNA簇
	3. DNA簇产生后，扩增子被线性化，测序引物随后杂交在目标区域一侧的通用序列上
	4. 测序：Genome Analyzer系统应用了边合成边测序原理
		1. 加入改造过的DNA聚合酶和带有4种荧光标记的dNTP，因为3’羟基末端带有可化学切割的部分，只容许每个循环掺入单个碱基。此时，用激光扫描反应板表面，读取每条模板序列第一轮反应所聚合上去的核苷酸种类
		2. 之后，将这些基团化学切割，恢复3’端粘性，继续聚合第二个核苷酸，如此继续下去，直到每条模板序列都完全被聚合为双链
		3. 统计每轮收集到的荧光信号结果，就可得知每个模板DNA片段的序列。目前的配对末端读长可达到2×50 bp，更长读长也能实现，但错误率会增高。读长会受到多个引起信号衰减的因素所影响，如荧光标记的不完全切割
		4. 加入DNA聚合酶和被荧光标记的dNTP 和接头引物进行扩增，在每一个测序列簇延伸互补链时，每加入一个被荧光标记的dNTP就能释放出相应的荧光，测序仪通过捕获荧光信号，并通过计算机软件将光信号转化为测序峰，从获得待测片段的序列信息

### Next generation sequencing (NGS)

sequencing steps/pipeline:
1. library preparation
	- 加DNA – 碎片化 – 加接头end repair & adaptor ligation (连接复制) – 碎片库
2. library amplification 碎片与板子上特定位点的吸附 – 连接 – 合成, 延伸(束状生长)
3. parallel sequencing 
4. data analysis

Illunina data processing
1. nucleotide flows – raw images
2. image processing – base-calling – quality filtering – .bcl
3. 质控(截掉质量值不好的测序结果) – Illumina fastq

## 三代测序

与前两代相比，是单分子测序，测序过程无需进行PCR扩增

PacBio (Pacific Biosciences): SMRT
1. 基本原理： DNA聚合酶和模板结合，4色荧光标记 4 种碱基；在碱基配对阶段，不同碱基的加入会发出不同光，根据光的波长与峰值可判断进入的碱基类型
2. DNA 聚合酶是实现超长读长的关键之一，读长主要跟酶的活性保持有关，它主要受激光对其造成的损伤所影响
3. 技术的关键：将反应信号与周围游离碱基的强大荧光背景区别出来
	1. 利用零模波导孔原理：如同微波炉壁上可看到的很多密集小孔，如果小孔直径大于微波波长，能量就会在衍射效应的作用下穿透面板而泄露出来，从而与周围小孔相互干扰；如果孔径小于波长，能量不会辐射到周围，而是保持直线状态（光衍射原理），从而可起保护作用
	2. 在一个反应管（SMRTCell：单分子实时反应孔）中有许多这样的圆形纳米小孔（零模波导孔），外径 100纳米，比检测激光波长小(数百纳米)，激光从底部打上去后不能穿透小孔进入上方溶液区，能量被限制在一个小范围里，正好足够覆盖需要检测的部分，使得信号仅来自这个小反应区域，孔外过多游离核苷酸单体依然留在黑暗中，从而实现将背景降到最低
	3. 通过检测相邻两个碱基间的测序时间，来检测一些碱基修饰情况，如果碱基存在修饰，则通过聚合酶时的速度会减慢，相邻两峰之间的距离增大，可通过这个来之间检测甲基化等信息
	4. SMRT技术测序速度很快，每秒约10个dNTP。但其测序错误率比较高（是目前单分子测序技术的通病），达到15%；出错是随机的，第二代测序技术存在测序错误的偏向，因而可通过多次测序来进行有效的纠错

BGISEQ-50：一款更专注、更小巧、更精简的高通量测序平台
- 该系统沿用了先进的联合探针锚定聚合技术（cPAS）和DNA纳米球（DNB）核心测序技术，内置独立的样本加载试剂槽和全自动试剂针穿刺系统。BGISEQ-50体积小巧，易于安放，不仅全面支持临床领域和科研领域的基础测序应用项目，而且适用范围广泛，突破空间限制，即使在高海拔下的低气压环境中也能正常运行

Oxford Nanopore Technologies: lon Torrent

纳米孔技术

## 应用：

基因组学(genomics):
	- 全基因组测序 whole genome sequencing(WGS)
	- 全外显子测序 whole exome sequencing(WES)
	- 数据分析：
		- 点突变/插入缺失标记/复制数变异/结构变异

### Transcriptome and RNA-seq analysis

RNA测序 (RNA-Seq)
- 原理：
	- 大型平行测序
	- complementary DNA(cDNA) – next-generation short read technologies
	- reference genome – transcriptome map
- 流程：
	1. 实验设计
		- 分组(control和实验组)
		- 物种(organism): novel/non-model/genome-sequenced/model
	2. 样品准备
		1. 提取poly-A RNAs
			- polyA selection
			- rRNA depletion – ribozero/ribominus
		2. 转换成ds-cDNA and shearing
		3. 亲和吸附 – adapter连接
	3. 测序：
		- single end (SET)
		- paired end (PET)
	4. data quality control
	5. RNA-seq reads – 数据分析
		- mapping reads – reference genome
		- visualization(Gbrowser)
		- de novo assembly
		- quantification
	6. differential expression analysis – reference transcriptome
- 结果：
	- 基因/转录/外显子表达，选择性剪切，基因融合，单核苷酸变异
	- 新的转录区域，Allele-specific expression，RNA编辑，非模式生物的转录组
- 优势：
	- 不需要已存在的序列 – reads很清晰 – 分辨率高 – 高生产量 – 可以揭示序列变异(SNPs)

sRNA(small RNA)测序
- 数据分析：
	- 表达差异化/基因融合/选择性剪切/RNA编辑
	- RNA测序分析：
		- RNA types
		- phenotypes
		- transcriptome
			- gene structure
			- 选择性剪切(alternative splicing)
- evolution:
	1. gene expression profiling – spotted cDNA microarray – 已知基因的表达水平
	2. whole genome expression profiling – tiling array – 辨识和检测新基因和剪切变异体
	3. mRNA测序 – NGS – mRNA-seq

### 表观遗传学(epigenomics):

ChIP-seq/ChIP-exo

CLIP-seq

Bisulfite-seq

数据分析：
- 甲基化/组蛋白修饰/转录因子结合

### single cell sequencing (sc) 单细胞测序

FastQC – quality

dup

# 生物芯片

主要的芯片平台
- 按照公司来区分：affymetrix，agilent和illumina，还有罗氏
- 按照应用来区分，表达芯片，基因分型芯片，拷贝数芯片
- 其它定制化芯片

# 基因组组装

Oligo-FISH (oligonucleotides fluorescence in situ hybridization): 
- detection of chromosome variation
- identification of allopolyploid
- deciphering of 3D genome structures

# 后处理

基因型填充 (Genotype-Imputation)

