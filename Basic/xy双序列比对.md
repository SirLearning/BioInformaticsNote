# 双序列比对

用于：基于同源序列鉴定的功能预测

注意：
蛋白质一般在三级结构的层面上执行功能
蛋白质序列的保守性决定于其编码DNA的保守性

- 进化假设（序列同源性模型）![img](https://api2.mubu.com/v3/document_image/083b9b3d-9006-41b0-9c0f-3b88e6010c5a-12251550.jpg)
  所有的生物都起源于同一个祖先
  序列不是随机产生，而是在进化上，不断发生着演变

- 同源序列

  - Ortholog（直系同源序列）：

    

    两个基因通过物种形成的事件而产生，或源于不同物种的最近的共同祖先的两个基因，或者两个物种中的同一基因，一般具有相同的功能

    - 物种形成

  - Paralog（旁系同源序列）：

    

    两个基因在同一物种中，通过至少一次基因复制的事件而产生

    - 基因复制

  - Xenolog（异同源序列）：
    由某一个水平基因转移事件而得到的同源序列

  - 一个复杂的问题![img](https://api2.mubu.com/v3/document_image/d6af729c-c9e7-4c01-9c00-d1c5fd8c6bae-12251550.jpg)

- 算法

  - 点阵法（Dot Matrix）

    寻找两条序列间所有可能的比对
    发现蛋白质或者DNA序列上正向或者反向的重复
    发现RNA上可能存在的互补区域

    - 工具：
      https://dotlet.vital-it.ch/
      https://myhits.isb-sib.ch/cgi-bin/dotlet
      http://www.bioinformatics.nl/cgi-bin/emboss/dotmatcher

    - Dotlet JS

    - 自身对比

      - 重复序列![img](https://api2.mubu.com/v3/document_image/5d7d80cc-5cc5-494f-9030-96a638f92f9d-12251550.jpg)

      - 反向重复/回文![img](https://api2.mubu.com/v3/document_image/1036bbc9-5ef3-4a86-b5c1-e8a8ca216ac0-12251550.jpg)

    - 不同序列比对![img](https://api2.mubu.com/v3/document_image/782868c1-11dc-43a0-9cc5-456b36cde727-12251550.jpg)

  - 动态规划算法

    比较所有可能的字符对，考虑匹配、错配以及空位罚分，并且将比对次数控制在多项式时间内

    - 前提（说明好坏）![img](https://api2.mubu.com/v3/document_image/dd2026f4-3152-4e00-b4d4-b478cef8bc2d-12251550.jpg)
      两条序列的相似性 → 相似/相同的生物学功能

    - 模型

      - 全局优化比对（Global）: Needleman-Wunsch

        BLAST (Global Alignment), https://blast.ncbi.nlm.nih.gov/Blast.cgi

        - 运用实例

          

          可采取线性罚分：gap=11

          - 递归算法

            

            要求解Sij的分数，我们必须先知道Si-1, j-1, Si-1, j, 以及Si, j-1的分数，这种方法叫做递归算法；
            采用这种方法，可以把大的问题分割成小的问题逐一解决，即动态规划算法；
            需要存储如何得到Sij分数的过程。

            - Needleman-Wunsch算法（过程标箭头）

              

              时间复杂度O(n^2)

              - 递归结果

                

                - 回溯

                  

                  - 比对结果![img](https://api2.mubu.com/v3/document_image/e6ec9418-996c-42a8-9999-c55dfae4a140-12251550.jpg)

      - 局部优化比对（Local）: Smith-Waterman

        EMBOSS Water, https://www.ebi.ac.uk/Tools/psa/emboss_water/

        - 运用实例

          

          可采取线性罚分：gap=12

          - Smith-Waterman算法

            

            时间复杂度O(n^2)

            - 递归结果

              

              - 回溯

                

                - 比对结果/打分![img](https://api2.mubu.com/v3/document_image/270e5004-8944-46b2-8f99-fb17ab398bb6-12251550.jpg)![img](https://api2.mubu.com/v3/document_image/eb73afb2-8c32-44c3-8834-4aed26752222-12251550.jpg)
                  Smith-waterman算法打分：9分
                  直接打分：-4+2+4-12+9-1=-2

    - 无空位罚分的双序列比对

      

      - 计算效率/计算复杂性

        用CPU的计算时间和内存占用量来衡量
        O( )=…, 时间复杂度
        对于需要解决的问题，其单位数量n运算的时间是一定的f(n)
        如果需要解决的问题的大小与单位数量n的平方成正比，则O(n)=n^2
        对于算法来说：O(logn) > O(n) > O(n^2)

        - NP难题

          无法找到能够在多项式时间复杂度内解决的问题
          一般的，O(nk), 当k≤3 时，为多项式时间，较为容易处理
          当O(nk)= 指数级时间，则难以处理

          - 近似算法/优化算法，求近似解

    - 有空位罚分的双序列比对

      

      

      

      递归

      - 时间复杂度：

        

        为O(2^2n)，指数增加，无法求最优解
        ​NP-hard问题

        - 斯特林公式![img](https://api2.mubu.com/v3/document_image/f0aeb4ee-a148-4f0f-a699-bf9ed1e3a21f-12251550.jpg)

      - 总分![img](https://api2.mubu.com/v3/document_image/d4aa63bf-a60f-47fe-8668-734c64a3d9bc-12251550.jpg)
        Score=Σ(AA pair scores) –gap penalty = 15

    - 打分模型

      - 替代矩阵

        字符相同：identity
        字符替代：similarity，相似性，氨基酸/碱基之间的替代和突变

        - 似然性值

          - 对于不相关或者随机的模型R，两条序列匹配的概率：![img](https://api2.mubu.com/v3/document_image/ba276dde-9ba7-4d60-a8e7-4e4d5d9052d1-12251550.jpg)
            建立模型：
            ​考虑长度为n的序列x和长度为m的序列y
            令xi为x序列中的第i位；yj为y序列中的第j位
            假设xi出现的频率为qxi, yj出现的频率为qyj

          - 对于另择假设/匹配模型M，两个字符匹配的概率为连接概率pab：![img](https://api2.mubu.com/v3/document_image/5f7d5a1f-975f-4e7c-bee2-c087425cbfca-12251550.jpg)

        - 几率值（odds ratio）

          

          两个似然性值之间的比值

          - 对数几率值（log odds ratio）![img](https://api2.mubu.com/v3/document_image/99ea6286-0d14-4d5a-948b-d56633947eb0-12251550.jpg)![img](https://api2.mubu.com/v3/document_image/bd023dfe-853f-47e4-bfb8-7d15e28dcc89-12251550.jpg)
            连乘->连加

        - BLOSUM62![img](https://api2.mubu.com/v3/document_image/257a5234-8d0e-40d1-83f1-c219d6a4ee5e-12251550.jpg)
          空位罚分：11
          延伸的空位罚分：1 (BLAST工具)
          观测数据库得到

      - 插入和缺失

      - 空位罚分

        - 线性罚分：![img](https://api2.mubu.com/v3/document_image/9919395f-afd7-43df-9bfb-86bec4a8d9a5-12251550.jpg)
          d, 每次罚分的分数；g，空位数

        - 修正的罚分：![img](https://api2.mubu.com/v3/document_image/da06a978-5a54-4127-9eee-d8f7524db3af-12251550.jpg)
          d, 第一次罚分的分数；g，空位数；e, 修正后的参数

      - 打分矩阵

        - Dayhoff: PAM系列矩阵

          Accepted point mutation (PAM): 可接受的点突变，氨基酸的改变不显著影响蛋白质的功能

          - 进化模型：
            基本假设：中性进化，Kimura, 1968
            进化的对成性: A->B = B->A
            扩展性：通过对较短时间内氨基酸替代关系的计算来计算较长时间的氨基酸替代关系

          - PAM1矩阵的构建

            

            两个蛋白质序列的~1%氨基酸发生变化
            定义进化时间以氨基酸的变异比例为准，而不是时间：各个蛋白质家族进化的速度并不相等

            - 流程

              - 序列数据集

                

                34个蛋白质超家族
                71个蛋白质分组
                15,720个突变
                序列相似性> 85%

                - 统计不同氨基酸之间的替代

                  

                  15,720

                  - 计算氨基酸出现概率

                    

                    蛋白质序列数据库中20种氨基酸的出现频率

                    - 计算 相对突变能力（relative mutability, ma）

                      

                      

                      例如，对于A，突变数3644，则
                      mA= 3644/(1000.08715720) = 0.0266
                      对于R，突变数为1191，则
                      mR=1191/(1000.04115720) = 0.0173
                      对于F，突变数为682，则
                      mF=682/(1000.0415720) = 0.0108
                      对于Y，突变数512，则
                      mY=512/(1000.0315720) = 0.0108
                      令mA=100，则mR=~65，mF=~41，mY=~41

                      - ~1%氨基酸突变

                        Maa反映a没有突变成其他氨基酸的能力
                        Maa= 1 –ΣMab
                        问题：
                        ΣMab可能会>>1%，使用λ，使得λΣMab约为1%，Maa约为99%
                        PAM1矩阵：
                        Maa= 1 –λΣMab =~ 99%

                        - 计算a->b的相对概率

                          Pa= 氨基酸a出现的概率
                          fab = a->b替代的总数
                          fa（所有与a相关的氨基酸替代数）= Σfab(a不等于b)
                          f = Σfa
                          定义：相对概率M’ab，
                          M’ab= Pr(a->b)=fab/fa

                          - λ的计算

                            

                            20种氨基酸，突变总数1%
                            200,000个氨基酸，突变总数2,000
                            λ= 2000/1468=~1.36

                            - 连接概率

                              

                              - 结果![img](https://api2.mubu.com/v3/document_image/2e96933b-503c-49ef-a7dc-292155d2cc5b-12251550.jpg)![img](https://api2.mubu.com/v3/document_image/a83894b8-b123-4b01-8a3b-8fa23942a467-12251550.jpg)

            - DNA打分矩阵PAM1的构建

              

              假设DNA四种碱基概率为：
              PA=PT=0.3, PC=PG=0.2
              若干序列比较发现1000个碱基替代
              f=1000
              fA= 550, fT=550, fC=350, fG=550
              相对突变能力：
              mA= 0.0183, mT=0.0183, mC=0.0175, mG=0.0275

              - 相对突变能力

                

                - PAM1

                  

                  总数40000个碱基，400个突变
                  λ(mA+mT+mC+mG)=400
                  λmA=λmT=90, λmC=85, λmG=135
                  因此
                  λmAC=16, λmAG=33, λmAT=41
                  λmCA=24, λmCG=37, λmCT=24
                  λmGA=49, λmGC=37, λmGT=49
                  λmTA=41, λmTC=16, λmTG=33
                  ​

                  - PAM2矩阵

                    

                    基本假设：每个氨基酸的突变的概率独立于前次突变。因此，PAM2=PAM1*PAM1

                    - PAM250矩阵![img](https://api2.mubu.com/v3/document_image/a170ea70-c4d5-4f28-a6c6-bb3dc4d61625-12251550.jpg)![img](https://api2.mubu.com/v3/document_image/91810426-24ff-41c4-9160-e426358875d7-12251550.jpg)
                      有250%的期望的突变
                      ​
                      蛋白质序列仍然有15-30%左右的相似性，例如：

                    - 当前使用的PAM250矩阵![img](https://api2.mubu.com/v3/document_image/50e63ae1-dc46-4962-96b1-77b8f8fae31a-12251550.jpg)

                    - 打分矩阵的使用![img](https://api2.mubu.com/v3/document_image/2ef732d5-687e-4793-9d01-b657e0d6ff87-12251550.jpg)
                      PAM250: ~15-30%的序列相似性
                      PAM120: ~40%的序列相似性
                      PAM80: ~50%
                      PAM60: ~60%
                      如何选择最合适的矩阵？
                      遍历尝试…

          - PAM系列矩阵的构建思想
            - 替代矩阵思想![img](https://api2.mubu.com/v3/document_image/cee16003-7d88-4bf7-b439-ea91ecce7136-12251550.jpg)

          - PAM250的计算

            

            相关比率值 Rab：通过进化形成的关联的两条蛋白质序列上的两个氨基酸有关联的几率 vs. 随机的两条蛋白质序列上，两个氨基酸有关联的几率
            Mab= 相关的蛋白质序列上a替换成b的概率

            - 因此

              

              - 结果![img](https://api2.mubu.com/v3/document_image/9dae43d6-e0ad-43a5-ae4c-0728a05550f3-12251550.jpg)

          - PAM系列矩阵的问题

            氨基酸的打分矩阵，不关心核酸
            进化模型的构建需要系统发育树的分析，因此，成为一个循环论证的问题：序列比对->矩阵构建->打分，进行新的序列比对
            数据集很小

            - 改进
              选用大量的序列数据，构建矩阵（JTT矩阵）
              BLOSUM系列矩阵
              核酸的打分矩阵

        - Henikoff: BLOSUM系列矩阵

          最被广泛使用的氨基酸打分矩阵系列

          - 术语名词

            - BLOCK: 
              蛋白质家族保守的一段氨基酸，无gap，一般几个~上百个氨基酸

            - Prosite家族：
              至少有一个BLOCK存在于该家族的所有蛋白质序列中

            - BLOSUM62: 
              序列的平均相似性为62%的BLOCK构建的打分矩阵

          - 利用”Block” (模块) 计算矩阵

            

            ~500组相似的蛋白质
            ~2,000个Blocks

            - 计算方法

              - 一列数据

                

                - 相对熵（Relative entropy）![img](https://api2.mubu.com/v3/document_image/4de35b1f-7d06-4b79-a753-d29ee56e0816-12251550.jpg)

                - 期望值（Expected Score）![img](https://api2.mubu.com/v3/document_image/0ba13258-157b-4a7f-ac82-ec226017763f-12251550.jpg)

              - 多列数据![img](https://api2.mubu.com/v3/document_image/cc9be9fa-95fa-44bb-9ea8-5bd00f47c41f-12251550.jpg)![img](https://api2.mubu.com/v3/document_image/8398a9b7-a5eb-4da4-a83d-af539e052b8e-12251550.jpg)

          - BLOSUM62![img](https://api2.mubu.com/v3/document_image/b6faadf1-6aaa-408a-af0a-c158d25d01ea-12251550.jpg)
            常用氨基酸打分矩阵
            lod 指数

        - BLOSUM vs. PAM![img](https://api2.mubu.com/v3/document_image/6d1df28e-8a07-4fc5-aecf-d036fde5217d-12251550.jpg)
          BLOSUM系列比PAM系列好

  - k-tuple算法

    FASTA, BLAST

    - 前提：

      

      对于两条序列A, B，若包含少量gap，则最优比对趋近对角线

      - 理论：![img](https://api2.mubu.com/v3/document_image/dd1d1cd3-38b2-4089-a579-4ae797d30029-12251550.jpg)
        令k为一常数，搜索限定区域内的最优比对
        时间复杂度：O(kn)

    - 缺点![img](https://api2.mubu.com/v3/document_image/45e32b89-edfa-48d6-97c8-9a3980d017f9-12251550.jpg)

    - FASTA, BLAST

      启发式算法（heuristic algorithm）

      - 特点

        不能保证搜索到最优的比对
        具有很好的灵敏度，略为降低特异性
        大大缩短序列比对的时间

        - k-tup算法
          字符串匹配
          时间复杂度：< O(n^2)

        - 应用
          大的数据库搜索

      - FASTA

        以短序列构建索引，采用hash表存储方式
        对于需要比较的两条序列，在hash表中查找所有完全匹配的片段；FASTA给每一个匹配给定一个tup值
        产生10个最高分值片段，重新用PAM250打分；
        将同一序列上的高分值区域连接在一起
        采用Needleman-Wunsch或者Smith-Waterman算法对该高分值区域重新打分

        - k-tup
          蛋白质序列：1~2 aa
          ​DNA序列：4~6 nt

        - 索引表构建

          

          - 给定两条蛋白质序列：

            

            Protein1: NCSPTA
            Protein2: ACSPRK

            - 匹配结果

              

              - 序列比对![img](https://api2.mubu.com/v3/document_image/bfadb442-7460-4b9c-949e-25532b59676b-12251550.jpg)

      - BLAST

        蛋白质序列数据库，构建由3aa组成的分值表,采用BLOSUM62矩阵打分
        待查询序列，打断成3aa的片段，在上述数据库中的分值表中进行查询
        保留高于域值的结果，并进行两端的延伸，HSP: high-scoring segment pair
        Nothing can be worse: 牺牲灵敏度，提高计算速度

        Nucleotide BLAST有三个program：
        https://www.ncbi.nlm.nih.gov/Class/MLACourse/Modules/BLAST/nucleotide_blast.html​

        - Word size:
          DNA, 11nt; 蛋白质，3aa

        - 索引表构建

          

          formatdb命令，将fasta格式的序列文件转换成blast能够识别的文件格式

          - 序列匹配![img](https://api2.mubu.com/v3/document_image/855e02ce-02a5-4bb0-86f7-b593f1c024a6-12251550.jpg)

        - 发展

          早期的BLAST版本：无空位罚分
          新版本：Gap Penalties: Existence: 11, Extension: 1

          - Psi-BLAST: 迭代搜索

            

            构建位点特异性矩阵

            - 步骤
              第一步，使用普通的blast算法进行搜索
              第二步，将搜索得到的序列，包括输入的序列放在一起，构建位点特异性的矩阵(Position Specific Matrix)
              第三步，利用上面得到的矩阵谱(profile)，再次在数据库中进行搜索
              重复2，3步，直到不再有新的序列出现

            - 评价
              优点：能够发现序列相似性非常低的同源序列
              缺点：常常得到假阳性的结果

          - Phi-BLAST：
            包含特定模体的序列相似性搜索

  - word算法

- 显著性

  - 显著性检验![img](https://api2.mubu.com/v3/document_image/dbb16d5d-4df0-476b-abed-b60bfc4f1a23-12251550.jpg)
    两条序列在进化上显著相关：

  - 显著性计算

    - 参数

      - Score

      - E-value

    - 贝叶斯方法：模型比较

      

      两个模型：两条序列无关的概率为P(R|x,y)以及两条序列相关的概率为P(M|x,y)
      两个模型的前向概率为：P(M)和P(R)，存在：P(R)=1-P(M)

      - 假设

        

        - 结果![img](https://api2.mubu.com/v3/document_image/23da0339-45ce-4a05-988b-9a7e893d68e3-12251550.jpg)![img](https://api2.mubu.com/v3/document_image/01bdda1b-3fee-46fb-95c0-5ad8b070614f-12251550.jpg)
          R，raw分值
          λ= 0.267
          K=0.0410
          m=208
          n=2,657,097
          ​均可由打分矩阵直接得到

- 同源序列搜索

  同源序列通常具有相似的生物学功能

  - 同源关系的分析

    直系同源 or 旁系同源

    - 直系同源序列的确定
      Reciprocal Best Hits：
      人类Bub1？-> 在酵母中做比对 -> Best Hit!

    - 旁系同源序列的确定
      BLAST，序列比对及数据库搜索，至少存在一个共有的功能结构域

  - 整体分析/蛋白质家族分析
    系统发育树的构建