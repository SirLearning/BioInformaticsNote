# Conda
## mamba

mamba 与conda 创建一个独立的python环境步骤一样，首先需要创建一个环境，然后激活环境。

mamba 创建环境： `mamba create -n XXX python=3.9`

XXX为创建环境的名称，python= 这里我选择用python3.9.

激活环境： `conda activate XXX`

退出环境：`conda deactivate xxx`

安装包：`mamba install xxx`

移除包：`mamba/conda remove -n xxx` XXX 第一个为环境名称，第二个为包名称

更新包：`mamba update XXX`

更新python：`mamba update python`

移除环境： `conda/mamba remove -n XXX --all`

导出环境： `conda env export xxx.yaml` 将现有的包导出，方便以后直接创建环境

# 正则表达式
regular expression (regex, regexp, or RE)
```
Import re # 导入正则表达式模块

re.search() # 用于搜索正则表达式模式第一次出现在字符串中的位置
re.search(r"\bfred\b",name) 
	# \bfred\b表示只有fred前后都是单词边界时才匹配成功，字母,数字,下横线都不是单词边界,只有fishC两边都是单词边界时 fred才会被匹配。
	# “.”作为通配符可以表示除换行符外的所有字符，\转义符，\d可以表示匹配任何数字（0-9）
	# 用正则表达式前加“r”表示元字符
```
## 修饰符
```
re.l 
re.L
re.M
re.S
re.U
re.X
```
## 转义字符
```
\'	单引号
\"	双引号
\a	发出系统响铃声
\b	退格符
\n	换行符
\t	横向制表符（TAB）
\v	纵向制表符
\r	回车符
\f	换页符
\o	八进制数代表的字符
\x	十六进制数代表的字符
\0	表示一个空字符
\\	反斜杠
```
## 元字符
```
.  除换行以外的其他任意字符
\序号
\A
\Z
\b  单词边界
\B
\d   数字 0-9
\D  除了数字之外的任意字符
\s  空白字符
\S   除空白字符以外的任意字符
\w  字母、数字、下划线
\W  除了字母、数字、下划线以外的任意字符
…… 等等等等
^  字符串的开始
$ 字符串结束
(?=…)  环视(零宽断言) 后面的字符串符合表达式…的时候的位置
(?!) 
*    0到无数次
+   1到无数次
?  0 或者1 次
[0-9] 数字0到数组9之间的任意一个
[a-z]  字母a到字母z的任意一个
[^cfC]  除了字母  c   f    C的任意一个字符
[\u4e00-\u9fa5] 汉字中的任意一个汉字 注
[^a-z] 除了字母 a 到字母z的任意一个字符
[^-a-c] 除了 -  字符以及字母a到字母z的任意一个字符
|   多选分支，或者关系
\1 \2 … 反向引用 < (\w) >.*</\1> 引用第一个捕获组的结果，用于匹配html的闭合标签
{n}  重复N次
{n,} 重复至少N次
 {n,m}   n到m次
[]  字符组，字符范围
()  捕获组（子表达式）
```
## 字符串
```
count(sub[,start[,end]])
encode(encoding='utf-8',errors='strict')
endswith(sub[,start[,end]])
expandtabs([tabsize=8])
find(sub[,start[,end]])
index(sub[,start[,end]])
isalnum()
isalpha()
isdecimal()
isdecimal()
isdigit()
isnumeric()
isspace()
istitle()
isupper()
join(sub)
ljust(width)
lower()
lstrip()
partition(sub)
replace(old,new[,count])
rfind(sub[,start[,end]])
rindex(sub[,start[,end]])
rjust(width)
rpartition(sub)
rstrip()
split(sep=None, maxsplit=-1)
splitlines(([keepends]))
startswith(prefix[,start[,end]])
strip([chars])
swapcase()
```
## 格式化操作符
```
%c	格式化字符及其 ASCII 码
%s	格式化字符串
%d	格式化整数
%o	格式化无符号八进制数
%x	格式化无符号十六进制数
%X	格式化无符号十六进制数（大写）
%f	格式化浮点数字，可指定小数点后的精度
%e	用科学计数法格式化浮点数
%E	作用同 %e，用科学计数法格式化浮点数
%g	根据值的大小决定使用 %f 或 %e
%G	作用同 %g，根据值的大小决定使用 %f 或者 %E
m.n	# m 是显示的最小总宽度，n 是小数点后的位数
-	# 用于左对齐
+	# 在正数前面显示加号（+）
#	# 在八进制数前面显示 '0o'，在十六进制数前面显示 '0x' 或 '0X'
0	# 显示的数字前面填充 '0' 取代空格
```
## 文件操作
```
## open
'r'	以只读方式打开文件（默认）
'w'	以写入的方式打开文件，会覆盖已存在的文件
'x'	如果文件已经存在，使用此模式打开将引发异常
'a'	以写入模式打开，如果文件存在，则在末尾追加写入
'b'	以二进制模式打开文件
't'	以文本模式打开（默认）
'+'	可读写模式（可添加到其他模式中使用）
'U'	通用换行符支持
## object
f.close()	关闭文件
f.read([size=-1])	从文件读取size个字符，当未给定size或给定负值的时候，读取剩余的所有字符，然后作为字符串返回
f.readline([size=-1])	从文件中读取并返回一行（包括行结束符），如果有size有定义则返回size个字符
f.write(str)	将字符串str写入文件
f.writelines(seq)	向文件写入字符串序列seq，seq应该是一个返回字符串的可迭代对象
f.seek(offset, from)	在文件中移动文件指针，从from（0代表文件起始位置，1代表当前位置，2代表文件末尾）偏移offset个字节
f.tell()	返回当前在文件中的位置
f.truncate([size=file.tell()]) 截取文件到size个字节，默认是截取到文件指针当前位置
## othersnext()用法：
next(iterator[, default])
	iterator – 可迭代对象
	default – 可选，用于设置在没有下一个元素时返回该默认值，如果不设置，又没有下一个元素则会触发 StopIteration 异常
```

# 数据分析

## 数据文件

xml (Extensible Markup Language) 可拓展标记语言：和json用途相似
- 特点：简单，易于在任何应用功能程序中读/写
- 用途：
	- 数据处理：说明、储存、传输
	- 作为软件、框架的配置文件：如Android Studio
		- 配置所开发的项目 (configure your project)
		- 生成AndroidManifest.xml文件：记录项目名、包名、默认配置好的项目属性、activity属性、后续组件的配置
- 编码工具：Dom4j, JDom
- 相比于json流行度更广，描述性更强

json (JavaScript Object Notation) JavaScript对象表示法：一种轻量级的数据交换格式
- 来源：ECMAScript（一种js规范）的一个子集
- 特点：
	- 数据体积小、传输速度快
	- 理想的数据交换语言：完全独立于任何编程语言的文本格式来存储和表示数据
		- 数据交互：与JavaScript的交互更加方便，更容易创建JavaScript对象
	- 扩展性强：没有什么是xml能扩展，json不能的
	- 解码难度低，几乎为0
- 编码工具：json.org，不借助工具也可以
- 数据：两者可相互包含
	- 数组 `[{}, {}]`：String[], ...
	- 对象 `{a:, b:}`：str, method, ...
- 与JavaScript之间的转换
	- data -> Object
		- eval()函数：解析json文本数据，将其转成一个JavaScript对象
	- Object -> data
		- Struts2组件：将JavaBean对象、集合转成json
		- SpringMVC：将JavaBean转成json
	- 开发包：

js (JavaScript)：在网页上执行的代码，脚本文件
- html文档中：使用`\`嵌入，`<\script>`标签，可包含在多个html文档中实现代码重用
- *Ajax*：使用JavaScript作为主干来创建Web应用程序
	- 该程序特点：
		- 在后台加载数据
		- 避免整个页面重新加载
	- 导致：JQuery、Prototype、Dojo等库的创建
- js文件可包含的内容：变量、运算符、函数 (function)、条件、循环、数组、对象

## dataframe

pandas中loc和iloc的区别

# matplotlib

