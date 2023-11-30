# 基因组分析

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

# 机器学习和数学基础

- 机器学习（Machine learning）

  

  - 发展历程

    

    AI > Machine learning > Deep learning

    - 生信机器学习

      SVM,
      ​Artificial neural networks
      Hidden Markov Model…

      - 人工智能生物学（Artificial intelligence biology）
        研究范式：大数据+ 大算力+ 强算法

      - 中国
        清华大学孙之荣教授:
        1997年，将人工神经网络引入生物信息学领域
        1999年，利用支持向量机预测可变剪接位点
        2001年，构建蛋白质细胞亚定位预测工具SubLoc，以及蛋白质二级结构预测算法

  - 数据类型
    1.序列数据：DNA、RNA、蛋白质序列
    2.结构数据：NMR、X-ray、Cryo-EM/Cryo-ET
    3.遗传/进化距离数据
    4.谱数据：基因芯片、蛋白质-蛋白质相互作用
    5.影像数据: 图像、视频（CT、MRI、超声）
    6.文本数据：科学文献、电子病历
    7.混合数据：二代测序数据（序列、谱）

  - 研究模式

    - Model-based
      需要建立假设
      构建理论模型
      不需要训练数据
      不需要调整参数
      准确性低
      可解释性高
      例如：基因芯片分析

    - Model-free
      不需要建立假设
      利用机器学习方法
      需要训练数据
      需要调整参数
      准确性高
      可解释性低
      例如：蛋白质二级结构预测

  - 基本内容

    A computer program is said to learn from

    - 学习对象

      experience E
      with respect to some
      class of tasks T
      and
      performance measure P,

      - if its performance at tasks in T, as measured by P, improves with experience E.

    - 模型评估与选择

      - 数据（样本/检验）

        - 阳性数据（P）
          真实的，被实验所证实的数据

        - 阴性数据（N）
          被实验所证明为无功能的数据

      - 评估参数

        - 真阳性(TP)
          阳性数据中被预测为阳性的数据

        - 假阳性(FP)
          阴性数据中被预测为阳性的数据

        - 真阴性(TN)
          阴性数据中被预测为阴性的数据

        - 假阴性(FN)
          阳性数据中被预测为阴性的数据

      - 评估方法

        

        评估算法准确性

        - 参数

          - 灵敏度(Sensitivity, Sn)![img](https://api2.mubu.com/v3/document_image/d7bf4286-a080-464b-8af2-c185dedc4f37-12251550.jpg)
            对于真实的数据，能够预测成“真”的比例是多少-(Type II error)

          - 特异性(Specificity, Sp)![img](https://api2.mubu.com/v3/document_image/3251aa4b-b5a4-4829-a27a-2eca0ac6f4b1-12251550.jpg)
            对于阴性的数据，能够预测成“假”的比例是多少-(Type I error)

          - 准确性(Accuracy, Ac)![img](https://api2.mubu.com/v3/document_image/7b46fbfc-ce9e-4631-82f9-d488d21de373-12251550.jpg)
            对于整个数据集(包括阳性和阴性数据)，预测总共的准确比例是多少

          - 马修相关系数(Mathew correlation coefficient, MCC)![img](https://api2.mubu.com/v3/document_image/2922e483-ee57-43d4-80cf-1f0a25621b64-12251550.jpg)
            当阳性数据的数量与阴性数据的数量差别较大时，能够更为公平的反映预测能力，值域[-1,1]

          - ROC curve + AUC值
            X轴：1-Sp
            Y轴：Sn
            AUC（area under the curve）值：ROC的面积越大，预测能力越强

        - 预测性能的评估（反映预测性能）

          - 自检法（Self-consistency validation）

            反映当前预测工具对目前已知的数据的预测能力
            ​
            ​训练数据当成测试数据
            训练数据中所有的阳性数据为测试数据中的阳性数据
            训练数据中所有的阴性数据为测试数据中的阴性数据

            - 假设：根据目前已知的数据所构建的计算模型能够反映未知的数据的模式

            - 缺点：不能反映计算模型的稳定性

        - 阈值确定

          - Threshold 或 Cut-off
            依据经验，人为设定的一个阈值，阈值以上或以下预测为阳性，即利用阈值进行“一刀切”。

          - 确定阈值的一般方法：
            传统策略：平衡Sn和Sp，使两者大致相当
            实际应用：高Sp低Sn保证预测结果的可靠性
            MCC最大值，保证综合预测性能最高

      - 预测性能的检验（反映预测系统的稳定性）

        预测性能 vs. 检验性能
        差距较小：系统稳定
        差距过大：系统不稳定，数据过训练

        - 过训练
          预测工具过训练：只能很好的符合训练数据，而对新数据则性能很差

        - 方法

          - 除一法（Leave-one-out validation）
            每次从数据集中去掉一个，包括阳性数据和阴性数据
            利用剩下的数据重新训练，并构建新的计算模型
            对去掉的这一个数据进行打分
            保证每个数据去掉一次，从而得到所有数据的分值
            计算各个阈值的Ac, Sn, Sp和MCC
            计算AUC值，作为准确性

          - N折交叉法（n-fold cross-validation）
            将数据集分成n组，并保证阳性数据与阴性数据的比例与原数据相同
            将n-1组作为训练数据，重新训练并构建计算模型；1组不用于训练
            将n-1组的数据重新分为n组，其中n-1组用来构建模型，1组用于调参
            对不用训练的1组进行打分，计算性能
            重复n次，使每组数据都用于独立测试集1次
            选取AUC最高模型

    - 线性模型 & 决策树

      

      

      - 线性回归（linear regression）![img](https://api2.mubu.com/v3/document_image/c6752078-7937-4589-8c5c-0a3b86f6d05c-12251550.jpg)

      - 对数几率回归/逻辑回归（logistic regression）![img](https://api2.mubu.com/v3/document_image/8d969770-682e-4f5c-b74e-ad09d2963dc4-12251550.jpg)

      - 信息熵![img](https://api2.mubu.com/v3/document_image/65babae9-6afd-40fc-8292-1e1c0d7711f6-12251550.jpg)

      - 信息增益![img](https://api2.mubu.com/v3/document_image/75e16ca1-d856-4e94-ad47-38d97376a839-12251550.jpg)

    - 神经网络 & 支持向量机

      

      

      - 单层 & 多层神经网络

      - 误差逆传播（Back propagation, BP）![img](https://api2.mubu.com/v3/document_image/df58a78c-423d-4fd2-b896-951e2187e197-12251550.jpg)

      - 划分超平面![img](https://api2.mubu.com/v3/document_image/738a3df3-7ae9-4981-a221-b893087a8872-12251550.jpg)

      - 核函数

    - 贝叶斯分类器 & 集成学习

      

      - 贝叶斯最优分类器![img](https://api2.mubu.com/v3/document_image/ea365a12-9b73-4ad7-bc64-5d93fa79653c-12251550.jpg)

      - 集成学习的错误率![img](https://api2.mubu.com/v3/document_image/25df0d51-cf11-4b44-ba0c-945efc2aeb67-12251550.jpg)

      - 集成学习的方法

        

        - 并行化
          Bagging、随机森林

        - 串行化
          Boosting

    - 聚类 & 降维与度量学习

      

      

      - 无监督学习

        - 性能度量

        - 距离计算

      - 聚类分析方法

        

        - k-means clustering

        - Hierarchical clustering

      - K近邻学习

      - 低维嵌入

      - 主成分分析
        t-SNE

      - 将高维数据尽可能的投影到二维平面上

    - 概率图模型 & 规则学习 & 强化学习

      

      - 隐马尔科夫模型（Hidden Markov Model, HMM）

      - 发散概率可估算

      - 状态转移态度未知（隐）

      - 强化学习![img](https://api2.mubu.com/v3/document_image/0beb6422-dcd6-4816-af77-682312caf0cc-12251550.jpg)
        任务与奖赏

  - 机器学习常用软件包
    - Scikit-Learn

  - 深度学习（Deep learning）

    - Convolutional neural network, CNN![img](https://api2.mubu.com/v3/document_image/d3bac351-c2a5-4de4-b2f4-9db734e43213-12251550.jpg)

    - Deep neural network, DNN![img](https://api2.mubu.com/v3/document_image/d151405e-2a13-41ba-9c5e-0389c5a557e2-12251550.jpg)

    - Recursive neural network, RNN![img](https://api2.mubu.com/v3/document_image/847aec7b-9884-4ac6-9c86-01256665c67d-12251550.jpg)

    - Generative adversarial network, GAN![img](https://api2.mubu.com/v3/document_image/95035e06-a327-4c2a-8e9a-a9aee3dfd8c4-12251550.jpg)

    - 基本内容

      - 神经元![img](https://api2.mubu.com/v3/document_image/73b4592b-43ff-4ade-b68f-7019d3d9ab1c-12251550.jpg)![img](https://api2.mubu.com/v3/document_image/46ec07ff-c0cb-4334-b0c4-f295b1f09267-12251550.jpg)
        神经元激活函数

      - 卷积层![img](https://api2.mubu.com/v3/document_image/37f2a5fd-0830-4bcc-9a5e-5271dbfab143-12251550.jpg)

      - 最大池化（Max pooling）![img](https://api2.mubu.com/v3/document_image/62e97e56-1b35-4816-ac73-b1677d0fd2c9-12251550.jpg)

      - 输出![img](https://api2.mubu.com/v3/document_image/a92de5ca-95a7-47f0-a08e-1c2ca14e19cc-12251550.jpg)

    - 混合学习/融合AI![img](https://api2.mubu.com/v3/document_image/d2fa99aa-b697-437e-b00e-83598975d72f-12251550.jpg)

    - 软件包
      - Keras

    - 和浅度学习对比![img](https://api2.mubu.com/v3/document_image/e159d36d-f440-45d6-bb11-8fdde2c77f18-12251550.jpg)

- 数学基础

  - 生物序列的概率模型

    - 色子模型

      一个色子存在6个概率值：p1, p2, …,p6，其中掷出i的概率为pi (i=1, 2, …, 6)。

      - 考虑三次连续的掷色子，结果为[1，6，3]，则总概率为：p1p6p3

    - 概率分布

      

      f(x)称为概率密度函数

      - 二项分布：

        

        

        - 酵母全基因组复制（P值大奖）

          

          基因数量的增加
          酵母~6000个基因，人类~21,000个基因
          单个基因复制、基因组复制、染色体片段复制
          通过基因组复制：K. waltii(克鲁雄酵母) > S. cerevisiae(酿酒酵母) 和S. bayanus(贝克酵母)
          克鲁雄酵母ORC1/SIR3：在酿酒酵母和贝克酵母中都有两个拷贝
          ​

          - 复制基因与已有基因的功能关系

            - “新功能形成”：Ohnoone-gene-only speeds-up (OS) model
              一个基因功能不变从而进化慢，另一个需要产生新功能从而进化快

            - “亚功能形成”：Both-genes speed-up (BS) model
              两个基因都只保留原有基因的部分功能，因此进化速率都快

          - 复制基因分别的进化速率估算

            - OS模型：其中一个基因进化速率快

            - BS模型：两个基因进化速率都快

          - 算p-value

            作者鉴定了酵母中457对通过全基因组复制产生的复制基因对（总共914个基因）。在酿酒酵母中，其中76对有加速进化的现象。“加速进化”在文中的定义指的是酿酒酵母里氨基酸替代率要比克鲁雄酵母里高50%。在76对有加速进化的复制基因对里，其中只有4对是两个基因都加速进化。因此基因对里只有一个加速进化的为72个基因（72/76=95%）

            - 统计模型![img](https://api2.mubu.com/v3/document_image/3191b256-7d4d-4f0f-b4cb-29d8615b4177-12251550.jpg)

      - 泊松分布

        

        稀有事件发生的概率：在一个连续的时间或空间中，稀有离散变量出现的概率
        方差等于均值

        - 细菌对噬菌体的应答

          进化：细菌是否有基因？受到噬菌体攻击如何生存？
          拉马克机制：获得性遗传免疫假说–细菌在接触到噬菌体后，小概率产生抵抗，不需要基因或遗传物质
          孟德尔机制：突变假说

          - 细菌生存潜在机制

            - 两类机制

              - 孟德尔——遗传变异

                细菌在噬菌体攻击之前已经具有抵抗能力，不需要与病毒相互作用，受到攻击时也不产生新的突变
                具有抵抗能力的细菌随时间比例增加

                - 非泊松分布：抵抗性细菌由紧密相关的个体构成群落

              - 拉马克——获得性遗传免疫

                细菌在受到攻击的时候才产生免疫能力
                具有抵抗能力的细菌在受到攻击时的比例恒定
                只有当与病毒接触时才产生免疫

                - 泊松分布：每一个抵抗是一个独立的事件

            - 两类实验

              

              有抵抗力的细菌比例是否随时间上升
              观察细菌克隆的个数，看抵抗是否与遗传突变相关

              - 将方差与均值进行比较
                在每一个实验中，可抵抗细菌的波动（fluctuation）远比均值高，不能归因于采样误差，与获得性遗传免疫的假设冲突

        - 鸟枪法的覆盖率（Lander-Waterman Model）

          假设：需要测序的BAC长度200 kbp
           总共测序的序列数量：N
           每次测序：500 bp
           每次测序的覆盖率p：500/200 kbp=0.0025
           因此：总覆盖率C=Np（每个点平均覆盖到的次数）
          Y: 测序能够覆盖到点X的次数

          - 近似符合泊松分布（Poisson distribution）

            

            - 准确性![img](https://api2.mubu.com/v3/document_image/c7da266e-b3c1-495c-95f2-f9b589c09b43-12251550.jpg)

        - 随机产生多个基因的概率![img](https://api2.mubu.com/v3/document_image/4a67de48-bed3-4b7f-885e-d72f016cf04e-12251550.jpg)

      - 超几何分布

        与二项式分布的区别：不放回抽样

        - 与二项分布对比![img](https://api2.mubu.com/v3/document_image/9359f24c-c335-47dc-902d-6aa4d13b4a61-12251550.jpg)![img](https://api2.mubu.com/v3/document_image/c55c8c1c-a624-4ba1-aca4-de29d2d17f49-12251550.jpg)

        - 不等式（p-value）![img](https://api2.mubu.com/v3/document_image/d111de14-9ca1-4464-8d9c-40db9d051626-12251550.jpg)![img](https://api2.mubu.com/v3/document_image/b7fadf1f-8a8d-4491-b496-163cd7900ccd-12251550.jpg)

        - 例

          研究者从26873个人类蛋白质中预测了2264个具有某种特定功能的底物，并进行进一步的分析。其中，有421个人类蛋白质具有某种功能结构域D，而在预测的2264个底物中，有94个蛋白质具有结构域D
          ​问：结构域D在2264个底物中是显著出现，显著不出现，还是随机出现？

          - 问题描述![img](https://api2.mubu.com/v3/document_image/25d72b06-9998-41eb-822c-aee41b33f3f3-12251550.jpg)
            N = 26873; n= 2264; M = 421; m = 94;
            (m/n)/(M/N) = 2.65
            因此，问题转化：在26873个人的蛋白质中，抓出2264个蛋白质，其中至少有94个蛋白质具有功能结构域的概率是多少？

          - 统计显著性

            统计显著：p-value < 0.05

            考虑两个假设H0（空假设）和H1（备择假设）
            H0代表随机情况下事件出现的概率
            H1代表当前出现事件的概率
            如果H0/H1<< 0.05，则接受H1而不接受H0

            超几何分布的p-value：
            “完全随机状态下”事件出现的概率，即p-value=H0
            H1=1

            - 超几何分布的精确概率计算：

              

              2X2表

              - 计算公式（Fisher’s Exact Test）

                

                - 上例
                  a+b+c+d=26873,
                  c+d=2264,
                  b+d=421,
                  d=94

    - 随机序列模型

      假设一个残基a随机出现的概率为qa，并且该概率独立于其它残基而存在

      - 生物序列![img](https://api2.mubu.com/v3/document_image/f12a8f3c-f614-4b8c-a8d0-81821995f46a-12251550.jpg)

    - 最大似然估计

      - 概率模型的参数通常是从大的可靠的数据集，即训练集中估算得到

        例如：通过对Swissprot数据库分析，各个物种中，20种氨基酸出现的频率

        - 最大似然性估计：

          充分使用了训练集的数据，作为概率模型的估算参数
          ​
          一般的，给定一个模型，包括参数θ以及数据集D，则对于参数θ的最大似然性估计，要保证P(D|θ)的最大化

          - 过训练（over-fitting）
            例如：掷色子3次，得到[6，6，6]，根据最大似然性的模型，则p1=p2=p3=p4=p5=0; p6=1

        - 氨基酸频率（几个主要真核物种中）![img](https://api2.mubu.com/v3/document_image/e0aaf692-e5ee-4cfd-9272-783daebb15ec-12251550.jpg)

    - 思路流程

      - 不同种概率

        考虑两个色子D1和D2

        - 条件概率：
          用色子D1掷出i的概率为P(i|D1);用色子D2掷出i的概率为P(i|D2)

        - 连接概率：
          随机挑出一个色子的概率P(Dj), j=1,2; 挑到第j色子且掷出一个i的概率（条件概率）为：P(i,Dj)= P(Dj)P(i|Dj)。一般定义为：P(X,Y) = P(X|Y)P(Y)

        - 边际概率：![img](https://api2.mubu.com/v3/document_image/a6a7f301-0cb9-40d5-aa52-02232465862e-12251550.jpg)
          当条件或者连接概率已知的时候，可以计算边际概率并去掉一个变量

      - 故事
        某天，Prof. Gene来到拉斯维加斯去旅游，一时兴起，就去了一个赌场玩两把。游戏是掷色子。但是，据说这个赌场的荷官不老实，使用了两种色子，其中99%的色子是正常（fair）的，而1%的色子（loaded）则使得出现6的概率为50%

      - 问题
        那么，P(6|Dloaded)和P(6|Dfair)是多少？而P(6,Dloaded)和P(6,Dfair)呢？随机拿到一个色子掷出6的概率是多少？

      - 可能性及结果
        P(6|Dloaded)=0.5
        P(6|Dfair)=1/6
        P(6,Dloaded)=0.5*0.01=0.005
        P(6,Dfair)=(1/6)*0.99
        随机拿到一个色子掷出6的概率：P(6,Dloaded) + P(6,Dfair)

      - 新问题
        Prof. Gene拿起一个色子，连续掷了三次，都是6，因此，他判断这个色子是loaded。他这样的判断可靠吗？如果不可靠，那么，怎样才能判断色子可能是loaded呢？

      - 贝叶斯理论及模型比较

        

        前向概率（prior probability）：P(Dloaded)=0.01 和P(Dfair)=0.99
        后向概率（posterior probability）:P(Dloaded|3个6)

        - 结果![img](https://api2.mubu.com/v3/document_image/ff841f15-333d-4233-b936-bd7b800740e3-12251550.jpg)

      - 扩展
        怎样才能认为是loaded色子？
        P(Dloaded|n个6)
        四个6：P=0.45
        五个6：P=0.71>0.5
        当连续掷出5个6以上时，我们认为可能是loaded！
        …
        ​

    - 例子

      

      

      - 对于给定4 bp的序列

        

        - 对于ACTG序列

          

          - 编程解决

            

            - 结果
              P(X-box|ACTG)=0.91！
              P(X-box|ATTT)=0.08
              P(X-box|AGTG)=0.60
              P(X-box|CCGA)=0.0009!