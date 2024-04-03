# 概念

定义：科学计算平台

## 数与图表

有效数字：

- 近似值的最后一位数字与真实值的误差小于最后一位数的0.5个单位（也就是最后一位的后一位四舍五入）
- 到达最后一位的有效数字的个数为有效数字的位数

绝对误差：

- 真实值很难测，只能估计范围，故有绝对误差限&eta;：反映了近似值x*的可信赖程度

相对误差：除以近似值

- 相对误差限&delta;

泰勒级数：

- f(x)在x~0~的某个邻域内有n+1阶导数：
  $f(x)=f(x_0)+f'(x_0)(x-x_0)+\frac{1}{2!}f''(x_0)(x-x_0)^2+\cdots+\frac{1}{n!}f^{(n)}(x_0)(x-x_0)^n+R_n(x)$
  $R_n(x)=\frac{f^{(n+1)}(\xi)}{(n+1)!}(x-x_0)^{n+1}$
- 根据提取需要的级数来得到逼近函数，此时会带来截断误差，用余项公式R~n~(x)来计算
  - 当f^(n+1)^(&xi;)在&xi;&in;(x~0~, x)（假设x~0~<x）中存在最大值M：R~n~(x)&leq;O(h^n+1^)（h为步长：x-x~0~）
- 误差传递
  - 一元函数：$\Delta f(x^*)=|f'(x^*)|(x-x^*)$
  - 多元函数：$\Delta f(x^*_1,x^*_2, \cdots, x^*_n)\approx |\frac{\partial f}{\partial x_1}|\Delta x^*_1+|\frac{\partial f}{\partial x_2}|\Delta x^*_2+\cdots+\frac{\partial f}{\partial x_n}|\Delta x^*_n$
- 计算机计算规则：
  1. 相近数相减会丢失有效数字
  2. 浮点溢出：
     1. 绝对值太小作为除数
     2. 两加数指数向大指数对齐，再将浮点部分相加，取单精度会导致小的数消失
        - 单精度((float)：1位符号，8位指数，23位小数(2^-23^&approx;1.9*10^-7^，故小数部分只能精确到后面6位，加上小数点前1位，有效数字为7位)
        - 双精度(double)：1位符号，11位指数，52位小数(2^-52^&approx;2.2*10^-16^，故小数部分只能精确到后面15位，加上小数点前1位，有效数字为16位)，在MATLAB中用eps表示
          - 正无穷大：1/0，用inf表示
          - 非数：0&times;inf
          - 虚数单位：i, j
          - 浮点运算数：flops (float operation per second, 每秒可支持的浮点运算数)，衡量一个设备计算能力的指标
  3. 简化计算步骤：$x^64=x*x^2*x^4*x^8*x^{16}*x^{32}$
  4. 模型误差、测量误差

统计图表：

- 统计表：易于参考比较，形式紧凑。表号、表题、横(行)标题、纵(列)标题、分割线、数字资料、表注
  - 调查表
  - 汇总表
  - 分析表
- 统计图：反映数据的变化趋势和变化特点。图号、图题、轴标、数轴、图注、图线、误差棒(箱图上下的棒)
  - 散点图、折线图：变量间关系
  - 柱状图、条形图：数据多少和数据间差别
    - 直方图、频率直方图：连续变量的柱状图
  - 饼图：数据系列中各项的大小比例
    - 复合型饼图、分离型饼图、三维饼图
  - 曲线拟合图：数据变化趋势

## 特点

计算功能强：数值计算、符号计算、计算可视化

- 矩阵变换及运算、多项式运算、微积分运算
- 线性与非线性方程求解、常微分方程求解、偏微分方程求解
- 插值与拟合、特征值问题、统计及优化问题符号工具

语言简单：用C语言开发

扩充能力和可开发性强：解释执行函数程序、开放系统，和Fortran、C等语言接口

- 只需将exe文件改成mex文件就可方便调用有关程序

工具箱：

- 功能工具箱：
	- matlab main toolbox
	- control system toolbox
- 生物学工具箱
  - Bioinformatics：分析基因组和蛋白质组的软件环境
  - SimBiology：集成图形环境中的建模、仿真和分析生物学系统的工具

# 基础

## 常用字符和函数

符号：

|  符号   |              取值               |
| :-----: | :-----------------------------: |
|   ans   |          结果省缺变量           |
|   pi    |             圆周率              |
|   eps   | 2^-52^, 计算机最小数，$1+esp>1$ |
|  flops  |           浮点运算数            |
|   inf   |           1/0, 无穷大           |
|   NaN   |    0/0, 0&times;inf, 不定量     |
|   i,j   |           $\sqrt{-1}$           |
| realmin |           最小正实数            |
| realmax |           最大正实数            |
| nargin  |        函数输入变量个数         |
| nargout |        函数输出变量个数         |

字符：

```matlab
; %各行隔开，不显示结果
, %各行隔开，显示结果
... %余下部分下一行出现
```

函数：

|  函数   |   名称   |   函数   |     名称     |
| :-----: | :------: | :------: | :----------: |
| sin(x)  |   正弦   | asin(x)  |    反正弦    |
| cos(x)  |   余弦   | acos(x)  |    反余弦    |
| tan(x)  |   正切   | atan(x)  |    反正切    |
| abs(x)  |  绝对值  |  max(x)  |    最大值    |
| min(x)  |  最小值  |  sum(x)  |   元素总和   |
| sqrt(x) |  平方根  |  exp(x)  |   自然指数   |
| log(x)  | 自然对数 | log10(x) | 以10为底对数 |
| sign(x) | 符号函数 |  fix(x)  |     取整     |

数据显示格式：Format命令

```matlab
Format short
Format long
Format short e	%5位浮点表示
Format long e	%15位浮点表示
```

## 矩阵、变量、运算、表达式

矩阵：

```matlab
A = [1,2,3;1 1 1
	 4 5 6]
who		%who, whos命令显示已定义的变量及有关维数信息
% 运算
a+b		%四则运算
a\b		%左除。矩阵右除要先计算矩阵的逆再做乘法，左除不需要，故通常右除慢一些
a^b		%幂运算，和乘、除一样，参加的矩阵必须为方阵
inv(a)	%求可逆矩阵
y = x'	%求转置
% 数组
a.*b	%运算
```

向量

```matlab
x = [a b c]
x = first:increment:last
linspace(first,last,n)		%创建从first开始到last结束，包含有n个数据元素的行向量
A(:,1)	%矩阵A的下标
A(:)	%将矩阵A所有元素排成一个单列
```

运算符

```matlab
% 关系运算符
<	%小于
<=	%小于等于
==	%等于
~=	%不等于
% 逻辑运算符
&	%与
|	%或
~	%非
xor	%与非
```

函数m文件：运行的都是局部变量

```matlab
function 因变量名=函数名(自变量名)
```

脚本m文件：运行的全部都是全局变量

## 绘图和控制语句

图形函数：

```matlab
% 条形图，直方图
bar(Y)
bar(X,Y)
bar(...,width)	% 设置带宽
bar(...,'style')	% 取 'grouped'/'stacked'，默认为 'grouped'
bar(...,'bar_color')
barh	%水平条形图
bar3(...,'style')	%三维条形图，取 'detached'/'grouped'/'stacked'， 默认为 'detached'
bar3h	%三维水平条形图

% 曲线图，基本二维图形函数
plot(Y)	%平面曲线图
plot(X1,Y1)
plot(X1,Y1,linespec)
plot(...,'propertyname',propertybalue,...)
plot3(X1,Y1,Z1)	%三维曲线图
plotyy	%双y轴坐标
% 符号函数(显函数、隐函数、参数方程)
ezplot(f)	% 默认区间为 -2*pi<x<2*pi 
ezplot(f,[a,b])
ezplot(f,[xmin,xmax,ymin,ymax])
ezplot(x,y,[tmin,tmax])
% 字符串fun指定的函数
fplot(fun,lims)	%fun(x): 关于独立变量x的字符串形式的符号函数，或是m文件的函数名；对向量中的每个x元素返回一个行向量
% 空间曲面
surf(X,Y,Z)
mesh(X,Y,Z)		%网格点形式的空间曲面
meshz(X,Y,Z)	%网格曲面周围画一个落幕(curtain)图
% 散点图
scatter(X,Y,S,C)	%二维散点图，默认为彩色圆圈标记。S为标记尺寸，是标量/X与Y的同维向量；C为标记颜色，是表示颜色的字符串/X与Y的同维向量/Length(X)×3的矩阵指定RGB值
% 等高值线图
contour(X,Y,Z,n)	%函数Z=f(X,Y)的n级二维等高值线图，n为等高线级数，省缺时取X轴的刻度分级数
[C,h] = contour(X,Y,Z,n)	%C为等高线矩阵，h为一个指向图形对象的句柄向量
clabel	%标注等高线
contour3(X,Y,Z,n)	%三维视图下绘制
[C,h] = contour(X,Y,Z,n)

% 面域图
area

% 射线图
compass

% 羽毛图
feather

% 双对数坐标图
loglog		%绘制对数坐标函数(x,y的坐标轴都是对数)
semilogx	%绘制x坐标是对数坐标
semilogy	%绘制y坐标是对数坐标

% 极坐标图
polar(theta,rho,linespec)

% 二维饼图
pie

% 阶梯图
stairs

% 二维杆图
stem
```

控制语句

```matlab
% 区间段
n = hist(Y)
n = hist(Y,X)
[n,xout] = hist(...)
% 辅助函数
title('...')
xlabel('...')
ylabel('...')
text(x,y,'...')	%将''中指定内容显示在(x,y)处
legend()	%图例
axis(x_min,x_max,y_min,y_max)	%x,y轴显示范围
grid		%图中显示虚线网格
hold on		%后面plot的图形和先前的叠加在一起
hold off	%解除hold on命令
```

控制流：

```matlab
% 循环控制
for; end	%非必要最好不要用for，防止内部嵌套；使用时也要预先分配数组(预先分配内存)
while; end
% 条件控制
if; else if; else; end; end	%几个if就有几个end
switch; case; otherwise; end	%不等于case时执行otherwise后面的语句
```

## 帮助

```matlab
% 函数搜索
help
% 词条搜索
lookfor	

```

help指令：函数搜索



# 作图

## 作图函数



## 作图参数

基本线型：

| 符号 | 线型  | 符号 | 线型   |
| ---- | ----- | ---- | ------ |
| .    | 点    | *    | 星号   |
| o    | 圆圈  | –    | 虚线   |
| x    | x标记 | :    | 点线   |
| +    | 加号  | -.   | 点画线 |

颜色：

| 符号 | 颜色 | 符号 | 颜色 |
| ---- | ---- | ---- | ---- |
| y    | 黄色 | g    | 绿色 |
| m    | 紫红 | b    | 蓝色 |
| c    | 青色 | w    | 白色 |
| r    | 红色 | k    | 黑色 |

## 画图控制命令

### 二维

```matlab
grid	% grid on(加格栅), grid off(删除格栅)
hold	% hold on(保持当前图形), hold off(释放), 后面不加';'
text	% 给定位置放置文本
hh = xlabel(string)	% x轴标注
hh = ylabel(string)	% y轴标注
hh = zlabel(string)	% z轴标注
hh = title(string)	% 加标题
hh = gtext(string)	% 鼠标放置标注
figure	% 创建图形
H = figure	% 创建图形并返回句柄
subplot	% 
H = subplot(m,n,t)	% 将整个作图区域划分为m*n块(以行排序)，激活第t块
zoom	% zoom on(左键放大2倍，右键缩小2倍)
axis([x1,x2,y1,y2])	% 设置坐标区范围
axis auto	% 将坐标轴返回到自动缺省值
axis square	% 将当前图形设置为方形
axis equal	% 坐标轴长度单位设置相等
axis normal	% 关闭 axis equal 和 axis square
axis off	% 关闭轴标记、格栅、单位标志
axis on	% 显示
```

### 条纹曲面图

```matlab
[X,Y]=meshgrid(x,y) % 产生一个以向量x为行，向量y为列的矩阵
```

# 计算

符号对象

```matlab
a = sym(s)	% 将数值对象s转化为符号对象
a = sum('s')	% 将字符串对象转化为符号对象
syms a b c x	% 创建多个符号变量，变量名之间用空格分开，不能用其他符号
findsym(f)	% 确定表达式f中所有自由符号变量
class(a)	% 判断对象a的类型
```

limit：

```matlab
limit(f,x,a)	% x趋向于a，默认a为0，变量x可不写
limit(...,'left')	% 同理，'right'是返回右极限
limit(...,inf)	% 返回正极限，-inf 为负极限
```

用来计算两个函数之间的等阶或等价

## 符号表达式运算

初等运算：

```matlab
% 符号表达式 -- 转换
subs(s,x,new)	% 用new替换符号表达式s中的符号x
eval(s)	% 将符号表达式转换为数值表达式
vap(s,n)	% 将符号表达式s转换为具有n位精度的数值，n缺省时按digits(n)函数设置为32
double(s,n)	% 将s转换为双精度数值

% 符号表达式 -- 化简
simple(s)	% 利用各种恒等式关系、函数关系对符号表达式s进行化简
pretty(s)	% 习惯方式显示表达式s
factor(s)	% 因式分解表达式s为因式乘积
expand(s)	% 展开表达式s中乘积为和式
collect(s,x)	% 将表达式s以x的幂次项整理
horner(s)	% 将表达式s中的符号多项式转化为嵌套式
[n,d]=numden(s)	% 提取分子n和分母d

% 复合函数运算
y=compose(f,g,t)	% 构造复合函数，返回复合函数f(g(t))

% 反函数运算
g=finverse(f,t)	% 获得反函数g(t)

x=solve(f,v)	% 解析代数f=0得到解析解，若做数值计算需要转变变量类型
[x1,x2]=fsolve(f1,f2,v1,v2)	% 解方程组，返回x1和x2
x=fsolve(f,x0)	% 数值搜索求解数值方程f=0，以x0为自变量初始值进行搜索
[x,f]=fsolve(f,x0)	% 返回方程的解和相应函数值
x=fzero(f,[a,b])	% 寻找一元函数的局部零点
[x,f]=fzero(f,x0,tol)	% 返回方程的解和相应函数值，x0是搜索起点，tol控制精度，省缺时为eps
```

求导：

```matlab
diff(f,v,n)	% 一元符号函数，对变量v求n阶导数，后两者可省缺
```

求极值：

```matlab
x=fminbnd(f,a,b,options)	
% options包含多个优化参数
% display：'off', 'iter', 'final'
% maxfunevals 函数评价最大允许次数
% maxiter 最大允许迭代次数
% tolx x处的终止容限
x=fminbnd(...,p1,p2)	% p1, p2为传递给目标函数的附加变量
[x,fval,exitflag,output]=fminbnd()	% fval是函数极值；exitflag为-1/0/1，表示迭代搜索的结果
% output. itrations 迭代次数
% output. algorithm 采用的算法
% output. funcount 函数评价次数
```

泰勒展开;

```matlab
taylor(f,n,x0)	% 在x0点展开n项，x0省缺为0

```

