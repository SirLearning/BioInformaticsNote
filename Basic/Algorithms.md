# 序列比对
## 双序列比对

用于：基于同源序列鉴定的功能预测

注意：
蛋白质一般在三级结构的层面上执行功能
蛋白质序列的保守性决定于其编码DNA的保守性

- 进化假设（序列同源性模型）
  ![img](https://api2.mubu.com/v3/document_image/083b9b3d-9006-41b0-9c0f-3b88e6010c5a-12251550.jpg)
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

## 序列比对

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
## 多序列比对

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

## 序列模式识别

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
# 机器学习

人工神经网络 ANN
- 基础：感知器 (Perceptron)
- 东邪：基因组拼接
  - de Bruijn图算法
- 西毒：进化树分析
  - 近似算法和似然估计
- 南帝：基因和物种分类问题
  - 核函数
- 北丐：统计建模（序列分析）
- 中顽童：判断问题
  - 深度学习
  - 生成对抗神经网络GAN


## 机器学习和数学基础

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

## 深度学习的应用

监督学习

- 分类
	- 简单贝叶斯
	- SVM
- 神经网络
	- 输入层
	- 中间 多层神经网络

无监督学习

- 聚类

### 概貌

机器学习过程：训练 – 测试 – 模型(一个映射函数)

- 三要素：因为机器学习要得到模型来预测未知的问题，可以看到机器学习合传统优化问题有区别
	- 模型：线性/非线性
	- 学习准则：期望风险
	- 优化：梯度下降 – 收敛到局部最优
- 类型：
	- 训练样本
	- 优化目标
	- 学习准则

深度学习：训练层数变得更多

- 层数 – 分元素矩阵变大 – 组合找到特征 – 结合
- 应用：图像领域、语音识别、视频
- 对抗学习
- 神经网络：层次网络结构 – 神经元(输入和输出)
	- 逐层优化，逐层初始化

迁移学习 – 基于深度学习 – 将猫狗的识别模型迁移到人身上

### 基本方法

自然对数

logistic激活函数，sigmoid

逻辑回归：

- 学习效率 – 每次调整的角度

神经网络：

- 输入层
- 隐藏层 – 深度学习多隐藏层 – sigmoid函数
	- 残差反向来传 – 神经网络学习：反向传播
	- 传递之间
		- 卷积(convolution)：把一个大的矩阵变成小的矩阵 – 重叠
			- 特征 – 左小右大，上下相同
			- 整体上特性的一致
		- 驰化(pooling) – 不重叠
			- 最大值驰化
- 输出层

人工神经网络(ANN)

卷积神经网络(CNN)

对抗神经网络(GAN)

强化学习

## 生物大数据挖掘的深度学习

分类 – 有监督

聚类 – 无监督

强化学习 – 有奖赏的

one-hot

对高保守序列 – 可以用强化学习来找特征

- HMM
- BLAST

建模 – 提取特征 – 建立网络

## 习题
### 概念

一、对于真核基因剪接位点识别这一问题，假设依据的信息为位点前后共计d个位置上的碱基序列，请回答

1. 若采用朴素贝叶斯方法，给出一种判别函数并说明需要确定的参数及其个数（4分）

   - 各位点概率相乘，共**4* d* 2+2**个参数

2. 若采用理想贝叶斯方法，给出一种判别函数并说明需要确定的参数及其个数（5分）

   - ln(前验概率* 条件概率密度)，共**4^d* 2+2**个参数

3. 比较上述两种方法的优缺点并给出一种与之不同的贝叶斯方法（10分）

   - 半朴素贝叶斯

4. 若采用 WMM 方法，给出一种判别函数并说明需要确定的参数及其个数（5分）

   - ln(位点概率/背景概率)，共**4* d* 2**个参数

5. 若采用 WAM 方法，给出一种判别函数并说明需要确定的参数及其个数（5分）

   - 共**[4^2* (d-1)+4]* 2**

6. （4）以上三种方法得到的预测效果会是什么关系，为什么？（6分）

   - 根据特征之间关系的考虑程度：

   - 理想贝叶斯>SVM、HMM、ANN>贝叶斯网络>WAM>朴素贝叶斯、WMM

7. 比较上述方法的优缺点并给出一种与之不同的贝叶斯方法（8分）

   1. WMM
      1. 优点：方法简单，涉及的参数少，便于计算和训练；
      2. 缺点：将每个位置出现碱基的概率都考虑为独立的，未考虑之间的相关性，不太符合实际。
   2. WAM
      1. 优点：考虑到相邻碱基之间的依赖性，引入条件概率分布，方法相对简单，涉及的参数也不是很多；
      2. 缺点：仅仅考虑相邻碱基之间的依赖性，忽略了长程关联，在预测时效果也不会太理想。
   3. 理想贝叶斯方法
      1. 优点：考虑到特征之间可能存在的所有依赖性的关系，并将其每种组合都列出概率分布，误差小，预测性能好；
      2. 缺点：参数太多，导致后验概率种类过多，数据量庞大，计算不便。
   4. 另可采用朴素贝叶斯方法，原理与理想贝叶斯相似，但在处理条件概率分布时认为给定类别下特征向量是条件独立的，即P(*x*1,…,*xd*|ω*i*)=∏*s*=1,..,d P(*xs*|ω*i*)，

一、给出基于最小错误率规则的两种理想贝叶斯决策函数；简述理想贝叶斯分类方法的特点与关键问题；分析WMM、WAM方法与理想贝叶斯方法的关系。（20分）

1. 特点：理论上，贝叶斯分类器具有最优的性能，即所实现的分类错误率或风险在所有可能的分类器中是最小的。但贝叶斯分类要求具备以下前提条件：类别数目已知，各个类别的先验概率以及类条件概率密度均为已知（必须是真实情况）；
2. 关键问题：对于高维特征x=[x1,…,xd]，贝叶斯定理中的似然函数（类条件概率密度或概率分布）P(x|ωi) = P(x1,…,xd|ωi)是一个高维分布，如何有效确定该函数是实现贝叶斯分类的关键问题。
3. WMM、WAM方法是理想贝叶斯方法的简化版本，具体来说，WMM是理想贝叶斯最简化的版本，完全不考虑每个特征之间的联系；WAM也是理想贝叶斯简化的版本，但是考虑了相邻特征之间的联系。

**一、**对于贝叶斯分类，请简要回答以下问题：

1. 贝叶斯分类的基本思想是什么？（5分）

   1. 已知类条件概率密度参数表达式和先验概率
   2. 利用贝叶斯公式转换成后验概率
   3. 根据后验概率大小进行决策分类

2. 叶斯分类的关键问题是什么? （5分）

   对于高维特征x=[x1,…,xd]，贝叶斯定理中的似然函数（类条件概率密度或概率分布）P(x|ωi) = P(x1,…,xd|ωi)是一个高维分布，如何有效确定该函数是实现贝叶斯分类的关键问题。

3. 理想贝叶斯、朴素贝叶斯和贝叶斯网络方法各有何优点？（10分）

   1. 理想贝叶斯：理论上，贝叶斯分类器具有最优的性能，即所实现的分类错误率或风险在所有可能的分类器中是最小的
      1. 但贝叶斯分类要求具备以下前提条件：类别数目已知，各个类别的先验概率以及类条件概率密度均为已知
   2. 朴素贝叶斯：参数少，可以实现，简洁
      1. 但是效果不佳
   3. 贝叶斯网络：有用的参数、关系就保留，无用的参数就丢弃，效果会增加；

### SVM

二、对于上题中的问题，现改用支持向量机（ SVM ）方法建立预测模型，请简要回答

1. 线性支持向量机的优化目标是什么？（5分）

   对n个观测样本，找到最优的分类平面

2. 核函数的作用是什么，核函数如何选择？核函数的参数如何确定？（6分）

   将样本映射到新的特征空间，实现在判别函数中的分离

3. 影响支持向量机方法预测效果的主要因素有哪些？（6分）

   训练数据、核函数类型

4. 支持向量机的复杂度取决于什么？

   支持向量和错分的个数，即不为0的α的个数；

二．请设计采用SVM方法识别Donor位点的一个完整方案

1. Selection of Features 特征选择：Fragments of 12 bps around TIS 
2. Data Sets 设置数据集
3. Encoding the sequence 编码序列： A:(1,0,0,0); G:(0,1,0,0); C:(0,0,1,0); T:(0,0,0,1)
4. Selecting Kernel function 选择核函数
   1. 核函数作用：避免了直接在新的超高维平面设计支持向量机的麻烦；做了一个隐含的映射，避免了显性的映射；
   2. 类型和参数的确定：尝试，选择效果最好的
5. Designating Parameters 设计参数

实际应用中支持向量机方法的潜力主要受哪些因素制约？

- 对大规模训练样本难以实施、解决多分类问题存在困难

**二．**请根据“利用支行向量机方法预测真核基因剪接位点”这一综合训练内容简要回答以下问题： 

1.  (1) 所采用的特征向量的维数是多少（4分）

   碱基分布：4

2.  (3) 线性支持向量机的优化目标（准则函数）是由哪两部分组成的？（4分）

   第一部分是经验风险最小；第二部分是推广能力最大

3.  (4) 支持向量机方法解决线性不可分问题的思路是什么？（4分） 

   映射到更高维的特征空间，使其可分。

4.  (5) 支持向量的个数与用于训练支持向量机的样本数之间是什么关系？（4分） 

   支持向量的个数远小于用于训练支持向量机的样本数

### ANN

三、对于上题中的问题，现采用单隐层前馈神经网络建立预测模型，请简要回答

1. （1）模型的输入层和输出层分别有多少个节点？（5分）

   输入层有d个，输出层有1个

2. （2）隐层的作用是什么？隐层节点数如何确定？（7分）

   1. 作用：为了是模型能够执行和学习任何功能，对输入数据进行处理。降低网络误差（也有文献认为不一定能有效降低），提高精度，但也使网络复杂化
   2. 确定节点数：针对训练样本数确定，必须小于N-1，与需解决的问题的复杂程度和转换函数的型式以及样本数据的特性等因素有关。在满足精度要求的前提下取尽可能紧凑的结构，即取尽可能少的隐层节点数。

3. （3）该模型与上一题的 SVM 模型有哪些相同之处和不同之处？两者的预测准确性可能会是什么关系？（8分）

   1. 相同：都是映射，都属于浅层机器学习模型
   2. 不同：显性和隐性
      1. 人工神经网络是以传统统计学为基础，其研究的内容是样本数据趋于无穷多时的统计性质，适用于超大样本数据，且可轻松从二分类拓展到多分类；
      2. 支持向量机则是以统计学习理论为基础,不涉及概率测度及大数定律等，计算的复杂性取决于支持向量的数目，避免了“维数灾难”，克服了神经网络中的“过学习问题”。更适用于小样本数据，且在多分类问题上不能直接运用。

4. 实际应用中人工神经网络方法的潜力主要受哪些因素制约？

   1. 易出现“过拟合”、易陷入局部最优

### HMM

四、对于隐马尔科夫模型（ HMM ）方法，请间要回答

1. HMM 的建立与应用需要解决哪些问题？（5分）
   1. HMM的结构
   2. 估计问题：根据一个O，建立一个M，在给定M下评估该序列的概率
   3. 解码问题：找到O最可能通过M的路径Q
   4. 学习问题：根据给出的O，来对M进行优化，其中可能存在Q。确定模型M参数
2. 给出采用 HMM 方法预测蛋白质二级结构的一种模型拓扑结构，并给出该模型需要确定的参数类型与个数。（10分）
   1. 有helix、coil、strand三种状态，根据序列编码特征向量，先进行训练而后在交叉检验后，使用模型对给定蛋白质的二级结构进行预测
   2. T: 3* 20* 3=180; E: 20* 3* 20=1200，共1380个参数

请根据以下一组保守序列片断的多序列比对结果，给出：

1. 描述该保守序列片断的隐马尔可夫模型（HMM）结构图；
2. 该HMM的状态转移概率矩阵（Transition matrix）和生成概率矩阵（Emission matrix）。（15分）

四．对于如图（A）和图（B）所示的两组保守序列片断的多序列比对结果，分析各适合用什么模型描述，并简要说明理由（15分）

1. 图A：有空格，隐马尔可夫模型，存在若干个不可观测的隐状态；
2. 图B：无空格，WAM或者WMM模型或SVM或贝叶斯网络，不存在隐状态；

### 特征向量

五、当采用支持向量机或人工神经网络等方法建立分类模型对蛋白质序列的功能进行分析时，需要先选取某些特征将长度任意的蛋白质序列编码成固定长度的特征向量。请设计一种能综合考虑各氨基酸的组成情况及其在序列长度上的分布情况的编码方案，并给出最终所得到的特征向量的维数。（15分）

1. 组成：**C=20**
2. 转换：**T=20* 20**
3. 分布：**D=20* 5* 4**
4. 共500维

给出考虑氨基酸组成及其疏水性（三种）将长度任意的蛋白质序列编码为固定长度特征向量的一种方案，并给出该特征向量的维数（15分）

1. C：3 
2. T：3* 3=9 
3. D：4* 3=12（四等分）
4. 24
5. 加上氨基酸组成，共524维

### 论述题

六、如果遇到类似真核基因剪接位点识别这样的研究课题，你认为应从哪些方面开展研究。（10分）

1. 6-mer等

五．对于Donor位点预测这一问题，目前你已了解了WMM、WAM、贝叶斯网络、SVM、ANN等方法

1. 你认为这些方法的预测准确度是一个什么顺序？（5分）
   1. SVM、HMM、ANN>贝叶斯网络>wam>wmm
2. 为了进一步提高预测性能，你认为应从哪些方面开展工作。（15分）
   1. 数据，质量，数据量，优化数据集的质量，保证原始数据的正确性。
   2. 特征之间的关系，有用的，优化特征的选取。对于深度学习来说，自动选取特征是难以实现的。对于图像识别来说，原始特征就是原始数据。
   3. 更有效的先验知识，虽然关注的是donor位点，但可以站在更高的层次去研究，可以站在编码区，基因结构的层面去研究。
   4. 更强的计算能力
   5. 更好的模型结构，只考虑有用的，模型的选择：选取donor位点的模型有很多，但是没有理论告诉我们哪种模型最好。可以尝试多种模型以及多种模型的结合

六．简要总结：

1. 你在本课程上机实践训练中所完成的内容、遇到了哪些困难、思考了哪些问题；（10分）
   1. 真核基因剪接位点预测的WAM模型编程实现中：
      1. 完成了：特征的提取（选取剪接位点前3个和后4个位置碱基信息）、训练集数据的提取和表示，统计算出WAM条件概率模型（包括P+和P-，用二维数组表示）、设置初始C值对测试集数据依次滑动进行打分、计算Sn和Sp、修改C值并作出了曲线，从图中选取Sn、Sp较理想的C值
      2. 遇到的困难：如何批量读取文件并将其中的数据输入到二维数组中
   2. 利用SVM方法预测真核基因剪接位点中：
      1. 完成了特征提取与数据编码、核函数的选择（高斯核）、参数学习
      2. 遇到的困难：核函数的选取和参数的确定
2. 通过本课程的学习与训练你有哪些收获。（5分）
   1. 了解和学习了WMM、WAM、贝叶斯网络、理想贝叶斯、SVM、HMM、传统ANN、深度神经网络等数据挖掘方法，明白了这些方法的基本原理以及能逐步应用这些方法去解决一些生物信息学研究中的问题。
   2. 分析问题和解决问题的能力得到了提升，对我们生信专业有了更深层次的认识。


# 生物背景+课程简介

SMMLB: Statistical Modeling and Machine Learning for Biology

## 课程简介

## 统计学

F检验 – 大数定理 – 贝叶斯推论 – 正态分布 – 方差 – 箱式图

样品选取：

- 选取多少小麦才能确保结果的准确性？
- 阿司匹林对抗癌的疗效（也有可能是其他抗癌的药物）

确定关联性

要求：

1. 基本原理
2. 基本公式
3. 科学的统计思维方法

贝叶斯推论：
$$
P(X|Y)=\frac{P(Y|X)P(X)}{P(Y)}
$$
统计学和机器学习：

- 如果你只是想从数据中找出哪类人更容易得某种疾病，机器学习可能是更好的选择。
- 如果你希望找出变量之间的关系或从数据中得出推论，选择统计模型会更好。

## 生物信息

测序

测序应用

- 产前诊断
- 癌症诊断

结构生物学

生物图像

生物现象特点：

- 变异性：个体之间差异
- 不确定性（随机性）：变异不能准确推算
- 复杂性：影响因素众多，有些是未知

基因表达数据分析

1. 差异表达基因分析
2. 基因共表达分析
3. 基因表达数据的聚类和分类
4. 基因集分析
5. 基因调控网络

基因集合分析

1. 测序一批“interesting”的基因
	1. 差异表达基因
	2. 直接做基因集分析
2. 生物学功能关联 – 某种功能是否显著
3. 计算分析方法
	1. gene ontology
	2. KEGG
	3. 超几何分布

微生物组生态数据分析

1. 物种的富集分析
2. 功能的富集分析
3. MWAS分析

## 计算科学

The art of computer programming, Donald Knuth

基因检测，比尔盖茨：sorting by reversal problem

PatternHunter, ExonHunter

Alphabet

深度学习：

1. Reinforcement Learning
2. Markov chain
3. visual recognition

机器学习：

1. 数据特征提取
2. 数据预处理
3. 训练模型
4. 测试模型
5. 模型评估改进

算法：

1. 回归 – 线性回归
2. 分类：
	1. 逻辑回归：通过Sigmoid函数将线性函数的结果映射到Sigmoid函数中，预估事件出现的概率并分类
	2. k-近邻：用距离度量最相邻的分类标签
	3. 朴素贝叶斯：$P(\omega_j|x)=\frac{p(x|\omega_j)P(\omega_j)}{p(x)}$, $p(x)=\sum_{j=1}^Np(x|\omega_j)P(\omega_j)$
	4. 决策树：构造熵值下降最快的分类树
	5. 支持向量机(SVM)：构造超平面，分类非线性数据
3. 聚类 – k-Means：计算质心，聚类无标签数据
4. 关联分析 – F-P Growth：频繁项集、关联规则、支持度、置信度
5. 降维 – 主成分分析PCA：降低数据复杂度，提高识别的精度
6. 人工神经网络：对数据之间的复杂关系进行建模，逐层抽象，逼近任意函数
7. 深度学习

## Topic

Sequence’s feature detection

- CpG island finding
- Gene finding:
	- promoter prediction
	- splicing site prediction
	- translation initial site prediction

Multiple alignment

Tree of life

- Phylogeny
- classical: morphological characters
- modern: molecular sequences
- appoaches
	- probabilistic model 概率模型
	- bootstrap 引导程序

Motif finding

Gene expression data – clustering and biomarker discovery

- microarrays

Regulatory network

- network inference
	- Bayesian network
	- Gaussian graphical model

Network analysis

- network modular (network clustering)
- network motifs

Dimension resuction

- curse of dimensionality
- techniques:
	- principal component analysis, PCA
	- singular value decomposition, SVD
	- multi-dimensional scaling, MDS
- visalization in low dimension

# 传统生物统计学

## 名词

### 概率统计

大数定理：伯努利 – 卡方检验

贝叶斯推论：利用看到的序列信息（事实），反过来推论到哪里是特定位点（剪切位点）

正态分布 – 方差 – 箱式图

t分布、t检验（学生式分布）：歌塞特，小样本检验替代大样本

F检验 – 方差分析：费歇尔 – Fisher Yates随机数字表

马尔科夫链 – mutual information

#### 基本内容

1. 

1. 

总体

样本：30

变量：

常数

参数：描述总体特征的数，通常未知

统计数：描述样本特征的数，样本观测值的已知函数

效应：

互作（连应）

变异 – 误差：

1. 随机误差/机误(random error)
2. 系统误差/错误(systematic error)

准确性

精确性

## 理论

统计分析：

1. 数据特征数的计算
2. 方差分析
3. 卡方检验
4. 回归和相关分析
	1. 孟德尔随机性
5. 协方差分析
6. 主成分分析
7. 期望最大化（EM）算法
8. 聚类
9. HMM模型（基因预测）

基本原则：重复、随机、局部控制

抽样：

1. 随机抽样：
	1. 简单随机抽样：抽签法，随机原理
	2. 分层随机抽样：区层，抽样分数，局部控制原理
	3. 整体随机抽样：群（主要变异来源明显来自区层内各区间，每一区间所占面积较小）
	4. 双重随机抽样
2. 顺序抽样（系统抽样、机械抽样）：按照既定顺序抽样，不能计算抽样误差、估计总体值
3. 典型抽样：主观选取典型群体作为样本，一般不在总体相对较小时用

统计归纳：变量分布具有集中性、离散性的特征

1. 集中性 – 平均数
	- 算数平均数：$\mu=\frac{1}{N}\sum^N_{i=1}x_i$
	- 几何平均数：$G=\sqrt[n]{x_1x_2...x_n}$
		- 适用于变量x为对数正态分布，经对数转换后成正态分布的资料
	- 调和平均数：$H=\frac{1}{\frac{1}{n}\sum\frac{1}{x}}$
		- 主要用于反映生物不同阶段的平均增长率或不同规模的平均规模
	- 中位数：$M_d$
	- 众数：$M_0$
	- 箱式图（box plot）: maximum, third quartile(Q3), median, first quartile(Q1), minimum – IQR=Q3-Q1
2. 概率分布 – 随机变量的概率分布
	- 离散型变量
		- 二项分布
		- 泊松分布
	- 连续型变量
		- 正态分布
3. 离散型 – 变异数
	- 极差
	- 方差
	- 标准差
	- 变异系数

假设推断

- 假设检验：显著性检验
- 假设推断：

变量间关系

- 函数关系（确定性）：数学表达式
- 统计关系（非确定性）
	- 因果关系（回归分析）
		- 一元回归：直线回归、曲线回归
		- 多元回归：多元线性回归、多元非线性回归
	- 相关关系（相关分析）
		- 简单相关分析：直线相关分析
		- 多元相关分析：复相关分析、偏相关分析

相关性分析：

- 直线关系
	- 正向直线关系
	- 负向直线关系
	- 直线回归方程：自变量、斜率（回归系数）、截距（回归截距）、y估计值
		- 最小二乘法
			- 点到直线的距离：$d=\sqrt{\frac{1}{k^2+1}}(y_1-(kx_1+b))$
		- 绘制散点图 – 观察趋势 – 检查异常点
		- 以自变量的取值为限：内插、外延

- 曲线关系

- 函数：对数、指数、幂函数、倒数、S形曲线

实验设计：

1. 对比设计
2. 随机区组设计
3. 裂区设计
4. 拉丁方设计
5. 正交设计

陷阱：深度学习得到的特征与样本无关

## 应用

基因差异表达

- 热图
- t-test

基因表达和性状关联性分析

基因分型

结构预测：打分函数

实际操作

生物大数据可视化

# Markov Model（马尔可夫模型）

## Markov Chain



$$
\begin{bmatrix}
P_{aa}&P_{ab}&P_{ac}\\
P_{aa}&P_{ab}&P_{ac}\\
P_{aa}&P_{ab}&P_{ac}\\
\end{bmatrix}
$$
只与上一次的吃饭地点有关

### 时齐马氏链

零阶马氏链

一阶时齐

可达 – 互通 – 不可约

常反

周期

遍历极限：

### page rank算法

网络搜索

page rank – 网页跳转访问矩阵

死网页问题 – damping factor:

MapReduce(处理过多的网页，巨大的矩阵)

## Hidden Markov Model (HMM) 理论

自己设计输入X<sub>i</sub>值，讲解，看人们穿的衣服来判断天气。

由观测值推测状态 – HMM参数较多

- 转移概率矩阵

计算方法：

- 隐过程
- 初始分布
- 转移矩阵
- 分布矩阵

识别问题 – &lambda;表示一个模型，利用Bayesian原理，猜测最好模型

- 基本（枚举复杂度2TN<sup>T</sup>）：

	- $$
		Pr(Y=y|\lambda)=\sum_{X=x}Pr(Y=y|X=x,\lambda)Pr(X=x|\lambda)=\sum_{x=(x1,...,x_T)}\pi(x_1)b_{x_1}(y_1)a_{x_1x_2}b_{x_2}(y_2)...a_{x_{T-1}x_T}b_{x_T}(y_T)
		$$

- 前传概率：

	- $\alpha_t(i)=Pr(y_1,y_2,...,x_t=i|\lambda)$，&lambda;表示一个模型
	- $\alpha_{t+1}(i)=Pr(y_1,y_2,...,y_{t+1},x{t+1}=i|\lambda)\\
		=\sum_j\alpha_t(j)a_{ji}b_i(y_{t+1})$
	- Forward Algorithm:
		- 初始 – 迭代 – 结果：$Pr(Y|\lambda)=\sum_{i=1}^N\alpha_T(i)$

- 后传概率：
	- $\beta_t(i)=Pr(y_1,y_2,...,x_t=i|\lambda)$
	- $\beta_{t}(i)=Pr(y_1,y_2,...,y_{t+1},x{t+1}=i|\lambda)\\
		=\sum_j\beta_t(j)a_{ji}b_i(y_{t+1})$
	- Forward Algorithm:
		- 初始 – 迭代 – 结果：$Pr(Y|\lambda)=\sum_{i=1}^N\beta_1(i)\pi_ib_i(y_1)$

解码问题 – Viterbi算法：

- 原则：
	- 单点最优
	- 路径最优
- 初概率
- 转移概率
- 条件概率

学习问题 – 由隐过程和过程来推算转移矩阵和分布矩阵 – 根据频率推算

- 极大似然估计
- 观测链相应的状态链已知
- 观测链相应的状态链未知 – 参数估计（EM思想）
	- EM算法（最大期望算法）：无法确定是否最优解，只是局部最优解

## HMM基因识别

CpG岛的识别

- BLOSUM62 – 状态链部分知道

gene识别

区别于底层模型 – 密码子要3个一组来考虑

geng scan – 更多考虑

药物测试

生存分析

蛋白预测

## HMM序列比对

# 进化树的概率模型

基础比较还是序列

研究热点：研究和改造进化

生物伦理：

- 可以做：老年人病入膏肓
- 不能做：新生儿
- 模糊地带：未得疾病之前就做改造

概率方法构建：二叉树

- 基于距离构建

	- UPGMA：	
		- 构建t*t矩阵
		- 寻找自小距离： 
	- Neighbor-Joining

- 基于特征构建

  - 最大简约法(Maximun Parsimony)
  	- occam’s razor method, 奥卡姆剃刀法：解释一个过程最好的理论是所需假设数目最少的一个
  	- 计算所有拓扑结构 – 代数最小的一个
  - 最大似然法(Maximum Likelihood)
  	- 似然函数
  	- 排列组合 – 54321
  	- 分子钟假设
  		- 水平基因转移 – 基因交流 – 设不成立
  	- 递归算法：
  		- ungapped alignment: 
  		- PAM矩阵

  # Motif finding的概率模型

## EM algorithm

example – 知道状态链的学习问题

EM – 永远得不到最优解

- 随机构建一棵树的结构
- MLE(cont)
- Z的设计
- 投硬币：
	- 每次投的时候知道用的是A还是B – 最大似然估计(ML)
	- 未知每次投的时候是A还是B – 最大期望法(EM)
- k-mean: 中心化，无法求环
- Hcluster(层次聚类)
- 和函数：将肉眼可看的分成不同维度
- 二维聚类：EM clustering – 每个点都有概率 – 不计算距离，计算概率
	- 高斯混合模型：两个高斯分布(正态分布)混合一起
	- 高斯函数：$f(x)=ae^{-\frac{(x-b)^2}{2c^2}}$
	- 高斯函数积分：$\int^{\infty}_{{-\infty}}e^{-ax^2}dx=\sqrt{\frac{\pi}{a}}$
	- GMM-EM

## Markov Chain Monte Carlo (MCMC)

避免给定起点对结果的影响，上山之后再下来 —— 模拟退火

### Monte Carlo

会适用于一种分布

Monte Carlo有一定的随机性

随机数：

- Linear congruence generator (LCG)：生成随机数，求模运算 – 密码学
	- 参数选择，很严谨(M)
	- Public key system (公钥) – 密码学：
		- 私钥 – collision attack

twin prime conjecture (哥德巴赫猜想) – 7000万

### MCMC

马氏链遍历性

应用：

- 生成复杂随机数 – 高维分布的随机向量
- 复杂空间上的极值 – 模拟退火：上山后下
- Gibbs Sample
- Metropolis
- Hill climbling

### Motif Finding

模体：一段序列在不同生物里面都保守 – 序列保守，长度短(模体是从序列上说的)

化学方法：DNase footprinting assay

motif特性：small & highly varible(与基因的距离多变)

最大似然估计(ML) – 只能从序列角度，要从更多的前后序列来判定

判定变量：

- 信息熵：保守型越强，熵越低
	- PWM：直接算各位点概率
	- Information – Entropy: H(x) =$2-\sum_{i=\{A,T,G,C\}}-p_i\log_2{p_i}$
	- 加入背景频率(background frequency)
		- different measure – Kullback-Leibler distance(divergence): $D_{KL}(P_{motif}||P_{bg})=\sum_{b=\{A,T,C,G\}}P_{motif}(b)\log\frac{P_{motif}(b)}{P_{bg}(b)}$
	- 保守型(以2为底的信息熵)和字母结合的图
- 互信息(Mutual information)

Assumption:

- one sequence, one motif
- has fixed length

parameter:

- $X_i$: ith sequence(观测值)
- $Z_{ij}$: motif start at position j in sequence i – 对应PWM

multinomial distribution: $Pr(X_i|Z_{ij}=1,p)= \prod_{k=1}^{j-1}p_{x_{ik},0}\prod_{k=j}^{j+W-1}p_{x_{ik},k-j+1}\prod_{k=j+W}^{L}p_{x_{ik},0}$

- motif – PSSM(:,1:n)
- background – PSSM(:,0) – $p_{x_{ik},0}$ – P(S|B)
- EM updating
	- L: 序列总长
	- W: 模体长度 

MEME Algorithm

- 不定开始位置，多判断，相比于直接固定序列位置来迭代，更加
- estimating p: 加1和4，防止结果出现0

MEME工具：

- 多起点爬山不能得到准确的最高点

Gibis采样

1. 后三条找模体 – 得矩阵 – 在第一条序列上用

# 基因表达数据分析

## 聚类分析 – Mixture model

判别问题 – 学习问题

机器学习分类：

- 监督学习 – 一开始就有分类 – 分类、回归
- 无监督学习 – 一开始没有标签，自己去找分类 – 聚类、相关性、降维
- 强化学习

聚类(cluster)工具

分等级聚类

相关性：

- 皮尔森相关性
- 欧几里得(Eud)相关性
- cosine相关性
- 傅里叶变换

KNN

连接：

- 单向连接 – 很多，但二维是一串
- 最远
- 最近
- 算中心点距离

K means

高斯混合模型 – EM算法

判断分几类(有多少个聚类点)：

- AIC
- BIC
- log-likelyhood：一个个尝试

## Classification-Lasso Based variable selection

类别预先就知道，把样本分到组里面去

### Bayesian decision rule

统计上的分类问题 – 贝叶斯的决策问题

### Fisher linear discriminant analysis

Fisher判别分析 – 组间最大，组内最小

- 过原点斜率变化 – 变化时可能跳过最大

### SVM

保证分开后，中间的空白越开越好

- 核函数 – 置换空间

拟合：

- 欠拟合
- 过拟合问题(overfitting) – 分的太好，再加一个点可能就不是那么好
	- 数据：
		- 训练数据：可以看到的数据
		- 验证数据
	- 均方误差(MSE)：$MSE=\frac{1}{n}\sum^n_{i=1}(y_i-f(x_i))^2$
	- 训练MSE减小，测试MSE变大 – 过拟合
	- 留一交叉验证
	- k折交叉检验：每次留几个

### 衡量分类器 – Measuring the accuracy of classifers

|                  | real negative     | real positive     |
| :--------------- | ----------------- | ----------------- |
| claimed positive | false positive FP | true positive TP  |
| claimed negative | true negative TN  | false negative FN |

参数：

- sensitivity (Sn): $\frac{TP}{TP+FN}$
- false positive rate (FPR): $\frac{FP}{TN+FP}$
- specificivity: 1-FPR
- correlation coefficient (CC): $\frac{TP\times TN-FP\times FN}{\sqrt{(TP+FN)(TN+FP)(TP+FP)(TN+FN)}}$
- approximate correlation (AC): $\frac{1}{2}(\frac{TP}{TP+FN}+\frac{TP}{TP+FP}+\frac{TN}{TN+FP}+\frac{TN}{TN+FN})-1$
- FDR: $\frac{N_{01}}{N_r}$
- F<sub>1</sub> score

ROC(receiver operating characteristic/relative operating characteristic)

- 分类器，Sn上升，FPR也上升，正常是对角线和偏上的二分类，这样才有用(但在实验中可能是弯曲的)
- 偏上：分离较好
- 直线：完全分不开
- 向下：全错

假设检验：

- 一型错误(type I error)：原假设正确，却拒绝了原假设 – $N_{01}$
- 二型错误(type II error)：原假设错误，没有拒绝原假设 – $N_{10}$

### Aggregating classifiers

参数不同，结合起来成为一个大的分类器 – 整合，每次换参数

随机森林(random forest, 集大成的分类器)：将判别树的结果整合，作为最终结果

- 投票

### 校正(correction)

Bonferroni method

Benjamimi method

- 通过控制FDR来决定P值的阈值
- FDR < 5%
- 造数据decoy

## gene expression classification

RNA-seq – RPKM/FPKM：数据规划

- FPKM：$FPKM=10^9\times\frac{C}{NL}$

GSEA：显著高于/显著低于所有的基因表达

## 参数选择(variable selection)

stepwise：一次去掉一个，看结果会不会更好

数据降维：

- LASSO：用正方形来切
- 岭回归(ridge regression)：用圆来切

## class comparison

# 基因网络推断

## Regulatory network

### 调控网络

可进行因果推断 – 因果性：不可反向

- 共出现 – 癌症基因与得癌症的因果性

有调控性，相关性：

- 无法通过统计方法来设计因果性：先后性
	- 只有一种方法 – 孟德尔随机化
- 实验方法简单

网络：

- 无/非尺/标度网络(scale-free network) – 连接其他点的个数分布 – 基因/社交网络
	- 正常是连接边个数正态分布，但在自然界中不常见
	- 世界上最多6个的社交圈

Clarify:

- 统计：共高或共低
- 实验：CRISPR

调控关系：震荡

### reverse engineering

逆向工程：测试一个个部件，推导整体的功能

DREAM挑战赛

### Bayesian网络

把网络变成有方向的 – 因果网络

整件事发生的概率：$P(B,E,A,C,R)=P(B)P(E)P(A|B,E)P(R|E)P(C|A)$

初级：参数学习

- 一条边 – 找到贝叶斯概率(用频率代替概率)

中级：图分解

- 找有几个概率 – 分成子网络
- 没有箭头：独立概率
- 有箭头：条件概率

高级：近似算法 – 关于图的

- 贪心算法：每次改变一个边，最后得到最可能的
	- $\Delta score=$
	- 看能不能达到局部最优
- stepwise

特级：EM算法解网络

- EM算法：
	- 通常有H隐状态
	- 数量N：
		- 独立：1
		- 条件：2<sup>n</sup>
	- training data：几个变量发生的频率
	- 参数更新
	- 结构更新

两者关系

功能网络：GO

## Gaussian Graphical Model

# 蛋白质相互作用

## 实验方法

### 物理作用

酵母双杂交 – 有人为选择因素 – 可靠性不是很高

质谱 – TAP-mass spectrometry – 组学

### 基因作用

组学的研究

很多时候说相互作用 – 从数据上说 – 同出现/共表达

数据库很多 – 其中能有实验验证的很少(10%) – 大多是预测

## P-P相互作用的预测

通过蛋白表达量来推断

证据：

- 共出现 – 时间上 – 空间上cellular location
- 结构互补配对

pfam：

- 域 – 线性排列

association：$V(D_{ij})=\frac{interacted protein pairs contain D_{ij}}{all protein pairs contain D_{ij}}$

## Network Module

difination

module detection

Bayesian approach

Markov clustering algorithm – MCL(马尔可夫聚类)

- 矩阵乘法

DB：

- STRING
- STITCH

## 蛋白质3D结构

### 结构预测

Rosetta stone

CASP(critical assessment of techniques for protein structure prediction)

- 13：DeepFold
- 14：AlphaFold – AlphaFold2
	- 中位GDT

微生物组大数据+蛋白质3D结构

- 非定向/定向方法 – 发掘未知功能基因
- 合成生物学模板
- 药物发掘/药物设计
	- 环境菌群 – 功能基因/代谢物

### AlphaFold2

数据库

### P-P相互作用

dock – 蛋白质复合物(冷冻电镜唯一的优势所在)

David Baker

Colabfold

### 蛋白质动态变化

### 蛋白质设计

ProteinMPNN

## 基因网络分析

## Network clustering

## Network Motif

## Markov random field (MRF)

# Dimension reduction(降维)

降维 – 让人能看到识别数据特征

高维 – 超平面分类 – 过拟合问题

维度爆炸 – 维度降低，准确度无法保证

## 特征选取

Feature selection – 选足够好的维度，降维后可以分很开

所有压缩问题都是特征选择的问题

很多特征相关性非常高 – 只考虑一个就有足够的代表性

### 最小冗余，最大相关 (mRMR)

### 随机森林

做决策需要几个关键特征 – 特征筛选

## 降维

映射的结果 – 判断依靠降维的方法

- 线性降维：降维时特征一样的要在一起 – 有分类的功能，但原始功能是降维
	- PCA 主成分分析 – 基因表达中主要的
		- 主成分：选取的代表原始样本的特征 – 根据样本方差最大
		- 可能不会得到肉眼可见的结果
	- LDA 线性判别分析
		- 同类接近 – 难以进一步分析，无法对同类里面做进一步分析
		- 不同类分离
	- 要素分析
		- CCA 典型相关分析 – 将数据X映射到二维平面上，用factor的Y来对这些点进行标记
			- 向外延伸的长度越长，越重要 – 将样本分的越开，越重要
		- SVD 奇异值分解 (singular value decomposition)
			- x – 基因
			- y – 样本
			- 样本排序 – 将基因表达信息聚类
- 非线性降维
	- MDS 多维尺度分析
		- 构造低维空间的内积矩阵 – 低维矩阵中两点距离和高维中一样
		- t-SNE – 单细胞表达
- LASSO
	- 核函数 kernel function – SVM

