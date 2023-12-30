# 软件安装

三类程序：
- 二进制可执行程序：下载软件包解压后可全路径调用
	- sratoolkit和ncbi的blast软件
- 语言代码
	- C源码：`./configure,make,make install`
	- python：模块依赖的问题，建议直接用conda
- 系统/语言自带软件中心安装器：`apt-get，yum，cpan，cran，brew, pip,conda，docker`
	- pip：`pip install --index-url https://pypi.douban.com/simple cnvkit deeptools HTSeq `
	- conda：也需要设置镜像加速
		- 安装：
			- `wget https://repo.continuum.io/miniconda/Miniconda2-latest-Linux-x86_64.sh`
			- `sh Miniconda2-latest-Linux-x86_64.sh`
		- 安装之后运行`source`激活conda，或者直接添加到环境变量，然后` source  ~/.bashrc` 激活环境变量
		- conda安装软件管理：安装bioconda
		- ```conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free
		  conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/conda-forge
		  conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/bioconda
		  conda config --set show_channel_urls yes
		  conda config --show
		  conda install -y -c bioconda homer
		  conda install -y -c // bioconda 等任何软件，安装之前先搜索了解软件本身```

```
solver: libmamba
channels:
  - https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free
  - defaults
restore_free_channel: true
auto_activate_base: false
```

# 比对

## 序列比对

- bwa, bowtie2, hisat2, subjunc, STAR 
- GCG
- BLAST
- ClustalX  http://bips.u-strasbg.fr/fr/Documentation/ClustalX/, 图形化的多序列比对工具 
- ClustalW  http://www.cf.ac.uk/biosi/resear...loads/clustalw.html, 命令行格式的多序列比对工具 
- GeneDoc  http://www.psc.edu/biomed/genedoc/, 多序列比对结果的美化工具 
- BioEdit  http://www.mbio.ncsu.edu/BioEdit/bioedit.html, 序列分析的综合工具
- WebLogo  http://weblogo.berkeley.edu/logo.cgi, 序列保守性
- Cluster 3.0  http://bonsai.hgc.jp/~mdehoon/software/cluster/software.htm

## 进化树

- MEGA  http://www.megasoftware.net/, 图形化、集成进化分析，物种和基因进化分析，不包括ML
- iTOL  https://itol.embl.de/, 物种和基因进化分析
- 集成的进化分析工具 ：
	- PAUP  http://paup.csit.fsu.edu/, 商业
	- PHYLIP  http://evolution.genetics.washington.edu/phylip.html, 免费
- ML建树工具：
	- PHYML  http://atgc.lirmm.fr/phyml/, 最快
	- Tree-puzzle  http://www.tree-puzzle.de/, 较快
	- PAML  http://abacus.gene.ucl.ac.uk/software/paml.html
	- PALM
- 基于贝叶斯方法的建树工具：
	- MrBayes  http://mrbayes.csit.fsu.edu/
	- MAC5  http://www.agapow.net/software/mac5/
- TreeView  http://taxonomy.zoology.gla.ac.uk/rod/treeview.html, 进化树显示工具
- Maple Tree  http://mapletree.sourceforge.net/

# 测序数据分析

- 基因预测：
	 - MEME  http://meme-suite.org/
	 - GenScan  http://genes.mit.edu/GENSCAN.html
- HMMalign  http://www.biology.wustl.edu/gcg/hmmeralign.html
- COMBAT, 去除批次效应 (Batch removal)
- NGS for DNA-seq:
	 - FastQC
	 - BWA
	 - STAR
- RNA-seq:
	 - RSeQC
	 - Salmon
	 - DESeq2
- ChIP/DNase-seq:
	 - MACS
	 - Cistrome
- Seurat, scRNA-seq and scATAC-seq
- MAESTRO, scATAC-seq
- Mutect, Genome-resequencing
- MAGeCK, CRISPR screens

质量控制工具：fastqc, fastx_toolkit, cutadapt, TrimGalore, RSeQC或者RNA-SeQC, qualimap, skewer, NGScheckmate

# 生物分子网络分析

- Cytoscape  http://www.cytoscape.org/
- 基因调控网络： 
	  - GeneNetwork  http://gn2.genenetwork.org/
	  - Cytoscape  https://cytoscape.org/
- 代谢通路：
	  - KEGG  https://www.kegg.jp/
	  - iPATH  https://pathways.embl.de/
- 蛋白和小分子互作数据：
	  - STITCH  http://stitch.embl.de/
	  - STRING  http://string-db.org
- Ontology and pathway
	  - DAVID
	  - GSEA

找变异：GATK, Platypus, VarScan, LoFreq, FreeBayes, SNVer, SAMtools, VarDict, cnvkit, sequenza

计数： bedtools, htseq-counts, FeatureCounts, salmon

差异分析的R包：limma, DEseq2, edgeR
- 差异表达分析及可视化：ballgown

重构转录本：stringTie

可视化：
- Genome Browser  http://genome.ucsc.edu/, 基因组可视化
- Echart  https://www.echartsjs.com/examples/zh/index.html, 生物数据可视化
- IGV

分子结构：
- 分子动力学模拟：
	  - GROMACS
	  - NAMD
- 降维、分子结构等分析
	  - PCA analysis  http://biit.cs.ut.ee/clustvis/
	  - DREAM Challenge  http://dreamchallenges.org/

生物数据分析平台
- Galaxy  https://usegalaxy.org/

免疫学 (Immunology)：
- Polysolver
- NetMHC
- TIMER
- TRUST
- TIDE

基因芯片检测分析：
- ScanArray
- Array-Pro

绘图：ggplot2+ggpubr包

其他：deeptools