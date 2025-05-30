生物信息数据格式：`.sam .bam .vcf`等

## 序列 (fa fq fai)

*fasta* (缩写为*fa*)：存储核酸或氨基酸序列，允许在序列前定义名称和编写注释。
- 结构分两行：
	- 第一行序列标识（ID）
	- 第二行为序列信息。
- fna,ffn,faa都属于fasta格式：
	- *fna (fasta nucleic acid file)*: 所有核酸序列信息
	- *ffn (fasta nucleotide coding regions file)*: 所有基因的核酸序列信息
	- *faa (fasta Amino Acid file)*: 即所有基因对应的蛋白质序列信息

*fastq* (缩写为*fq*)：存储生物序列和对应序列质量，相当于fasta的plus (+quality) 版
- 结构分为四行：
	- 第一行序列标识 (ID)：每部分信息之间用`:`分隔开，如 `@SIM:1:FCX:1:15:6329:1045:GATTACT+GTCTTAAC 1:N:0:ATCCGA`
		- `SIM` instrument ID（即测序仪的硬件ID）  
		- `1` run number（该测序仪上的测序顺位数字）
		- `FCX` followcell ID（测序芯片的ID）
		- `1` lane ID（第几条lane）  
		- `15` Tile number（Tile数字）
		- `6329` X coordinate of cluster（桥式PCR生成的簇的横坐标）  
		- `1045` Y coordinate of cluster（簇的纵坐标）  
		- `GATTACT+GTCTTAAC` read1 UMI ID + read2 UMI ID（拆分数据的UMI序列）  
		- `1` read number，1 表示read1，2表示read2  
		- `N` Y if the read is filtered (did not pass), N otherwise.（N表示合格，Y不合格）  
		- `0` control number（在HiSeq X and NextSeq平台上总是为0）  
		- `ATCCGA` index（拆分数据用的index序列）
	- 第二行为序列信息
	- 第三行为单独一个+（表示与第一行相同的序列标识，为了节省内存省略为+，此行保留以凑成偶数行保证后续数据处理的便捷性）
	- 第四行，对应第二行序列的质量值（用ascii码表示，通过质量值公式可以计算其准确度）

*fai*：提供随机访问fasta/fastq文件的接口
- 格式：以`\t`分割（fasta 5列，fastq 6列）
	- NAME: Name of this reference sequence
	- LENGTH: Total length of this reference sequence, in bases
	- OFFSET: Offset in the FASTA/FASTQ file of this sequence's first base
	- LINEBASES: The number of bases on each line
	- LINEWIDTH: The number of bytes in each line, including the newline
	- QUALOFFSET: Offset of sequence's first quality within the FASTQ file


## 注释 (gff gtf bed)

`.gff .gtf`，高通量测序中对已经map到参考基因组的reads做注释

- *GFF (general feature format)*：用于基因组注释，目前是第三版`.gff3`
	1. seqid ：通常格式染色体ID或是contig ID
	2. source：注释的来源，一般指明产生此gff3文件的软件或来源数据库。如果未知，`.`代表空
	3. type： 一般使用gene，repeat_region，exon，CDS，或SO对应编号等
	4. start：起始位置，从1开始计数（需要注意：bed文件从0开始计数
	5. end：终止位置
	6. score：得分，注释信息可能性说明，可以是序列相似性比对时的E-values值或者基因预测时的P-values值。`.`代表空
	7. strand：`＋`表示正链，`－`表示负链，`.`表示不需要指定正负链，`?` 表示未知
	8. phase ：仅对编码蛋白质的CDS有效，本列指定下一个密码子开始的位置。可以是0、1或2，表示到达下一个密码子需要跳过碱基个数
	9. attributes：包含额外属性的列表，格式为`tag=value`，不同属性之间以`;`相隔

- *GTF (gene transfer format)*：用于对基因的注释
	1. seqname: 通常格式染色体ID或是contig ID
	2. source：注释的来源。，一般指明产生此gff3文件的软件或来源数据库。如果未知，.代表空
	3. start：起始位置，从1开始计数
	4. end：终止位置
	5. feature：表示基因结构。CDS，start_codon，stop_codon是一定要含有的类型
	6. score：得分，注释信息可能性说明，可用`.`代替空
	7. strand：链的正向与负向，分别用`+`和`-`表示
	8. frame：密码子偏移，可以是0、1或2
	9. attributes：必须要有以下两个值：
		- gene_id value: 表示转录本在基因组上的基因座的唯一的ID。gene_id与value值用空格分开，如果值为空，则表示没有对应的基因
		- transcript_id value: 预测的转录本的唯一ID。transcript_id与value值用空格分开，空表示没有转录本

- *BED (Browser Extensible Data)*：通过规定行的内容来展示注释信息
	- 每行至少包括**chrom**，**chromStart**，**chromEnd**三列，另外还可以添加额外的9列，这些列的顺序是固定的
	1. chrom：染色体号，例如，chr1，chrX
	2. chromStart：feature在染色体上起始位置，从0开始算，染色体上第一个碱基位置标记为0
	3. chromEnd：feature在染色体上终止位置
		- 染色体上前100个碱基片段的位置位置标记为：chromStart=0, chromEnd=100
		- 实际上，第100个碱基不属于当前片段中，当前片段的碱基应该是0-99
		- 所以在BED文件中，起始位置从0开始，终止位置从1开始
	4. name：BED行名，在基因组浏览器左边显示
	5. score：在基因组浏览器中显示的灰度设定，值介于0-1000
	6. strand：正负链标记. Either "." (=no strand) or "+" or "-"
	7. thickStart：feature起始位置(for example, the start codon in gene displays)
		- When there is no thick part, thickStart and thickEnd are usually set to the chromStart position
	8. thickEnd：feature编码终止位置 (for example the stop codon in gene displays)
	9. itemRgb：R,G,B (e.g. 255,0,0)值，当_itemRgb_ 设置为 "On"，BED的行会显示颜色
	10. blockCount：blocks (exons)数目
	11. blockSizes：blocks (exons)大小列表，逗号分隔，对应于_blockCount_
	12. blockStarts：blocks (exons)起始位置列表，逗号分隔，对应于_blockCount_
		- 这个起始位置是与_chromStart_的一个相对位置

## 变异 (vcf)

- *VCF (variant call format)*：用于SNV (single nucleotide variations)，INDEL (insertions & deletions), CNV (copy number variation), SV (structural variant)
	1. CHROM：染色体号，注意不需要前缀`chr`: `1A`
	2. POS：变异位点，对于 INDEL，为 INDEL 的第一个碱基位点: `1144739`
	3. ID：dbSNP 的编号，`.`为置空: `1-1144739`
	4. REF：参考基因组的碱基，也就是等位基因: `G`
	5. ALT：检测样本的碱基，同一位置有多个则以`,`分隔: `C`
	6. QUAL：Phred 的质量值，表示改位点存在变异的可能性；分数越高则认为越可靠，但同时需要考虑测序深度，覆盖度等因素；`.`代表置空，不代表质量值为0: `.`
	7. FILTER：过滤标志，如果为`PASS`则认为是一个变异: `.`
	8. INFO：详细信息，用 key=value的格式来表示；key 一般是简写，具体描述在文件开头的`header lines`中显示: `DP=8953;NZ=1006;AD=8890,63;AC=1005,19;GN=987,18,1;HT=18;MAF=0.009940358`
		1. `AA	Ancestral Allele	一个群体或物种的共同祖先中存在的该等位基因	AA=A`
		2. `AC	Allele Count	该变异的等位基因（ALT列）在样本集合中出现的次数。如果有多个 ALT，使用 ,分隔	AC=4973`
		3. `AF	Alternate Allele Frequency	该变异在样本集合中的频率。对于 1000 Genomes 来说，EAS_AF，AMR_AF，AFR_AF，EUR_AF， SAS_AF 分别表示东亚，美洲，非洲，欧洲，南亚人群的等位基因频率	AF=0.993011`
		4. `AN	Allele Number	该变异的等位基因总数。以二倍体生物为例，如果样本为杂合子（基因型 0/1），AN 值为 1，表示改位点只有一个等位基因发生突变。如果样本为纯合子（基因型 1/1），AN 值为 2	AN=5008`
		5. `DP	Read Depth	该变异位点测序深度，也就是改位点 reads 覆盖度	DP=2365`
		6. `MQ	Mapping Quality	该变异比对时，reads 的平均质量	MQ=100`
		7. `QD	Quality by Depth	该变异质量分数（QUAL）与测序深度（DP）的比值。用于评估改位点的质量。	QD=0.12`
		8. `VT	Variant Type	变异类型，一般包括 SNP，MNP，INDEL，SV 等	VT=INDEL`
		9. `MAF	minor allele frequency	次要等位基因频率	这个测量可以用来粗略地了解给定人群中给定SNP的基因型变异，换句话说，它告诉你这个SNP有多普遍`
		10. `EAF	effect allele frequency	效应等位基因频率	它本质上是等位基因，其与疾病的关系正在被研究。因此，效应等位基因总是次要等位基因`
	9. FORMAT：可选，变异位点格式: `GT:AD:GL`
		1. `GT	Genotype	表示基因型；对于二倍体样本，用两个数字中间以 /或 |分隔；0表示 REF 的等位基因，1表示 ALT 的等位基因，2表示有第二个 ALT 的等位基因。 1/1表示纯合子，0/1表示杂合子，有两个基因型`
			- 相位化 (phasing) 是确定某个个体在某个基因位点所携带的等位基因来自哪个亲本的过程
			- GT 字段中的`/`表示基因型未相位化，表示我们不确定哪个等位基因来自父亲或母亲
			- GT 字段中的`|`表示基因型相位化，也就是说可以确定等位基因的来源亲本
		2. `AD	Allele Depth	样本中等位基因的 reads 覆盖度；对于二倍体，1000,1100用逗号分隔，前者是 REF，后者是 ALT`
		3. `DP	Read Depth	该位点 reads 覆盖度`
		4. `GQ	Genotype Quality	基因型的质量值，表示该基因型的可能性，值越高，可能性越大。计算：Phred 值=-10log10(P)，p为基因型错误的概率`
		5. `PL	Provieds the Likelihoods of the given genotypes	三种基因型的质量值，即0/0，0/1，1/1，三种基因型的概率总和为1。值越小表示是该基因型的概率越大。同样是计算 Phred 值，但是 p 为基因型存在的概率`
		6. `PGT	Phased Genotype	只出现在进行过相分离的样本中。表示相分离后的基因型，两个数字间使用 |表示二倍体样本的基因型`
		7. `PID	Phase ID	描述基因型相位的标识符`
		8. `PS	Phase Set	描述同一样本中基因型相位的信息`
	10. SAMPLEs：可选，各个样本的值，来自`BAM`文件`@RG`的`SM`标签；一般每个样本对应一列，因此该文件会超过十列；每个样本会与 FORMAT 列的格式一一对应，不同格式用`:`分隔: `0/0:5,0:0,2,10  0/0:4,0:0,1,8   0/0:4,0:0,1,8   0/0:3,0:0,   1,6   ./.     0/0:4,0:0,1,8   ./.     0/0:3,0:0,1,6   0/0:7,0:0,2,13`

## 比对 (sam bam)

- *SAM (sequence alignment/map format)*：存储测序数据和参考基因组比对结果的文件，每行以table键分割
	- 标头部分 (header section)：SAM/BAM的注释部分
		- 该部分并非必须，可以省略；
		- 每一行都以`@`符开头，后面跟着两个大写字母，每个字段之间以`\t`分割，每个字段遵循`TAG:Value`的格式（`@CO`开头的行除外）；
		- 每行可以使用以下正则表达式表示：`/^@(HD|SQ|RG|PG)(\t[A-Za-z][A-Za-z0-9]:[ -~]+)+$/ or /^@CO\t.*/`，`@`后紧跟的两个大写字母主要有`HD，SQ，RG，PG和CO五类`，前四类常用如下表，其中加了`*`号的表示该标签必须存在，例如`@HD`这个标签存在时，`VN`必须同时存在
		1. `@HD`：SAM文件的版本、sort方式
			1. `VN*`：version的简写，SAM文件的版本
			2. `SO`：sorting order of alignments，比对的sort顺序，包含四类：
				- unknown, unsorted, queryname
				- coordinate：先以第三列RNAME排序，如果RNAME相同，则以第四列POS字段排序，RNAME为`*`时，该read放在其他结果之后，顺序任意
			3. `GO`：grouping of alignments，比对结果的分组信息，聚集相似的比对结果，分组方法有：
				1. none：默认
				2. query：根据QNAME分组
				3. reference：根据RNAME/POS分组
			4. `SS`：sub-sorting order of alignments，当排序方式不在上面SO中的四类时，以SS方式排序，如`@HD SO:unsorted:SS:unsorted:MI:coordinate`
		2. `@SQ`：比对使用的参考基因组信息
			1. `SN*` reference sequence name
			2. `LN*` reference sequence length
			3. `AH` alternate locus
			4. `AN` alternative reference sequence names
			5. `AS` genome assembly identififier
			6. `DS` description. UTF encoding may be used.
			7. `M5` 参考基因组MD5校验值
			8. `SP` species
			9. `MT` molecule topology，线性或环状
			10. `UR` URL of the sequence
		3. `@RG`: read group
			1. `ID*` ID for every sample SAM
			2. `CN` name of sequencing centre
			3. `DS` description
			4. `DT` sequencing date of sample read
			5. `FO` flow order
			6. `KS` the array of nucleotide bases that correspond to the key sequence of each read
			7. `LB` 文库名称
			8. `PG` programs used for processing the read group
			9. `PI` predicted median insert size
			10. `PL` sequencing platform, like ILLUMINA
			11. `PM` platform mode, more detailed technology/platform information
			12. `PU` detailed information for sequencing platform, like flowcell number, lane number for illumina
			13. `SM` name of sample, or pool for pool sample
		4. `@PG`: 使用何种比对软件、生成当前sam文件的命令行
			1. `ID*` only ID for alignment software
			2. `PN` name of software, like `bwa`
			3. `CL` command of alignment, like: `bwa samse hg19.fasta sample.fastq -f sample.sam`
			4. `PP` 前一个程序的标识
			5. `DS` description
			6. `VN` version of software
		5. `@CO`: 其他注释信息
	- 比对部分 (alignment section)：SAM文件的核心部分，每一行代表一个序列的线性比对 (linear alignment of a segment)，每行包含前11个必需字段，和第12个字段后多个可选字段，使用`TAB-separated`分割，当某个字段信息缺省时，如果字段是字符串型以`*`替代，如果字段是整型以`0`来替代，下表为11个必需字段（11列）含义的概述：
		1. `QNAME (query template name)	字符串	[!-?A-~]{1,254}	需要比对的序列名称（FASTQ中第一行）` 如果QNAME唯一，则序列被认为来源于同一模板；`*`表示该字段缺省；一般情况下，该字段为FASTQ文件的第一行信息；嵌合（Chimeric alignment）比对或者多次比对（Multiple mapping）的序列会导致一个QNAME在SAM中多次出现。
		2. `FLAG	整型	[0,2^16-1]	FLAG的位操作符` SAM中显示的是下图中第一列值或者第一列中的数值和，当显示的是下表中第一列数值时，意义为Description所列出，如果是多个数值和，意义为Description多行意义汇总，常用的意义见下表：
			- `1 0x1`：该read使用双端测序，是PE双端测序，单端测序为0
			- `2 0x2`：该read和完全比对到参考序列，没有错配和缺失
			- `4 0x4`：该read没有比对到参考序列，没有mapping到参考序列上
			- `8 0x8`：双端序列的另外一条序列没有比对上参考序列（read1或者read2），mate序列没有mapping到参考序列上
			- `16 0x10`：该read比对到参考序列的负链上（该read反向互补比对到参考序列）
			- `32 0x20`：该read的另一条read比对到参考序列的负链上，mate序列比对到参考序列的负链上
			- `64 0x40`：双端测序 read1
			- `128 0x80`：双端测序read2
			- `256 0x100`：该read不是最佳的比对序列，一条read能比对到参考序列的多个位置，只有一个是最佳的比对位置，其他都是次要的
			- `512 0x200`：该read在过滤（碱基质量，测序平台等指标）时没通过，序列没有通过QC
			- `1024 0x400`：PCR（文库构建时）或者仪器（测序时）导致的重复序列，是PCR重复序列
			- `2048 0x800`：该read可能存在嵌合（发生在PCR过程中），当前比对部分只是read的一部分，是补充比对
			- `73, 133, 89, 121, 165, 181, 101, 117, 153, 185, 69, 137 `：双端reads只有一条reads比对上
			- `77, 141`：双端reads都没比对上
			- `99, 147, 83, 163`：reads比对上了，大小方向均对
			- `67, 131, 115, 179`：比对上了，但是方向不对
			- `81, 161, 97, 145, 65, 129, 113, 177`：唯一比对，但是大小不对
		3. `RNAME (Reference sequence NAME of the alignment)	字符串	\*|[!-()+-<>-~][!-~]*	参考基序列的名称` 比对时参考序列的名称，一般是染色体号（如果物种为人，则为`chr1~chr22，chrX，chrY，chrM`）。RNAME（如果不是`*`）必须在header section部分`@SQ`中`SN`标签后出现；如果没有比对上参考基因组，用`*`来表示。如果RNAME值是`*`，则后面POS和CIGAR也将没有值
		4. `POS	整型	[0,2^31-1]	序列比对到参考序列中的起始位置坐标（以1为起始）` 该read比对到参考基因组的位置坐标，最小为`1`（1-based leftmost）；该read如果没有比对上参考序列，则RNAME和CIGAR也无值
		5. `MAPQ (MAPing Quality)	整型	[0,2^8-1]	比对质量值` 对应参考序列的质量，比对的质量分数，越高说明该read比对到参考基因组上的位置越准确；其值等于`-10 lg Probility （错配概率）`，得出值后四舍五入的整数就是MAPQ值。如果该值是`255`，则说明对应质量无效
				- 例如，MAPQ为`20`，即Q20，错误率为0.01，20 = -10log10(0.01) = -10*(-2)
		6. `CIGAR (Compact Idiosyncratic Gapped Alignment Representation)	字符串	\*|([0-9]+[MIDNSHPX=])+	CIGAR字符串` 
			1. `M	0	match	read	ref`
			2. `I	1	insertion	read	ref`
			3. `D	2	deletion	no	ref`
			4. `N	3	跳过参考基因组，转录组中表示遇到内含子	no	ref`
			5. `S	4	soft clipping，比对时跳过read中部分序列，不改变read长度	read	no`
			6. `H	5	hard clipping，比对时直接剪掉部分序列，read长度被改变，发生在比对开始或者结束时	no	no`
			7. `P	6	padding，read比对时中间跳过参考序列部分区域	no	no`
			8. `=	7	该read完全匹配	read	ref`
			9. `X	8	该read不匹配	read	ref`
			10. 例如：`3M1D2M1I1M`，3个碱基匹配、1个缺失、2个匹配、1个插入、1个匹配
		7. `RNEXT	字符串	\*|=|[!-()+-<>-~][!-~]*	双端测序中另外一个read比对的参考序列名称` 双端测序中另外一条read比对的参考序列的名称，单端测序此处为`0`，RNEXT（如果不是`*`或者`=`，`*`是完全没有比对上，`=`是完全比对）必须在header section部分`@SQ`中`SN`标签后出现。第3和第7列，可以用来判断某条read是否比对成功到了参考序列上，read1和read2是否比对到同一条参考染色体上
		8. `PNEXT	整型	[0,2^31-1]	双端测序中另外一个read比对到参考序列中的起始位置坐标` 双端测序中，是指另外一条read比对到参考基因组的位置坐标，最小为`1`（1-based leftmost）
		9. `TLEN (insert DNA size)	整型	[-2^31+1,2^31-1]	建库时打断的长度` 文库长度/插入片段长度
		10. `SEQ	字符串	\*[A-Za-z=]+	序列碱基信息（FASTQ中第三行）` read碱基序列，FASTQ的第二行
		11. `QUAL	字符串	[!-~]+	SEQ字段对应的ASCII码质量字符（FASTQ中第四行）` FASTQ的第四行
		12. `Optional fields` 可选的自定义区域，可能有多列，多列间使用`\t`隔开，并不是每行都存在这些列，每列格式为TAG:TYPE:VALUE
			1. `TAG` 为两个大写字母，可分为6类：
				1. Additional Template and Mapping data（一些比对信息）
					1. `AM:i:score` The smallest template-independent mapping quality of any segment in the same template as this read. (See also SM.)
					2. `AS:i:score` Alignment score generated by aligner.
					3. `BQ:Z:qualities` Offset to base alignment quality (BAQ), of the same length as the read sequence. At the i-th read base, BAQi = Qi (BQi 64) where Qi is the i-th base quality.
					4. `CC:Z:rname` Reference name of the next hit; ‘=’ for the same chromosome.
					5. `CG:B:I,encodedCigar` Real CIGAR in its binary form if (and only if) it contains >65535 operations. This is a BAM fifile only tag as a workaround of BAM’s incapability to store long CIGARs in the standard way. SAM and CRAM fifiles created with updated tools aware of the workaround are not expected to contain this tag. See also the footnote in Section 4.2 of the SAM spec for details.
					6. `2CP:i:pos` Leftmost coordinate of the next hit.
					7. `E2:Z:bases` The 2nd most likely base calls. Same encoding and same length as SEQ. See also U2 for associated quality values.
					8. `FI:i:int` The index of segment in the template.
					9. `FS:Z:str` Segment suffix.
					10. `H0:i:count` Number of perfect hits.
					11. `H1:i:count` Number of 1-difffference hits (see also NM).
					12. `H2:i:count` Number of 2-difffference hits.
					13. `HI:i:i` Query hit index, indicating the alignment record is the i-th one stored in SAM.
					14. `IH:i:count` Number of alignments stored in the fifile that contain the query in the current record.
					15. `MC:Z:cigar` CIGAR string for mate/next segment.
					16. `MD:Z:[0-9]+(([A-Z]|\^[A-Z]+)[0-9]+)*` String for mismatching positions. The MD fifield aims to achieve SNP/indel calling without looking at the reference. For example, a string `10A5^AC6` means from the leftmost reference base in the alignment, there are 10 matches followed by an A on the reference which is difffferent from the aligned read base; the next 5 reference bases are matches followed by a 2bp deletion from the reference; the deleted sequence is AC; the last 6 bases are matches. The MD fifield ought to match the CIGAR string.
					17. `MQ:i:score` Mapping quality of the mate/next segment.
					18. `NH:i:count` Number of reported alignments that contain the query in the current record.
					19. `NM:i:count` Number of differences (mismatches plus inserted and deleted bases) between the sequence and reference, counting only (case-insensitive) A, C, G and T bases in sequence and reference as potential matches, with everything else being a mismatch（可以结合CIGAR字段计算错配碱基个数）. Note this means that ambiguity codes in both sequence and reference that match each other, such as ‘N’ in both, or compatible codes such as ‘A’ and ‘R’, are still counted as mismatches. The special sequence base ‘=’ will always be considered to be a match, even if the reference is ambiguous at that point. Alignment reference skips, padding, soft and hard clipping (‘N’, ‘P’, ‘S’ and ‘H’ CIGAR operations) do not count as mismatches, but insertions and deletions count as one mismatch per base.Note that historically this has been ill-defifined and both data and tools exist that disagree with this defifinition.
					20. `PQ:i:score` Phred likelihood of the template, conditional on the mapping locations of both/all segments being correct. 
					21. `Q2:Z:qualities` Phred quality of the mate/next segment sequence in the R2 tag. Same encoding as QUAL.
					22. `R2:Z:bases` Sequence of the mate/next segment in the template. See also Q2 for any associated quality values.
					23. `SA:Z:(rname ,pos ,strand ,CIGAR ,mapQ ,NM ;)+` Other canonical alignments in a chimeric alignment, for matted as a semicolon-delimited list. Each element in the list represents a part of the chimeric alignment. Conventionally, at a supplementary line, the fifirst element points to the primary line. Strand is either ‘+’ or ‘-’, indicating forward/reverse strand, corresponding to FLAG bit 0x10. Pos is a 1-based coordinate.
					24. `SM:i:score` Template-independent mapping quality, i.e., the mapping quality if the read were mapped as a single read rather than as part of a read pair or template.
					25. `3TC:i:` The number of segments in the template.
					26. `TS:A:strand` Strand (‘+’ or ‘-’) of the transcript to which the read has been mapped.
					27. `U2:Z:` Phred probability of the 2nd call being wrong conditional on the best being wrong. The same encoding and length as QUAL. See also E2 for associated base calls.
					28. `UQ:i:` Phred likelihood of the segment, conditional on the mapping being correct.
					29. `XA:Z:` Alternative hits; format `chr,pos,CIGAR,NM`
					30. `XS:i:` suboptimal alignment score. If AS and XS are close or equal, then you are getting multiple alignments happening.
				2. Metadata（这部分内容和 SAM中header section部分相关，描述read测序相关信息）
					1. `RG:Z:readgroup` The read group to which the read belongs. If @RG headers are present, then readgroup must match the RG-ID fifield of one of the headers.
					2. `LB:Z:library` The library from which the read has been sequenced. If @RG headers are present, then library must match the RG-LB fifield of one of the headers.
					3. `PG:Z:program` id Program. Value matches the header PG-ID tag if @PG is present.
					4. `PU:Z:platformunit` The platform unit in which the read was sequenced. If @RG headers are present, then platformunit must match the RG-PU fifield of one of the headers.
					5. `CO:Z:text` Free-text comments.
				3. Barcodes（UMI/单细胞测序cell barcode）: DNA barcodes can be used to identify the provenance of the underlying reads. There are currently three varieties of barcodes that may co-exist: Sample Barcode, Cell Barcode, and Unique Molecular Identififier (UMI).
					1. Despite its name, the `Sample Barcode` identififies the Library and allows multiple libraries to be combined and sequenced together. After sequencing, the reads can be separated according to this barcode and placed in difffferent “read groups” each corresponding to a library. Since the library was generated from a sample, knowing the library should inform of the sample. The barcode itself can be included in the PU fifield in the RG header line. Since the PU fifield should be globally unique, it is advisable to include specifific information such as flflowcell barcode and lane. It is not recommended to use the barcode as the ID fifield of the RG header line, as some tools modify this fifield (e.g., when merging fifiles).
					2. The `Cell Barcode` is similar to the sample barcode but there is (normally) no control over the assignment of cells to barcodes (whose sequence could be random or predetermined). The Cell Barcode can help identify when reads come from difffferent cells in a “single-cell” sequencing experiment.（在单细胞测序中，追溯read来源的标签）
					3. The `UMI` is intended to identify the (single- or double-stranded) molecule at the time that the barcode was introduced. This can be used to inform duplicate marking and make consensus calling in ultra deep sequencing. Additionally, the UMI can be used to (informatically) link reads that were generated from the same long molecule, enabling long-range phasing and better informed mapping. In some experimental setups opposite strands of the same double-stranded DNA molecule get related barcodes. These templates can also be considered duplicates even though technically they may have difffferent UMIs. Multiple UMIs can be added by a protocol, possibly at difffferent time-points, which means that specifific knowledge of the protocol may be needed in order to analyze the resulting data correctly.（UMI信标签，RNA-seq中UMI可以对原始的 RNA 分子进行“绝对定量”）
						1. `BC:Z:sequence` Barcode sequence (Identifying the sample/library), with any quality scores (optionally) stored in the QT tag. The BC tag should match the QT tag in length. In the case of multiple unique molecular identififiers (e.g., one on each end of the template) the recommended implementation con catenates all the barcodes and places a hyphen (‘-’) between the barcodes from the same template.
						2. `QT:Z:qualities` Phred quality of the sample barcode sequence in the BC tag. Same encoding as QUAL, i.e., Phred score + 33. In the case of multiple unique molecular identififiers (e.g., one on each end of the template) the recommended implementation concatenates all the quality strings with spaces (‘ ’) between the difffferent strings from the same template.
						3. `4CB:Z:str` Cell identififier, consisting of the optionally-corrected cellular barcode sequence and an optional suffiffiffix. The sequence part is similar to the CR tag, but may have had sequencing errors etc corrected. This may be followed by a suffiffiffix consisting of a hyphen (‘-’) and one or more alphanumeric characters to form an identififier. In the case of the cellular barcode (CR) being based on multiple barcode sequences the recommended implementation concatenates all the (corrected or uncorrected) barcodes with a hyphen (‘-’) between the difffferent barcodes. Sequencing errors etc aside, all reads from a single cell are expected to have the same CB tag.
						4. `CR:Z:sequence+` Cellular barcode. The uncorrected sequence bases of the cellular barcode as reported by the sequencing machine, with the corresponding base quality scores (optionally) stored in CY. Sequencing errors etc aside, all reads with the same CR tag likely derive from the same cell. In the case of the cellular barcode being based on multiple barcode sequences the recommended implementation concatenates all the barcodes with a hyphen (‘-’) between the difffferent barcodes.
						5. `CY:Z:qualities+` Phred quality of the cellular barcode sequence in the CR tag. Same encoding as QUAL, i.e., Phred score + 33. The lengths of the CY and CR tags must match. In the case of the cellular barcode being based on multiple barcode sequences the recommended implementation concatenates all the quality strings with with spaces (‘ ’) between the difffferent strings.
						6. `MI:Z:str` Molecular Identififier. A unique ID within the SAM fifile for the source molecule from which this read is derived. All reads with the same MI tag represent the group of reads derived from the same source molecule.
						7. `OX:Z:sequence+` Raw (uncorrected) unique molecular identififier bases, with any quality scores (optionally) stored in the BZ tag. In the case of multiple unique molecular identififiers (e.g., one on each end of the template) the recommended implementation concatenates all the barcodes with a hyphen (‘-’) between the difffferent barcodes.
						8. `BZ:Z:qualities+` Phred quality of the (uncorrected) unique molecular identififier sequence in the OX tag. Same encoding as QUAL, i.e., Phred score + 33. The OX tags should match the BZ tag in length. In the case of multiple unique molecular identififiers (e.g., one on each end of the template) the recommended implementation concatenates all the quality strings with a space (‘ ’) between the difffferent strings.
						9. `RX:Z:sequence+` Sequence bases from the unique molecular identififier. These could be either corrected or uncorrected. Unlike MI, the value may be non-unique in the fifile. Should be comprised of a sequence of bases. In the case of multiple unique molecular identififiers (e.g., one on each end of the template) the recommended implementation concatenates all the barcodes with a hyphen (‘-’) between the difffferent barcodes.If the bases represent corrected bases, the original sequence can be stored in OX (similar to OQ storing the original qualities of bases.)
						10. `QX:Z:qualities+` Phred quality of the unique molecular identififier sequence in the RX tag. Same encoding as QUAL, i.e., Phred score + 33. The qualities here may have been corrected (Raw bases and qualities can be stored in OX and BZ respectively.) The lengths of the QX and the RX tags must match. In the case of multiple unique molecular identififiers (e.g., one on each end of the template) the recommended implementation concatenates all the quality strings with a space (‘ ’) between the difffferent strings.
				4. Original data
					1. `OA:Z:(RNAME,POS,strand,CIGAR,MAPQ,NM ;)+ `The original alignment information of the record prior to realignment or unalignment by a subsequent tool. Each original alignment entry contains the following six fifield values from the original record, generally in their textual SAM representations, separated by commas (‘,’) and terminated by a semicolon (‘;’): RNAME, which must be explicit (unlike RNEXT, ‘=’ may not be used here); 1-based POS; ‘+’ or ‘-’, indicating forward/reverse strand respectively (as per bit 0x10 of FLAG); CIGAR; MAPQ; NM tag value, which may be omitted (though the preceding comma must be retained). In the presence of an existing OA tag, a subsequent tool may append another original alignment entry after the semicolon, adding to—rather than replacing—the existing OA information. The OA fifield is designed to provide record-level information that can be useful for understanding the provenance of the information in a record. It is not designed to provide a complete history of the template alignment information. In particular, realignments resulting in the the removal of Secondary or Supplementary records will cause the loss of all tags associated with those records, and may also leave the SA tag in an invalid state.
					2. `OC:Z:cigar `Original CIGAR, usually before realignment. Deprecated in favour of the more general OA.
					3. `OP:i:pos` Original 1-based POS, usually before realignment. Deprecated in favour of the more general OA.
					4. `OQ:Z:qualities` Original base quality, usually before recalibration. Same encoding as QUAL.
				5. Annotation and Padding: The SAM format can be used to represent de novo assemblies , generally by using padded reference sequences and the annotation tags described here. See the Guide for Describing Assembly Sequences in the SAM Format Specifification for full details of this representation.
					1. `CT:Z:strand;type(;key(=value)?)*` Complete read annotation tag, used for consensus annotation dummy features. The CT tag is intended primarily for annotation dummy reads, and consists of a strand, type and zero or more key=value pairs, each separated with semicolons. The strand fifield has four values as in GFF3,2 and supplements FLAG bit 0x10 to allow unstranded (‘.’), and stranded but unknown strand (‘?’) annotation. For these and annotation on the forward strand (strand set to ‘+’), do not set FLAG bit 0x10. For annotation on the reverse strand, set the strand to ‘-’ and set FLAG bit 0x10. The type and any keys and their optional values are all percent encoded according to RFC3986 to escape meta-characters ‘=’, ‘%’, ‘;’, ‘|’ or non-printable characters not matched by the isprint() macro (with the C locale). For example a percent sign becomes ‘%25’.
					2. `PT:Z:annotag(\|annotag)*` where each annotag matches start;end;strand;type(;key(=value)?)* Read annotations for parts of the padded read sequence.The PT tag value has the format of a series of annotation tags separated by ‘|’, each annotating a sub-region of the read. Each tag consists of start, end, strand, type and zero or more key=value pairs,each separated with semicolons. Start and end are 1-based positions between one and the sum of the M/I/D/P/S/=/X CIGAR operators, i.e., SEQ length plus any pads. Note any editing of the CIGAR string may require updating the PT tag coordinates, or even invalidate them. As in GFF3, strand is one of ‘+’ for forward strand tags, ‘-’ for reverse strand, ‘.’ for unstranded or ‘?’ for stranded but unknown strand. The type and any keys and their optional values are all percent encoded as in the CT tag.
				6. Technology-specifific data
					1. `FZ:B:S,intensities` Flow signal intensities（测序拍照的光强度数据） on the original strand of the read, stored as (uint16 t) round(value * 100.0).
					2. Color space
						1. `CM:i:distance` Edit distance between the color sequence and the color reference (see also NM).
						2. `CS:Z:sequence` Color read sequence on the original strand of the read. The primer base must be included.
						3. `CQ:Z:qualities` Color read quality on the original strand of the read. Same encoding as QUAL; same length as CS.
				7. Locally-defifined tags: You can freely add new tags. Note that tags starting with ‘X’, ‘Y’, or ‘Z’ and tags containing lowercase letters in either position are reserved for local use and will not be formally defifined in any future version of this specifification. If a new tag may be of general interest, it may be useful to have it added to this specifification. Additions can be proposed by opening a new issue at [https://github.com/samtools/hts-specs/issues](https://link.zhihu.com/?target=https%3A//github.com/samtools/hts-specs/issues) and/or by sending email to samtools-devel@lists.sourceforge.net.
			2. `TYPE` 可以由如下格式`A (character), B (general array), f (real number), H (hexadecimal array), i (integer), or Z (string)`
			3. `VALUE` 内容与TYPE相关，TYPE为`i`时VALUE为整数，以此类推
- *BAM (binary alignment/map format)*：SAM的二进制格式文件，通过BGZF library参考库压缩而成

