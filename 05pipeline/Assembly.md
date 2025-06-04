植物基因组组装与注释流程​：
1. ​组装步骤​
    - ​Survey分析​：K-mer评估基因组大小、杂合度、重复率（工具：Jellyfish, GenomeScope）。
    - ​De novo组装​：
        - 长读长：Canu, Hifiasm（高杂合基因组）；
        - 混合组装：SPAdes（Illumina+ONT）。
    - ​染色体挂载​：Hi-C（Juicebox）、Bionano光学图谱。
    - ​质量评估​：BUSCO（基因完整性）、LAI（重复序列准确性）。
2. ​注释流程​
    - ​重复序列​：RepeatModeler/RepeatMasker + EDTA。
    - ​基因结构​：BRAKER（整合RNA-seq）、GeMoMa（同源预测）。
    - ​功能注释​：InterProScan（蛋白域）、EggNOG（直系同源）。
    - ​非编码RNA​：tRNAscan-SE（tRNA）、Infernal（Rfam数据库）。

> ​**案例**​：
> - 赤松（21.7Gb）：HiFi+Hi-C分单倍型组装，填补裸子植物空白。
> - 马铃薯：图形泛基因组解析56万结构变异（SV）。

技术挑战​
- ​T2T基因组​：端粒到端粒组装（已实现水稻、拟南芥）。
- ​多倍体分型​：单倍型解析（甘蔗同源四倍体）。
- ​超大基因组​：松科（>20Gb）组装策略优化。

发展现状
- ​技术驱动​：长读长测序普及推动染色体级别组装，成本降至$1000/人类基因组。
- ​数据爆发​：近三年完成793物种测序（占总数50%），被子植物为主。

> ​**引用课件关键图**​：
> - 图1：三代测序技术比较（PacBio vs. Nanopore）
> - 图2：赤松单倍型基因组组装流程
> - 图3：植物基因组数据库分类树


