# 多序列比对

序列保守-> 潜在的功能保守
不同物种中的同源基因，功能保守，序列相似性较高
通过多条序列的比较，发现保守与变异的部分

构建HMM模型，搜索更多的同源序列
构建分子进化

- 全局多序列比对

  

  GENEDOC
  http://genedoc.software.informer.com/

  - 最优算法

    搜索有限空间，类似于BLAST算法
    http://www.ncbi.nlm.nih.gov/CBBresearch/Schaffer/msa.html​

    - 时间复杂度

      - 双序列比对![img](https://api2.mubu.com/v3/document_image/a6d4c404-f738-4909-a0ee-fde43496cf85-12251550.jpg)

      - 多序列比对![img](https://api2.mubu.com/v3/document_image/80247a4e-6c58-49f2-baaa-f2aa899bcb25-12251550.jpg)![img](https://api2.mubu.com/v3/document_image/bd602ee4-8e4c-41a6-98fc-1f0ac6499ef6-12251550.jpg)

    - 动态规划算法

      - 全空间![img](https://api2.mubu.com/v3/document_image/f115984e-5cea-4bca-97e7-caed3b78aaa4-12251550.jpg)
        http://www.ncbi.nlm.nih.gov/CBBresearch/Schaffer/msa.html

      - 优化算法![img](https://api2.mubu.com/v3/document_image/19921c20-3d1c-4eb6-90de-0141c43d64a0-12251550.jpg)
        搜索有限空间，类似于BLAST算法
        http://www.ncbi.nlm.nih.gov/CBBresearch/Schaffer/msa.html​

      - hyperlattice

        

        - 最优问题![img](https://api2.mubu.com/v3/document_image/234a8021-f3b4-4089-803f-9d4bbbdfdaa6-12251550.jpg)
          最优的多序列比对，其两两序列之间的比对不一定最优

  - MSA：![img](https://api2.mubu.com/v3/document_image/f52dacc9-7bcd-42fe-b04b-b7bc117c5271-12251550.jpg)
    多序列比对的打分策略

  - 多序列比对的计算方法

    渐进方法：Progressive methods
    迭代方法：Iterative refinement
    部分有向图算法
    隐马尔科夫模型：HMM profile-profile
    整合算法：Meta-methods
    结构特征

    - 渐进方法（Pairwise alignment）

      ClustalW/X: "Classic Clustal"
      http://www.clustal.org/
      http://www.clustal.org/clustal2/
      T-Coffee
      http://tcoffee.org/
      http://tcoffee.crg.cat/apps/tcoffee/all.html

      - ClustalW/X

        

         ClustalW: 1994年，Julie D. Thompson
        等人改进、开发
         ClustalX: 1997年，图形化软件

        - 计算过程![img](https://api2.mubu.com/v3/document_image/c76451d7-8d2f-4b40-80cf-7b3281035f76-12251550.jpg)
          将所有序列两两比对，计算进化距离（差异）矩阵
          使用邻接法（neighbor-joining）构建指导树（guide tree）
          将进化距离最近的两条序列用全局动态规划算法进行比对
          “渐进”地加上其他序列

        - 打分原则![img](https://api2.mubu.com/v3/document_image/9ef89d1c-e8ac-4ba3-9bb7-46727c3c0094-12251550.jpg)
          每条序列的权值和权值的使用
          Score:BLOSUM62的分数

        - ClustalX使用
          导入序列文件
          执行比对：do alignment
          文件导出：dnd、aln

      - 渐进方法的问题

        - 启发式算法（Heuristic algorithm）

          最终结果可能受初始选定的序列的影响

          距离最近的，有两组序列AB和CD，哪组最先比对？两种方案：
          \1. 分别、同时比对。究竟应以AB为准，加入CD，然后再加上其他序列，还是以CD为准？结果可能出入很大
          \2. 随机挑选一组作为基准
          当序列之间差异较大时，上述问题更加明显

          - 举例![img](https://api2.mubu.com/v3/document_image/0fbe54ab-5ec1-4086-bb2e-ad6dd9fae381-12251550.jpg)

    - 迭代算法

      

      

      部分解决渐进算法存在的问题，主要是ClustalW/X存在的问题
      PRRP/PRRN
      https://www.genome.jp/tools-bin/prrn
      DIALIGN
      http://dialign.gobics.de/
      ​

      - PRRP/PRRN![img](https://api2.mubu.com/v3/document_image/40822361-06c7-45c9-84d9-4ddf7bdf6c07-12251550.jpg)
        \1. 先用“渐进”算法进行多序列比对
        \2. 基于多序列比对的结果构建进化树
        \3. 重新计算序列之间的进化距离，再用“渐进”算法进行多序列比对
        \4. 重复上述步骤，直到结果不再发生改变为止

      - DIALIGN![img](https://api2.mubu.com/v3/document_image/885e5534-34b2-46d1-83d0-689e301e6245-12251550.jpg)
        对所有序列进行两两之间的局部最优比对
        找到所有能够匹配的部分M1；将重叠的、前后一致的（consistency）匹配部分连接起来为M2
        将剩下的未比对的序列重新比对，再发现能够匹配的部分，构成新M1，将一致的部分构成M2
        重复上述步骤，直到结果收敛

    - 部分有向图算法：POA

      

      

      https://simpsonlab.github.io/2015/05/01/understanding-poa/
      https://sourceforge.net/projects/poamsa/

      - 激酶的多序列比对![img](https://api2.mubu.com/v3/document_image/312564e5-b3ce-4b1a-b418-efbe746a8814-12251550.jpg)

      - mRMA的基因组定位![img](https://api2.mubu.com/v3/document_image/6db6fe81-450b-4ce0-b9cd-56f73e3d91ea-12251550.jpg)

    - 隐马尔科夫模型（HMM profile-profile）：ProbCons
      主要改进：
      所有序列通过profile HMM的方法进行双序列比对（两两比对）
      将渐进算法与迭代算法整合
      http://probcons.stanford.edu/

    - 整合算法（Meta-methods）：MUSCLE

      

      算法分为三个部分，每个部分相对独立
      http://www.drive5.com/muscle/​

      - Draft progressive:
        (1) 对两条序列，计算距离采用k-mer的思想
        ​(2) 用UPGMA算法构建引导树
        ​(3) 使用渐进算法进行多序列比对
        ​优点：两条序列之间的距离不采用动态规划算法进行比对，节省时间

      - Improved progressive:
        (1) 基于k-mer得到的树可能会产生次优结果，因此，采用Kimura距离的方法对k-mer产生的树重新计算距离矩阵
        (2) 重新用UPGMA构建进化树
        (3) 使用渐进算法进行多序列比对

      - Refinement:
        (1) 随机从进化树上挑出一条边，删除
        (2) 得到两组树，对每组树，计算profile
        (3) 将两组profile进行比对
        (4) 如果最终得分提高，保留结果，否则丢弃

      - ClustalOmega
        算法原理类似MUSCLE
        http://www.clustal.org/omega/
        https://www.ebi.ac.uk/Tools/msa/clustalo/

    - 结构特征

      

      空位罚分：结合蛋白质的二级结构信息

      - SPEM![img](https://api2.mubu.com/v3/document_image/b2eb6097-647a-4551-a8b2-ebf119282620-12251550.jpg)![img](https://api2.mubu.com/v3/document_image/78313f6a-5378-40b8-a5d5-dbafae7868c0-12251550.jpg)
         序列相似度高：准确性大致相当
         序列相似度低：比其他工具高7~15%

      - PROMALS![img](https://api2.mubu.com/v3/document_image/e90242c6-590b-40a7-9831-a3231f8d8feb-12251550.jpg)
        2007年，序列identity<10%的多序列比对
         数据库搜索更多同源序列
         预测二级结构
         隐马尔科夫模型：考虑氨基酸的打分和二级结构
         渐进算法的概率打分

    - 其他

      MAFFT：渐进& 迭代
      https://www.genome.jp/tools-bin/mafft
      T-Coffee (M-coffee)：整合其他工具的输出结果
      http://tcoffee.crg.cat/apps/tcoffee/all.html
      Multiple Sequence Alignment
      https://www.ebi.ac.uk/Tools/msa/

      - T-Coffee

        

        - 序列比对

          - Clustal程序
            计算两两序列之间的全局最优比对结果

          - LALIGN程序
            计算两两序列之间的局部最优比对的结果
            https://www.ebi.ac.uk/Tools/psa/lalign/

        - 构建指导库（primary library）![img](https://api2.mubu.com/v3/document_image/475aff32-8a48-4f60-923a-6aea88715afa-12251550.jpg)
          即综合考虑上述两两部分结果，设计加权系统，找到序列中最保守的部分

        - 渐进算法

          得到最终的结果

          - 通常的“渐进”算法![img](https://api2.mubu.com/v3/document_image/67c410e3-2ddb-4936-8021-bda9fdd86302-12251550.jpg)

          - 基于指导库的修正![img](https://api2.mubu.com/v3/document_image/b3896235-1924-4ade-813f-8c69096f69eb-12251550.jpg)

  - 结果处理
    GeneDoc, BioEdit等软件
    选择需要拷贝的行 -> 比对结果的美化和后处理

  - 性能检验
    - BAliBASE：
      基于蛋白质三级结构，将同一家族的蛋白质序列进行多序列比较
      用BAliBASE中的比对结果，来检验多序列比对工具的性能
      http://www.lbgi.fr/balibase/​

  - 工具比较

    - 性能
      ClustalW/X: 最经典、最被广泛接受的工具
      MUSCLE: 最流行的多序列比对工具
      Clustal Omega:类似MUSCLE
      T-Coffee：序列相似性高时最准确
      DIALIGN: 序列相似性低时较准确
      POA：性能接近T-Coffee和DIALIGN，速度最快（目前主要用于三代测序数据分析）

    - 运算时间![img](https://api2.mubu.com/v3/document_image/8ad1d41f-9c67-4f09-830b-231a8d911067-12251550.jpg)

- 局部多序列比对

# 序列模式识别

- 序列模式

  - 功能结构域（functional domain）![img](https://api2.mubu.com/v3/document_image/cd15b23d-1fe1-4b44-82d7-a68404da5933-12251550.jpg)
    具有完整的、独立的三级结构
    具有特定的生物学功能
    一般长度，几十到几百个氨基酸
    允许插入/缺失，即允许存在gap

  - 模体（motif）

    不具有独立的三级结构
    具有特定的生物学功能：结合，修饰，细胞亚定位，维持结构，等
    长度一般几个到几十个氨基酸或者碱基

    - SUMO化的序列模体：![img](https://api2.mubu.com/v3/document_image/85b1a708-0df3-4466-b50e-b90c588064d1-12251550.jpg)
      Ψ-K-X-E (Ψ:A, I, L, V, M, F, P; X: 任意氨基酸)

  - 模块（BLOCK）![img](https://api2.mubu.com/v3/document_image/e3c25771-1be0-457d-bdb3-798b35d4f366-12251550.jpg)
    几个到几十个氨基酸
    无gap，从全局多序列比对的结果直接处理得到
    描述蛋白质家族或者一类蛋白质的序列保守性

  - 模式（pattern/profile）
    在算法上用来描述一类功能结构域，模体或者模块的表示方式
    根据序列数据，构建的预测模型
    数据形式：概率表示
    用来预测新的可能符合特定模式的序列
    例如，直接将Ψ-K-X-E视为SUMO化位点的，普适的“模式”，则可以预测所有包含该模式的蛋白质序列

- 位点特异性打分矩阵（Position Specific Scoring Matrix (PSSM)）/ 权重矩阵模型（Weight Matrix Model (WMM)）

  

  对蛋白质家族进行多序列比对分析，发现结果中保守的BLOCK
  根据BLOCK序列推导相应的PSSM
  注意：
  不考虑gap的影响
  BLOCK长度一般在几个~几十个残基/碱基

  - 种类

    - 第一种PSSM（由 BLOCK 转得）![img](https://api2.mubu.com/v3/document_image/6563bc98-d26b-4acd-aceb-163e208af96b-12251550.jpg)

    - 第二种PSSM![img](https://api2.mubu.com/v3/document_image/dbf3679a-8290-463e-bacc-dccb4b6d5678-12251550.jpg)
      每一个位置上显示每种氨基酸或者碱基出现的频率

    - 第三种PSSM![img](https://api2.mubu.com/v3/document_image/04e5f2ed-827f-4dd5-8334-4c564852de6a-12251550.jpg)
      每一个位置显示氨基酸/碱基出现的概率

  - 应用

    可以根据BLOCK推导得到的PSSM进行数据库的搜索，发现包含该模式的新的蛋白质，并预测功能
    思考：
    根据PSSM，如何计算新的序列？
    PSSM中究竟包含着何等信息？

    - PSSM->发现

      Do not miss: 性能检验！！！
      结果需要计算Sn, Sp, Ac& Mcc
      需要计算Self-consistency, Leave-one-out validation & n-fold cross-validation

      - 计算log-odds ratio/Odds ratio

        

        

        

        P(S|+)，根据阳性训练数据计算出来的概率
        P(S| -)，计算方法：
        A. DNA序列，四种碱基出现的频率
        B. 蛋白质序列，20种氨基酸出现的频率

        - 结果

          

          结果需要计算Sn, Sp, Ac & Mcc

          - 计算
            Self-consistency
            Leave-one-out validation
            ​n-fold cross-validation

          - 结果解释
            细胞中的剪接机器（Splicing machinery）可能识别其他的，不包括在训练数据中的模式
            PSSM模型不能很好的反映真实的5’ SS的识别情况
            两种可能：either or both

        - 性能检验

      - 计算流程：滑动窗口![img](https://api2.mubu.com/v3/document_image/d90fec2d-0147-4ae2-82ef-5755a08a00ea-12251550.jpg)
        设定域值；窗口宽度12 bp；依次打分预测

      - Log-odds ratio vs. 贝叶斯

        - 例子

          

          - 贝叶斯方法
            必须估计真实的与错误的数量上的比例；另外，假设在未知数据中，(+)与(-)之间的比例不变

          - Log-odds ratio
            不需要知道(+)与(-)之间的比例；
            ​观测到的数据，其为(+)与(-)的比值

        - 域值的确定
          都需要计算Sn, Sp, Ac& MCC

    - PSSM->信息

      PSSM/motif/domain/BLOCK：每一个位置上究竟包含了什么样的信息？
      对于同一个motif/PSSM：有些位点较其他位点提供更多的信息，why?
      如何定量化“信息”？

      - 信息论

        

        - 香农熵：

          2^b = M（b为bit (binary digit) 信息，M为所有概率事件的总数）
          因此：
          b = log2(M)
          b = -log2(1/M)
          b = -log2(P)（若所有事件概率相同，则P=1/M）
          ​

          - 概率相同
            对于某一个motif的一个位置上，可能存在20种氨基酸，且概率相等，则P=1/20
            ​香农熵：b = -log2(1/20) = 4.32 bits

          - 概率不同![img](https://api2.mubu.com/v3/document_image/aba1ed4e-32c8-43b1-a0a6-022e1a3edcee-12251550.jpg)![img](https://api2.mubu.com/v3/document_image/b70a6d60-9008-4ced-bec3-418602e08d70-12251550.jpg)

          - 香农熵：不确定性！

            

            H为每个位置上的“香农熵”，表示在每一个位置上，各种氨基酸出现的不确定性

            - 信息：盒子模型![img](https://api2.mubu.com/v3/document_image/bfbc44c2-6d54-4e3e-b631-e6cda85b5a25-12251550.jpg)
              假设只能回答两个问题；则
              A. 回答问题之前，不确定性为3 bits
              B. 回答问题之后，不确定性为1 bit
              获得信息R：
              R= Hbefore–Hafter= 3-1 = 2 bits

            - 信息：序列分析![img](https://api2.mubu.com/v3/document_image/85233969-87f5-4ac1-a7a7-f9067b9579bb-12251550.jpg)

- 模体发现：

  - 吉布斯采样（Gibbs Sampler）

    Gibbs Sampler是一种Monte-Carlo类的方法，对于输入序列，找到一个最大的似然函数

    - 定义![img](https://api2.mubu.com/v3/document_image/839d359a-6398-4e96-bb5e-5cc97d9c5514-12251550.jpg)
      对于序列s，且在位置A有一个motif的似然函数

    - 特点
      模体发现的一种随机算法（Monte Carlo）
      寻找次优解的算法
      根据PSSM/WMM对随机抽取的序列进行打分来调整采样，直到结果收敛
      不能够保证每次运算的结果一致：需要多运算几次，并进行比较
      对蛋白质、DNA、RNA序列模体的发现有帮助

    - Gibbs Sampling 算法

      - 从每条序列上随机的抽取一段序列，序列长度固定

        

        - 构建PSSM/权重矩阵

          

          - 随机挑选一条序列

            

            - 用构建好的PSSM对该序列上所有可能的motif进行打分(窗口滑动，每次1个氨基酸或者碱基)

              

              窗口滑动，每次1个氨基酸或者碱基

              - 根据似然性的计算，得到似然值最大的模体，即新的motif

                

                - 更新PSSM矩阵

                  

                  - 反复迭代计算，直到似然性结果与PSSM不再发生变化![img](https://api2.mubu.com/v3/document_image/7aedd52a-47cb-4046-98a5-d148f6e1ea50-12251550.jpg)

    - Strong Motif![img](https://api2.mubu.com/v3/document_image/21579643-7e5f-4026-ad42-d9132e99695f-12251550.jpg)

  - 期望最大化算法（Expectation Maximization Algorithm）

    已开发工具：Multiple EM for Motif Elicitation (MEME)
    http://meme-suite.org/

    - 功能：![img](https://api2.mubu.com/v3/document_image/6d27d260-9008-407b-a095-e739d938192d-12251550.jpg)
      确定motif在每条序列上的起始位置（motif大致的位置与长度是确定的）
      假设10条序列，长度20个碱基
      进行多序列，大致确定motif的位置
      待找motif长度为5个碱基

    - EM算法

      E step: 估计motif起始位置的期望最大化
      M step: motif似然性的期望最大化

      - Motif的概率 vs. 背景概率

        

        计算motif中每个位置的碱基的概率分布
        背景概率：根据剩下的序列计算四种碱基的概率分布

        - 似然性概率值的计算

          

          - E step: 起始位置估计

            

            Z值：motif在不同位置起始的几率值。Z值最大化，即为“最可能的起始位置”

            - M step：P值最大化![img](https://api2.mubu.com/v3/document_image/6e3b1410-9898-4b7c-b311-4223e737749f-12251550.jpg)
              根据选择的最大Z值，重新计算矩阵，并计算P值最大的motif

      - 迭代![img](https://api2.mubu.com/v3/document_image/ec31c47a-1da9-48c1-8062-58d300ec66bb-12251550.jpg)

  - Gibbs & EM: 总结
    基本假设：所有序列都拥有，且仅拥有一个motif
    估算两个关联的函数：Gibbs (WMM & motif的似然性)，EM (motif起始位置，Z值& motif的似然性)
    利用两个函数的其中之一修正另一个，采取迭代/反复计算的方法，使结果收敛
    不保证得到的结果为最优，近似算法

  - 模体/PSSM的优化
    仅保留10-50个MAP最高的模体
    利用生成的模体/PSSM对剩余的序列进行打分
    将所有结果按照得分排序
    依次将结果加入模体/PSSM
    重新计算MAP，若分值提高则保留，反之放弃

  - 问题
    给定一组序列，可能的motif仅在部分序列中出现，怎么解决？
    给定一组序列，其中存在某种motif可能在序列上出现两次以上，如何解决？

  - TFBS finding

    TFBS: 转录因子识别特定的motif（transcription factor binding site）

    - CHIP-chip/CHIP-seq:![img](https://api2.mubu.com/v3/document_image/b3b82b72-f5a3-451b-aa17-3298ec6b9641-12251550.jpg)
      高通量鉴定与特定转录因子结合的DNA片段
      存在假阳性
      通过多个motif结合

    - Protein-DNA binding sites finding

      

      基本模型
       给定n条序列
       假设存在若干模体，w1, w2,…，其中w1, w2之间的间隔为gL -> gM
       w1, w2不一定在每条序列上存在
       w1, w2可以在正链或反链上存在

      - 发现方式

        MDscan: a two-step algorithm
        Word enumeration (Seed):
        候选基因排序：结合强度或read数
        Top sequence (3~20)
        统计长度为w的word个数(w-mer)
        考虑正链和反链
        “m-matches”:
        保证随机产生两个w-mer存在m个匹配概率<0.15%
        可随机生成例如1M对w-mers来计算

        - m-matches![img](https://api2.mubu.com/v3/document_image/0d2597b8-259f-47df-a81e-5b4a410d315b-12251550.jpg)
          随机生成1,000,000对w-mers，不超过1500对存在m-matches

    - 问题
      过表达某转录因子，其中500个基因上调，200个下调，如何分析？
      CHIP-array实验中，发现与转录因子X结合的基因有500个，如何分析？

  - 模体的信息量

    PSSM: Seed + “m-matches”

    - 估算信息量(Maximum a posteriori, MAP)：![img](https://api2.mubu.com/v3/document_image/175fa94e-0468-4448-beed-3aae6247b9b2-12251550.jpg)![img](https://api2.mubu.com/v3/document_image/7a6a85de-97c2-4929-a654-97aa4c3aee45-12251550.jpg)
      Xm: 模体/PSSM里存在m-matches的个数；
      pij:模体/PSSM里第i位的第j个核酸的出现频率
      p0(s): 从随机数据里产生一个模体s的概率
      log(expected bases/site): top sequences里“期望”获得的m-matches个数(未知)

    - Markov background model:![img](https://api2.mubu.com/v3/document_image/6ec0817b-ce8d-4aa2-84b4-b5ab66ebc843-12251550.jpg)
      A. 随机数据
      B. 针对每一个w-mer，计算其背景概率

  - MotifX算法![img](https://api2.mubu.com/v3/document_image/a8520592-24ba-46d6-90eb-776416c5318c-12251550.jpg)

- 马尔科夫

  20世纪初，俄国数学家Andrey Markov提出马尔科夫链

  - 马尔科夫模型

    

    随机过程的一种，主要特点为“无后效性”，即根据当前的状态即可完全确定将来的状态
    具有马尔科夫性的过程称为马尔科夫过程

    - 参数估计![img](https://api2.mubu.com/v3/document_image/142ffe84-9819-4238-8ea7-ec944ace9697-12251550.jpg)

    - K-order 马尔科夫模型

      - 一阶马尔科夫模型![img](https://api2.mubu.com/v3/document_image/b38cb333-6aac-4cde-bf45-dcd25c3e7537-12251550.jpg)
        当前位置仅依赖前一位

      - k阶马尔科夫模型![img](https://api2.mubu.com/v3/document_image/b6123dcd-2ff6-49f6-989f-8d533f39cbc4-12251550.jpg)
        当前位置依赖前一位，而前一位依赖前两位,…,前k-1位依赖前k位

      - 0阶马尔科夫模型
        位点独立

    - Markov & PSSM

      对真实的数据进行训练，PSSM =~ 0阶马尔科夫模型
      对新序列的扫描：从头至尾，每次移动1~n位（窗口滑动的方法）
      分别计算窗口内的序列，是(+)和(-)的概率，计算log-odds ratio
      设定域值，若高于域值，则保留结果

      - 然而![img](https://api2.mubu.com/v3/document_image/b10e0273-9293-4eda-a044-72a7295822fd-12251550.jpg)
        对给定的一段序列进行扫描并预测，结果可能如下：

      - 另外

        长度不确定！
        起始位置不知！
        Markov models & PSSM: Not work!!!

        - CpG岛的预测![img](https://api2.mubu.com/v3/document_image/45a3d361-e046-4fce-9ad3-6e8e3ac37fee-12251550.jpg)
          CpG岛：在人的基因组中，如果双碱基对CG出现，则C通常被甲基化。并且，甲基化的C很快会突变成T。因此基因组中CpG岛非常少。然而，在基因的起始位置，例如promotor区域，因为功能的保守性，其序列很少突变，CpG的含量能够保持在40~60%
          PSSM & Markov are not work at all!

        - 蛋白质跨膜结构域![img](https://api2.mubu.com/v3/document_image/2f281c24-b9c8-4216-89d3-13b9f1079d74-12251550.jpg)
          细胞内，有些蛋白质部分在细胞膜外，部分在细胞膜内，负责细胞外信号向细胞内的转导等其他功能
          跨膜结构域：长度不定，具有强的疏水性

        - 基因预测![img](https://api2.mubu.com/v3/document_image/e3ce4fa9-7244-41da-a3ab-8fc4f1e9d4f2-12251550.jpg)
          基因预测：给定一段序列，能否预测是否包含基因
          基因结构预测：真核生物的基因，包括启动子，外显子，内含子，剪切子，ESE，沉默子…….

  - 马尔科夫链
    时间(先后顺序)和状态都离散的马尔科夫过程

  - 隐马尔科夫模型（Profile HMM）

    

    存在状态的跳转：转移概率 -> 未知！
    隐马尔科夫模型：状态之间的转移概率未知

    - 概念
      1.多序列比对的结果中，氨基酸之间存在三种状态：
      匹配（M）, 插入I）和缺失（D）
      2.HMM：三种状态之间的转换关系未知-> hidden -> 转移概率
      3.每个位置上的氨基酸/碱基以及插入、缺失的频率/概率可以通过观测求得-> not hidden
      4.模型训练：通过训练，估算转移概率

    - CpG岛的HMM

      

      存在两种状态：是CpG岛(CpG Island, I)，不是CpG岛(Genome, G)

      - HHM![img](https://api2.mubu.com/v3/document_image/7295ab05-11e6-475f-bd11-793c8f5e72db-12251550.jpg)
        Hidden: 对当前未知的碱基，跳转到下一个位置，究竟是I还是G的概率，未知
        Observable: I和G中的四种碱基分布的概率能够通过实际数据的观测进行计算

      - Viterbi算法

        求出在当前结果最大的概率值，以及保存相应的路线

        - 预测CpG Island

          

          给定序列：ATCGCA,预测CpG的位置?
          状态转移矩阵已知

          - 步骤![img](https://api2.mubu.com/v3/document_image/d640e096-5253-4fda-968b-365e8740fd5a-12251550.jpg)![img](https://api2.mubu.com/v3/document_image/cbb89002-2466-4e51-9f91-769c3cfdd143-12251550.jpg)![img](https://api2.mubu.com/v3/document_image/bd2a661b-c735-4e56-9dc0-f172f4ceca16-12251550.jpg)![img](https://api2.mubu.com/v3/document_image/6dc8d089-e294-43a1-a934-2ab955f3fd0f-12251550.jpg)![img](https://api2.mubu.com/v3/document_image/d4f2de32-b2d4-46af-b6fd-b1e4540f92d7-12251550.jpg)![img](https://api2.mubu.com/v3/document_image/4c6fd49b-d0a4-4edf-b7c8-f95953bd1307-12251550.jpg)![img](https://api2.mubu.com/v3/document_image/19f8a1b6-9e26-4109-ade4-c57afafe6680-12251550.jpg)

          - 预测结果
            ATCGCA: 其中，CGC被预测为CpG Island

      - 递归算法
        动态规划的算法

      - 如何推算状态的概率矩阵

        - HMM:参数估计

          

          - 通过实际数据来估算参数：![img](https://api2.mubu.com/v3/document_image/128ae4a9-1be0-4461-bc82-3c2827961462-12251550.jpg)
            贝叶斯理论

          - Baum-Welch算法

            目的：给定观察值序列O，通过计算确定一个模型H，使得P(O|H)最大

            - 算法步骤：
              初始模型（待训练模型）H0
              基于H0以及观察值序列O，训练新模型H
              如果logP(O|H) -log(P(O|H0) < Delta，说明训练结果已经收敛，算法结束
              否则，令H0 ＝H ，继续第2步工作

            - 操作流程
              1.以CpG Island为例
              2.需要估计的转移概率矩阵有四个值：Pii, Pig, Pgg, Pgi
              3.初始化转移概率矩阵H0，例如，都设为0.5
              4.用Viterbi算法算出所有给定数据的结果及路径
              5.根据所有的路径，可以得到Nii, Nig, Ngg, Ngi
              6.计算新的Pii, Pig, Pgg, Pgi
              7.如果结果收敛，停止；否则，重复4-6

  - 总结

    马尔科夫& 隐马尔科夫

    - 马尔科夫：

      所有状态已知或者可以通过实际数据的观测得到

      - 给定转移概率矩阵
        使用Viterbi算法，求出使给定序列概率值最大的路径

    - 隐马尔科夫：

      发散概率可以通过数据观测得到，状态之间的转移概率矩阵未知

      - 参数估计
        Baum-Welch算法，递归算法，直到结果收敛

- 蛋白质翻译后修饰（POST）

  生化反应：产生或破坏共价键
  发生在氨基酸的主链或侧链上
  通常由特定酶催化
  可发生在15种非疏水的氨基酸上
  目前已发现>680PTMs
  https://www.uniprot.org/docs/ptmlist.txt

  - 磷酸化位点预测

    磷酸化：蛋白激酶通过ATP的水解所释放的能量，将磷酸基团转移到底物蛋白的丝氨酸/苏氨酸，或者酪氨酸的残基上
    可逆的蛋白磷酸化调控了细胞生命中绝大部分的分子、细胞和生理过程
    在哺乳动物的基因组中，编码了约~500个蛋白激酶
    在细胞内，约1/3的蛋白被磷酸化
    磷酸化位点的鉴定，是理解整个细胞内的信号通路、网络以及进一步的系统生物学研究的基础

    - GPS算法

      基本假设：相似肽段，相似功能

      - 打分策略![img](https://api2.mubu.com/v3/document_image/6b5ce5c2-7b29-46a6-be56-f561194ebe73-12251550.jpg)![img](https://api2.mubu.com/v3/document_image/e1e8d4c5-ce48-42ff-ac8d-495547423627-12251550.jpg)

    - 蛋白质序列编码

      另一种算法

      - 赝氨基酸组成（Pseudo amino acid composition）![img](https://api2.mubu.com/v3/document_image/69cd2400-8587-4b2a-8a12-ac33cfe72365-12251550.jpg)

      - k间隔氨基酸对组成（Composition of k-spaced amino acid pairs）![img](https://api2.mubu.com/v3/document_image/5af37191-8318-4421-bded-61a92cdb93ac-12251550.jpg)

      - 正交二进制编码（Orthogonal binary coding/one-hot coding）![img](https://api2.mubu.com/v3/document_image/e8b537ca-3765-4f19-aa8f-39bb10d41ecc-12251550.jpg)