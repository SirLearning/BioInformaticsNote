# 先验

## 数据存储

数据格式：sam, bam, vcf, bed, MAF
- 序列文件：
	- *fasta* (缩写为*fa*)：存储核酸或氨基酸序列，允许在序列前定义名称和编写注释。 已成为生物信息学的标准格式，格式简单，多种文本处理工具和 Python等脚本语言处理均可对其直接处理
		- 结构分两行：
			- 第一行序列标识（ID）
			- 第二行为序列信息。
		- fna,ffn,faa都属于fasta格式：
			- *fna (fasta nucleic acid file)*: 所有核酸序列信息
			- *ffn (fasta nucleotide coding regions file)*: 所有基因的核酸序列信息
			- *faa (fasta Amino Acid file)*: 即所有基因对应的蛋白质序列信息
	- *fastq* (缩写为*fq*)：是一种存储生物序列和对应序列质量，现已成为存储高通量测序数据的事实标准，相当于fasta的plus (+quality) 版
		- 结构分为四行：
			- 第一行序列标识（ID）
			- 第二行为序列信息
			- 第三行为单独一个+（表示与第一行相同的序列标识，为了节省内存省略为+，此行保留以凑成偶数行保证后续数据处理的便捷性）
			- 第四行，对应第二行序列的质量值（用ascii码表示，通过质量值公式可以计算其准确度）
	- *fai*：提供随机访问fasta/fastq文件的接口
		- 格式：以\t分割，fasta 5列，fastq 6列
			- NAME: Name of this reference sequence
			- LENGTH: Total length of this reference sequence, in bases
			- OFFSET: Offset in the FASTA/FASTQ file of this sequence's first base
			- LINEBASES: The number of bases on each line
			- LINEWIDTH: The number of bytes in each line, including the newline
			- QUALOFFSET: Offset of sequence's first quality within the FASTQ file
- 基因组注释文件：gff, gtf，高通量测序中对已经map到参考基因组的reads做注释
	- *GFF (general feature format)*：用于基因组注释，目前是第三版`.gff3`
		1. seqid ：通常格式染色体ID或是contig ID
		2. source：注释的来源，一般指明产生此gff3文件的软件或来源数据库。如果未知，`.`代表空
		3. type： 一般使用gene，repeat_region，exon，CDS，或SO对应编号等
		4. start：起始位置，从1开始计数（需要注意：bed文件从0开始计数
		5. end：终止位置
		6. score：得分，注释信息可能性说明，可以是序列相似性比对时的E-values值或者基因预测是的P-values值。`.`代表空
		7. strand：`＋`表示正链，`－`表示负链，`.`表示不需要指定正负链，`?` 表示未知
		8. phase ：仅对编码蛋白质的CDS有效，本列指定下一个密码子开始的位置。可以是0、1或2，表示到达下一个密码子需要跳过碱基个数
		9. attributes：包含额外属性的列表，格式为`tag=value`，不同属性之间以`;`相隔
	- *GTF (gene transfer format)*：用于对基因的注释
		1. seqname: 通常格式染色体ID或是contig ID
		2. source：注释的来源。，一般指明产生此gff3文件的软件或来源数据库。如果未知，.代表空
		3. start：起始位置，从1开始计数
		4. end：终止位置
		5. feature ：表示基因结构。CDS，start_codon，stop_codon是一定要含有的类型
		6. score ：得分，注释信息可能性说明，可用`.`代替空
		7. strand：链的正向与负向，分别用`+`和`-`表示
		8. frame：密码子偏移，可以是0、1或2
		9. attributes：必须要有以下两个值：
			- gene_id value: 表示转录本在基因组上的基因座的唯一的ID。gene_id与value值用空格分开，如果值为空，则表示没有对应的基因
			- transcript_id value: 预测的转录本的唯一ID。transcript_id与value值用空格分开，空表示没有转录本

参考基因组、基因组注释：
- 人体基因：数量，分类，基因结构
- genecard
- TCGA
- ENCODE
- GTEx
- 基因集注释数据库：GO terms/Pathway (KEGG, BIOCARTA,Reactome)  MSigDB


数据库集合网站：NAR Database Category List

大型数据库网站：
1. NCBI
2. EBI
3. 
4. NGDC（BIGD）

数据库使用注意事项：
1. 安全问题：不要将公司或者是私人信息发送到web server
2. 科学可重复性：
	- 记录使用的数据库
	- 记录使用的程序
	- 记录程序版本号
	- 记录序列的accession numbers：在不同的database中会有不同，所以要记录database IDs以及选取最大的一个数据库。
	- 记录程序参数 -- 写lab book
3. 保存：
	- Flashy graphs: 发表以及查看
	- ASCII(text) files: 之后的工作
		- MSAs: xxxx.aln
		- Trees: xxx.dnd, xxx.ph
4. 检查不同程序的边界值(borderline results)：检查其准确性
	- 多用几个程序，来缩小误差概率，最后的结果用一致性检验和一致的方法来做对比和取最佳结果（consistency-checking; consensus approach）
5. 注意unpublished methods（当然发行过的也不一定是好的）
6. Data选用新的最好
7. 大多数资源对学术是free的，但面向公司的都是付费的。

构建数据库需要注意的事情：
- 抢占先机: clustalw
- 持续维护: PlantTFDB, AnimalTFDB
- 软件和数据库的依赖性: OS

## 文献检索

引文网站：
- NCBI Pubmed: articles
- Web of Science

学术搜索：
- Google scholar
- Google or bing.com

出版社：
- Springer-Nature
- Elsevier Science
- HighWire Press
- Wiley Press
- Oxford

文献管理：
- Endnote
- Zotero

# 国际数据中心

## NCBI

NCBI e-utilities:
- Search, link, and download sequences of genebank programatically

Batch Entrez: 
- 输入一个Entrez accession numbers的文件，会输出下载所有的有关记录

使用：
- 最常研究的DNA功能片段叫什么

NCBI Gene: integrates information from a wide range of species
- Nomenclature：术语
- Genomic：基因组信息
- Expression
	- GEDS: gene expression display server
- Biblography: 相关文章
- GeneRIFs: gene reference into functions
- Pathways from Pubchem
	- Wikipathways: 生物学通路数据库
	- Reactome
- Maps
- Interactions: 相互作用
- variations：突变体
	- Genotypes
	- SNP
- Phenotypes: 表型
- Disease:
	- OMIM: 人类基因和基因表型的汇总，内容较深刻
		- a comprehensive, authoritative compendium of human genes and genetic phenotypes
	- OMIM-PCNA
- General gene information
	- Markers: 标记
	- Pseudogene(s): 假基因
	- Homology: 直系同源
	- Ontology: 功能（如药用）
- RefSeqs
	- 转录型（可变剪切）
	- Genomic: 基因组信息
	- Related sequences
	- RefSeq ID: 
		- NM_xx, NP_xx, NR_xx, NC_xx
		- 小数点后有数字才是唯一的mRNA序列，这个是版本号


| Accession prefix |                        Molecule type                         |                           Comment                            |
| :--------------: | :----------------------------------------------------------: | :----------------------------------------------------------: |
|       AC_        |                           Genomic                            |    Complete genomic molecule, usually alternate assembly     |
|       NC_        |                           Genomic                            |    Complete genomic molecule, usually reference assembly     |
|       NG_        |                           Genomic                            |                  Incomplete genomic region                   |
|       NT_        |                           Genomic                            |           Contig or scaffold, clone-based or WGSa            |
|       NW_        |                           Genomic                            |              Contig or scaffold, primarily WGSa              |
|      NZ_^b^      |                           Genomic                            |           Complete genomes and unfinished WGS data           |
|       NM_        | [mRNA](https://www.ncbi.nlm.nih.gov/books/n/handbook/A1237/def-item/app114/) |         Protein-coding transcripts (usually curated)         |
|       NR_        | [RNA](https://www.ncbi.nlm.nih.gov/books/n/handbook/A1237/def-item/app158/) |                Non-protein-coding transcripts                |
|      XM_^c^      | [mRNA](https://www.ncbi.nlm.nih.gov/books/n/handbook/A1237/def-item/app114/) |          Predicted model protein-coding transcript           |
|      XR_^c^      | [RNA](https://www.ncbi.nlm.nih.gov/books/n/handbook/A1237/def-item/app158/) |        Predicted model non-protein-coding transcript         |
|       AP_        |                           Protein                            |             Annotated on AC_ alternate assembly              |
|       NP_        |                           Protein                            |           Associated with an NM_ or NC_ accession            |
|      YP_^c^      |                           Protein                            | Annotated on genomic molecules without an instantiated transcript record |
|      XP_^c^      |                           Protein                            |      Predicted model, associated with an XM_ accession       |
|       WP_        |                           Protein                            |      Non-redundant across multiple strains and species       |
- ^a^ Whole Genome Shotgun sequence data.
- ^b^ An ordered collection of [WGS sequence](https://www.ncbi.nlm.nih.gov/books/n/handbook/A1237/def-item/app195/) for a genome.
- ^c^ Computed.

- links to:
	- HomoloGene
	- Genetic Variations:
		- SNP(single nucleotide polymorphism): 单链多态性
			- SNP
			- SNP: geneview
		- Variation viewer:
			- SV(structural variation)
			- CNV(copy number variation)
		- ClinVar: 有关人类健康的基因组变异
		- dbVar: 人类基因组结构变异数据库
		- Mutation
	- Genome
	- phenotype
	- locus-specific resources worldwide.

GeneCards: 人类基因数据库

EBI：维护着世界上最全面的分子数据资源

​	EBI sequence analysis

​		MSA,

​		EMBOSS: The European Molecular Biology Open Software Suite

## EBI

## SIB Expasy

## Ensembl

## UCSC

## NGDC (BIGD)

国家生物信息中心 (CNCB)

原始测序数据归档库：genome sequence archive(GSA)

- 特点：在国内，更加快速
- 数据库：
	1. 基因组序列库：genome warehouse
	2. 基因组变异库：genome variation map
		- dbSNP & dbVar: 不再接收非人类的突变数据
	3. 2019新型冠状病毒信息库
	4. 基因表达数据库：gene expression nebulas
	5. 人类长非编码RNA数据库
	6. 甲基化数据库：methbanl
	7. 脑疾病知识库：brainbase
	8. 特色物种基因库

- 工具：
	- 生物大数据算法与工具
		- CloudPhylo:
		- Identification of long non-coding RNAs based on feature relationship
	- 生物大数据跨库搜索引擎：BIG Search

生物多样性多维数据资源平台

精准医学多维数据资源平台

# Gene

## 基因结构

### 测序 – 注释

注释 Annotation: 用计算机和实验的方法来标注基因组
- Four levels of annotation：预测(where)、相似性(like)、结构域(do)、通路作用(pathway)

Genes: 
- Types:
	- RNA genes: tRNA, rRNA, snRNA, snoRNA, microRNA
	- Protein coding genes:
		- Prokaryotic gene model 原核基因结构: ORF-genes
			- small genomes, high gene density: Haemophilus – 85% genic
			- Operons: one transcript, many genes
			- No introns: one gene, one protein
			- Simpler regulatory features
			- Open reading frames: One ORF per gene(start – stop condon)
		- Eukaryotic gene model 真核基因结构 : spliced genes
			- Posttranscriptional modification 后转录修饰: 5’-CAP – polyA tail
				- acceptor site – donor site
			- ORF: mature mRNA, all internal exons
				- UTRs: pre-start, post-stop
			- multiple translates
- Human gene: 22K genes code for about 100,000 protein
	- Karyotyoe: 46, linear
	- Genomic sequence features:
	- seqence type: 
		- Repeats(junk DNA): about 50%
			- RepeatMaster
		- coding genes: 20,338(Ensembl) 1%, 1/3为多拷贝
			- transcripts: 200,000
			- Consortium(35,000), Celera(30,000), Affymetrix(60,000), Incyte and HGS(over 120,000), GenBank(49,000), UniGene(>89,000)
			- intron: 30bp～数十kb不等，内含子的平均长度3413.1bp
			- exon: 一般不长于800bp, approximatedly 180,000
				- flanking untranslated regions(5’ UTR and 3’ UTR)
				- Exon with 3’UTRs str c
				- on average 9 exons per gene
			- mRNA剪接位点（Splicesites）：GT－AG法则（内含子）
				- 5’端大多数是GT（称为donorsite）开始
				- 3’端大多数是AG（称为acceptorsite）结束
		- Pseudo genes: 14,638 假基因，会对找寻真基因造成困扰
		- Non-coding RNAs (ncRNA): tRNA, rRNA, snRNA, snoRNA, miRNA
		- tRNASCAN-SE 一个perl脚本，整合了tRNAscan, EufindRNA, Cove三个独立的tRNA检测软件
	- Mitochondrial genes: 37(code for 22 tRNAs, 13 proteins and 2 tRNAs)
	- microbiome flora

Karyotype 染色体组

Statistics:

Human genome:
- Haploid(单倍体) nuclear genome size (3.0×10<sup>9</sup>)
- Highly conserved regions：
	- Coding DNA covers about 30 Mbp (1%)
	- Other regulatory regions cover about 100 Mbp (3%)
- Repetitive DNA covers more than 50%
- Segmental duplication: more than 5%
- Endogenous(外源) retroviral(逆转录病毒) genomes (ERVs): 5-8% (inherited 遗传的)
- Other associated genomes
	- Mitochondrial genome: about 16.5 Kbp, circular genome
	- Viral(病毒) genomes (transfected exogenous Retroviruses)
	- Microbiome 微生物群 (~3,000 microbes are estimated to harbor(隐藏在) human body)

Human gene/protein:
- About 22K genes code for about 100,000 proteins in human
- Mitochondrial genes: 37 (code for 22 tRNAs, 13 proteins and 2 rRNAs)
- About 3.5 million genes encoded by about 3000 microbiome flora
	- Oral microbiome, gut microbiome, etc.
- Coding genes: 20,338 (source Ensembl)
- Pseudogenes: 14,638
- Gene transcripts: 200,000

Human exome(外显子组):
- Some exome capture kits：
	- protein coding regions
	- the flanking untranslated regions (5'UTR and 3'UTR)
- Exome studies usually include all the protein coding regions covering about 30 Mbp of DNA (~1%)
- Human genome has approximately 180,000 exons
- On average there are 9 exons per gene, but the number varies by gene length, which ranges from 1-363. The Titin gene (TTN) has 363 exons.
- Average exon length is about 122 bp

Sequence of an organism's genome:
- Genes
- Exon boundaries & splice sites
- Beginning and end of translation
- Alternative splicing
- Regulatory elements
	- Promoters

## 基因预测

基因预测（Gene Prediction）
- Ab initio 从头预测: 基于统计规律或信号检测
	- 编码区域字符上下文特殊
	- 氨基酸同义密码子选择的偏好性
	- 基因结构特定位点信号识别基因：
		- 剪切信号: splice sites, GT-AG
		- 起始密码子: start site/codon(ATG)
		- 终止密码子: stop site/codon(TAA, TAG, TGA)
		- 启动子: initial
		- 终止子: terminal
- 同源预测: 基于相似性比较
	- 基于功能的相似性
	- 编码序列比组成型序列更加保守
- RNA-seq, EST 表达数据: 基于表达数据
	- 二代测序RNA-seq：组装获得完整基因
	- 三代测序RNA-seq：可直接获得部分表达基因的完整序列
	- PCR获得的RNA及EST序列：可用于验证基因

基因识别（Gene Identification）
- Promoter,
- transcription start, 
- 剪切位点识别: Splice signals(GT, AG)
	- Acceptor site: 3', AG
	- Donor site: 5', GT
- Poly-A site(多腺苷化信号识别),
- 蛋白编码区的识别, 
- Intron/exon
- 核糖体亚单位：

基因寻找(Gene Finding), Signal detection: : promoters, start/stop condons, splice sites…
- Methods
	- Consensus strings
	- Pattern recognition
	- Weight matrices(矩阵) -- score
	- Weight array matrices
	- Maximal dependence decomposition(MOD)
	- Hidden Markov Models(HMM)：
		- 典型基于HMM的基因预测系统：
			- VEIL
			- HMMgene
			- GeneMark.hmm
			- Genie
			- GENSCAN
		- Simple HMM M for gene detection: 'in exon' and 'in intron'
	- Neural Networks(NN)
- Splice site detection: weight matrices -- hidden markov models

基因注释（Gene Annotation）

生物学信息：
Genome database: HGP (human genome project)

## Ensembl: 欧洲

Ensembl Genes: protein/mRNA + sequence assembly
- base: UniPort/Swiss-Prot, UniProt/TrEMBL, NCBI RefSeq
- Flow
	- align species-specific protein
	- align similar proteins (related species)
	- add UTRs using mRNA information
	- build transcripts using mRNA evidence – build additional transcripts using ab initio predictors and homology evidence
	- combine gene annotations with alternative transcripts
- ID:
	- human: ENSG/T/P/E### (gene/transcript/peptide/exon)
	- other species like Mus musculus: ENSMUSG/T/P/E###
- gene structure:
	- UTRs: no UTRs, UTRs annotated
- database: species – 300多个基因组
- Human Genome:
	- genome assembly
	- comparative genomics
	- regulation
	- gene annotation
	- variation
- 3 level browse:
	- Gene
		- summary: gene alleles
			- plice variants
		- sequence: secondary structure
		- comparative genomics: 
			- genomic aligments, 
			- gene gain/loss tree, 
			- orthologues
		- ontologies: GO(gene ontology)
		- phenotypes
		- genetic variation
			- Variant: table/image
		- regulaton: ENCODE, Tarbase
		- external references
		- ID history
		- export data
	- Transcript: show transcript table
		- RefSeq match
		- transcript level
		- sequence: exons, cDNA
		- variant table
	- Protein
		- domain feature
- Tools:
	- assembly converter
	- ID history converter
	- BioMart: search engine, data-mining tool
		- search item: 
			- human gene (IDs), chromosome, base pair position
		- attribute
		- filters
		- data sets:
			- Ensembl genes, Vega genes, SNPs
			- Markers, Phenotypes, expression, ontology, homology presictions, annotation
		- know the IDs of one gene in both Ensembl and MGI(markersymbol ID)
		- HapMap
	- BLAST(basic local alignment search tool)
	- BLAT(BLAST-like alignment tool): faster
		- 对基因组做
	- variant effect presictor: 
		- analyse variants
		- 预测变异的潜在影响
		- 搜索匹配已知变异
- sister sites: different species
- open source – user projects with own data
- pre and archive sites

## Ensembl biomart



# Genome

## NCBI genome

直接查询，dataset下载

进入FTP站点查看最全的参考基因组数据：[Index of /genomes (nih.gov)](https://ftp.ncbi.nlm.nih.gov/genomes/)

## UCSC genome browser

美国

select:
- species
- appropriate assembly
- gene

result:
- genome location
- gene ID and sequence
- expression
- found from different cell lines
- DNase I hypersensitivity clusters
- DNA conservation
- aa conservation
- SNPs in dbSNP
	- synonymous, missense or splice variants, intronic, UTR
- repetitive or complexity regions

Transcript details

Track groups:
- mapping and sequencing
- genes and gene predictions
- phemotype and literature
- EST
- regulation
	- ENCODE (DNA元件百科全书): 描述功能性元件
		- ENCODE cCREs (candidate cis-regulatory elements): 
			- subset of representative DNase hypersensitive sites
		- ENCODE regulation tracks
			- TF ChIP

Tools
- my data – custom tracks / add custom tracka
	- BED (browser extensible data): positonal annotations
		- ChIP-seq signal for TF binding
		- required field:
			- chrom
			- chromStart
			- chromEnd
	- GFF: DNA功能片段注释 – posions of all data items in a limited gene transfer format
	- wig(gle): continuous signal data
		- DNase I HS, ChIP-seq signals
	- BAM: alignments of seq
		- RNA-seq alignments
	- VCF (variant call format): variation data format
		- SNPs, ExAC data

integrative gennomics viewer (IGV): view next generation sequencing data
- loading large datasets (>~100mb) and a large number of samples

ExAC browser (exome aggregation consortium)
- looking up contextual information for NGS data such as allele frequencies

UCSC genome browser
- 找注释，只有很少的 small files

## UCSC Table Browser

作用：advanced searching

Tables – Table brower
- Genomes
- Data
- Location
- Filter and intersect
- output

create a custom track:
- define track characteristics
- define browser characteristics
- format the data
- upload and view the track in genome browser

track characteristics:
- pairedReads: default view is pack
- Gap: default view of other tracks set

## DOE Joint Genome Institute (JGI)

bioenergy research at JGI

program:
- fungal genomics program
	- MycoCsm
- metagenomics(宏基因组学) program
- microbial genomics program
	- Archaea
	- Bacteria
- plant genomics program
	- phycocosm – algal genomics

Genome DB for one organism

# Protein

## Protein database

### general protein databases

Expasy (SIB) – UniProtKB/Swiss-Prot
- UniPort knowledgebase – uniprotkb

TrEMBL – translated EMBL – UniProtKB/TrEMBL
- 有 high-quality computationally analyzed records
- enriched with automatic annotation
- translations of annotated coding sequences from
	- EMBL-bank
	- genbank
	- DDBJ nucleotide sequence database
- from PDB
- from gene prediction
	- Ensembl
	- RefSeq
	- CCDS

UniProt
- UniPortKB (uniprot knowledge base)
	- 两类：
		- uniprotkb/swiss-prot: manually annotated and reviewed
		- uniprotkb/TrEMBL: automatically annotated
	- popular organisms
	- ID：字母嗯好数字的组合
- UniRef (uniprot reference clusters)
	- 提供蛋白质序列的clustered sets
	- 从UniProtKB和UniProt Archive records中获取覆盖整个蛋白质空间的 数据
	- 有多种方式来隐藏冗余的序列(根据百分比来筛选方式)：
		- UniRef100: 特征序列+亚片段+11个或更多的残基(从任何生物中) – 形成一个单UniRef entry
		- UniRef90: 聚集UniRef100的序列成束
			- 每一束由与最长序列90%一致、80%重叠的序列组成
		- UniRef50: UniRef90的种子序列组成
			- 每一束由与最长序列50%一致、80%重叠的序列组成
- UniParc (uniprot archive)
	- a comprehensive and non-redundant repository
	- 包含所有主要公开数据库中的蛋白序列
- Proteomes
	- 包含物种全部测序的基因组

### 蛋白结构数据库

PDB (Protein Databank): http://www.rcsb.org
- 不仅有蛋白结构，还有核酸和多糖结构
- ID：
	- 第一个符号：1-9数字
	- 第二到第四：数字字母均可
- entry
- 3D view – 序列标注视图

pFAM  http://pfam.xfam.org/

PDBe

RasMol: display

AlphaFold DB (AlphaFold Protein Structure Database)
- 平均已经取得实验测定结构的准确程度

### 功能数据库 (domain, function site)

Gene function
- Genome Location: chromosome location, sequence loci
- Functional Domain: BLAT
	- InterPro Domains
	- Pfam Domains
- Gene Ontology (GO) annotations with structured vocabulary
	- Molecular function
	- Biological process

Pfam:
- 两个内容：
	- Pfam-A entries：被很好维护的families
	- Pfam-B entries：自动生成的entries
		- 使用ADDA数据生成的对Pfam-A的补充
		- 质量较低
		- 用于鉴定当没有Pfam-A时的功能保守序列
- HMM Search
- Pfam Search

SMART
- 两种模式：
	- normal
	- genomic

motif databases: Scan Prosite, PRINTS
- store：保守的模体 – 核酸/蛋白序列
- 保存方式：
	- consensus sequences
	- aligments
	- statistical representations: residue frequency table

Interpro：蛋白质功能数据库的整合
- members: 
	- CDD, Pfam, PRINTS, SMART, 
	- PROSITE profiles, PROSITE patterns
	- CATH-Gene3D, HAMAP, PANTHER, PIRSF, SFLD, SUPERFAMILY, TIGRAMs
- entry type:
	- domain
	- family
	- homologous superfamily
	- repeat
	- sites:
		- conserved site
		- active site
		- binding site
		- PTM
- species
- domain architectures: 与其他domain一起的组合
- search – 可直接用domain搜索
- Browse

Gene Ontology (GO)
- 一项倡议(initiative) – 标准化物种/数据库间，基因和基因产物的属性的表示
	- a contrilled vocabulary of terms
	- gene product annotation data
	- tools to acccess and process this data
- GO enrichment analysis
- evidence: GO注释(annotation)格式中需要有的部分
- 不同系统，如免疫系统的GO标记
- browse – drill-down browsing – interactive tree
- search the ontology

KEGG (Kyoto Encyclopedia(百科全书) of Genes and Genomes)
- KEGG PATHWAY Database
	- metabolism
	- genetic information processing
	- enbironmental information processing
	- cellular processes
	- organismal systems
	- human diseases
	- drug development

National Cancer Institute
- Cancer Genome Anatomy Project – pathway
- Erk1/Erk2 Mapk signaling pathway

PPI database:
- HPRD
	- browse
- BioGrid (biological general repository for interaction datasets)
- BIND
- MINT

## prediction of protein function (PFP)

在GO的分类中，有41.7%的蛋白功能是未知的

function的定义：
- 结构
- 细胞学
- 医学

可利用多种方式来预测蛋白质的功能

### PFP from homology

- detection 检测同源性
	- pairwise序列相似性搜索: BLAST, FASTA, full Smith-Waterman
	- profile-based similarity searches: PSI-BLAST, HMM
	- 序列相似性应当在蛋白质层面被评估
- 相关表征：
  - sequence homology(蛋白有共同的祖先基因)
  - sequence similarity(序列的相似值，是准确值)
  - functional homology(不同物种中的蛋白有相似作用) – 与SH和SS没有相关性
- 类型：
  - 基因复制，造成不同的基因功能变化：
    - neofunctionalization(新功能化)
    - subfunctionalization(亚功能化)
    	- 每一个复制基因起部分原始基因的功能
    	- 功能的同源性无法被定义
    	- 每一个直系同源有相同的分子功能，在不同的亚过程或位置
  - 保留原始功能 – orthologs 直系同源
  	- 类型：
  		- 1-to-1 orthology：不同物种的单基因功能相同
  			- same: molecular function/biological process/localization
  			- 在原核生物和联系较紧密的物种中产生
  		- 1-to-many orthology：一个物种中的单基因与另一个物种中定点多基因相联系 – mixture of neo- and sub-functionalizations
  			- same: molecular function
  			- different: biological process/sun-process/sub-cellular localization/tissue
  			- 在简单模式生物嗯好高级真核生物中常见
  		- many-to-many orthology：多物种的多基因，都是从同一原始基因发展而来的 – 不同的sub和neo功能化发生在不同的物种中
  			- same: molecular function
  			- different: biological process/sun-process/sub-cellular localization/tissue
  			- 在较远联系的高等真核生物间常见
  	- detection 直系同源的检测：
  		- 重建立系统发生树(phylogenetic trees) – 理论上最正确的方式 – 分析特定的基因
  		- reciprocal matches 相互匹配：一对一，正反向找到一个
  			- best reciprocal matches 相互最佳匹配
  				- 简单的相互最佳匹配只适合1-1 orthology
  			- detection of in-paralogsm – orthologs detection
  			- DB: inparanoid, COGs
  		- manual curation – synteny, protein function
  - 改变功能 – paralogs 旁系同源
- construction of gene trees
  - 检测相关蛋白 – 序列相关性
  - 建立a blocked MSA(multiple sequence aligment)
  - 重建most likely phylogenetic tree
  - trivially extract orthologs and paralogs

### PFP from domains

功能信息较少 – 可能序列同源性比对没有结果

domain:
- 真核蛋白含有许多globular domains，可以独立折叠出空间构型
- 在进化中，这些domains变得统一
- 使用HMMs来从序列鉴定这些domains

HLH DNA binding domain

定位信号
- SMART – signal transduction domains
- Pfam – have the most up-to-date domain collection
- interpro – genome annotion – the domains are annotated with GO terms
- NCBI(CDD) – 接入NCBI的BLAST界面

E-value: 越低越好，序列越长越低（不容易碰到）

### PFP from motifs

类型：
- transmembrane helices
- disordered regions 
- Eukaryotic linear motifs(ELMs)
  - types:
  	- modification site – 磷酸化位点
  	- ligand peptides – SH3 binding site
  	- 目标信号 – nuclear localization sequences
  - prediction:
    - 条件：
      - 大多功能模体缺乏信息，难以从序列上预测：
      	- 低一致序列 – 简单的一致序列随处可见
      		- 准确性更高的PSSMs, ANNs, SVMs也不够准确
      	- 典型的ELM只有三个保守残基 – 过小而难以定位
      	- 允许一些变体
      	- ELM包含的完全信息不在位点处
      - fewer and smaller DB: 相比于domains的数据库，含有更少的例子
        - ProSite(被整合): 
        - ELM: 功能之一是motif discovery and search tools(纯找片段)
      - curation(对数据的综合处理)更加困难
      	- domain数据库可以通过蛋白质序列建立
      	- functional motif数据库必须通过实验验证来验证
      - 预测功能模体的行为：
      	- 信号肽
      		- signal found
      			- N-ter – exportation – secretion – mitochondria – chloroplast
      			- internal – NLS
      			- C-ter – GPI-anchor
      			- other membrane anchors
      		- signal dectection tools
      			- SignalP
      			- MitoProt
      			- ChloroP
      			- Predotar
      			- PSort
      			- TargetP
      			- Sigcleave (EMBOSS)
      			- Phobius
      			- Big-PI
      			- DGPI
      	- 跨膜结构域和拓扑结构
      		- detection: signal peptide, hydropathy, helices
      			- tools
      				- TMHMM
      				- TMPred
      				- TopPred2
      				- DAS
      				- HMMTop
      				- Tmap (EMBOSS)
      				- Phobius
      				- ConPred II
      		- organisation: topology
      	- 转录后修饰 post-translational modification(PTM)
      		- 种类:
      			- phosphorylation 磷酸化 – S-T-Y
      				- NetPhos – 真核
      				- GPS
      			- N-glycosylation N-糖基化 – N
      			- O-glycosylation O-糖基化 – S-T-(HO)K
      				- NetOGlyc – 哺乳动物蛋白
      				- DictyOGlyc – GlcNAc – 网菌属
      				- YinOYang – O-beta-GlcNAc – 真核
      			- Acetylation 乙酰化, methylation 甲基化 – D-E-K
      			- sulfation 硫酸盐化 – Y
      				- Sulfinator
      			- farnesylation 法尼基化, myristylation 十四烷化, palmitoylation 棕榈酰化, geranylgeranylation 香叶酰香叶酰化, GPI-anchor – C-Nter-Cter
      				- N端十四酰化 – NMT
      			- ubiquitination family 泛素化 – K-Nter
      			- inteins (protein splicing) 内含肽
      			- pre-translational 转录前– selenoprotein – C
      		- detection:
      			- pattern prediction – PROSITE
      			- experimental – MS/MS detection
      	- domains/motifs
      		- descriptors:
      			- PROSITE
      			- Pfam
      			- SMART
      			- PRODOM
      			- BLOCKS
      			- PRINTS
      			- TIGRfam
      		- federation – InterPro
      		- techniques
      			- patterns, Regexp
      			- PSSM (PSI-BLAST)
      			- Profiles
      			- HMM
      	- coils 盘绕
      		- helix of helix – coiled-coil
      		- Leu-zipper
      		- detection:
      			- COILS – 权重矩阵
      			- Paircoil, Multicoil – pairwise
      			- Marcoil – HMM
      			- Pepcoil (EMBOSS) – 权重矩阵
      	- 二级结构：准确度为70-80%
      		- structure: &alpha;-helices, &beta;-sheets, turns, random coil
      		- tools:
      			- Garnier (EMBOSS)
      			- PHD
      			- DSC
      			- PREDATOR
      			- NNSSP
      			- Jpred
      			- Jnet
      	- 低复杂度片面区域 low complexity regions
      		- repeats
      			- DUST(DNA)/SEG – 从头检测
      			- RepeatMasker(DNA) – 搜索合集
      			- REP – 搜索合集
      			- REPRO, Radar – 从头
      			- PEST, PESTFind – 从头
      			- EMBOSS(DNA)
      				- einverted/equicktandem/etandem
      				- 回文
      			- EMBOSS(protein)
      				- oddcomp
      		- compositional bias
      	- 抗原性肽链 antigenic peptide: 连接MHC的肽链
      		- MHC：编码动物主要组织相容性抗原的基因群的统称
      		- 分类：
      			- class I – 8, 9, 10 mers
      			- class II – 15 mers(3+9+3)
      		- tools:
      			- SYFPEITHI
      			- HLA_Bind (BIMAS)
      			- MAPPP combined expert
      			- Antigenic (EMBOSS)
      			- 预测蛋白酶体切割位点 – NetChop/PaProc
    - algorithms:
    	- sliding window – transmembrane
    	- nearest neighbor
    	- patterns/regular expression
    		- Pattern：人工智能+运算, PSSM权重矩阵
    		- Regexp
    	- weight matrices – PSSM
    	- HMM/profiles
    	- neural networks
    	- rules

### GO/pathway/PPI network

gene ontology(GO) – controlled vocabularies
- molecular function – activity – 在GO中不区分发生的背景/时间/环境
	- catalytic activity
	- binding activity
	- transporter activity
- biological process – 如嘧啶代谢等，是molecular function的有序组装
- cellular component – 细胞中原有的结构 – 解剖学结构/基因生产组(核糖体、蛋白酶体、蛋白二聚体等)
- 工具：
	- AmiGO – browse GO
	- Blast2GO – 搜索方式
		- GO terms
		- InterPro domains
		- RFAM IDs
		- enzyme codes
	- BlastKOALA – blast KEGG
		- Knumber
		- GhostKOALA
		- KEGG pathways

EcoCyc pathways

PPI network：数据库集合 – database
- HPRD
- BIND
- BioGrid
- DIP
- IntAct
- MINT
- IntNetDB

STRING network
- 7种不同颜色的线：
	- 红 – fusion evidence
	- 绿 – 邻近证据
	- 蓝 – 同出现
	- 紫 – 实验
	- 黄 – 文本挖掘数据 textmining evidence
	- 浅蓝 – 数据库证据
	- 黑 – 共表达

### PFP from co-expression：很多次看到，就有相互作用

- COXPRESdb：基因表达数据库
- WGCNA：权重网络的R包
- CoExp：web tool – 共表达网络的开发

# Molecular

## databases

药物数据库：
- DrugBank  https://www.drugbank.ca/

分子数据：
- Genome: 
	- EBI Magnify  https://www.ebi.ac.uk/metagenomics/, 微生物组
- Transcriptome
	- AnimalTFDB 3.0  http://bioinfo.life.hust.edu.cn/AnimalTFDB/, 动物转录因子数据库
- Proteome
- Metabolome
- Lipidome
- Epigenome
- Meta-genome
