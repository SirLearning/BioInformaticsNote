虽然在AI时代，很多经验性学习的价值都不高了，但是最为基本的内容还是要熟练掌握的。

# ASCII 码

ASCII 码（美国信息交换标准代码）：是标准的字符集，有128个字符
- 许多网站都可以查看：
	- [ASCII 表 | 菜鸟工具](https://www.jyshare.com/front-end/6318/)
	- [HTML ASCII 参考手册 | 菜鸟教程](https://www.runoob.com/tags/html-ascii.html)
- 与 UTF 的区别：
	- 首先要了解 Unicode：Unicode 包括了世界上所有字符的编码，可以容纳100多万个符号
		- 可以查询[Unicode – The World Standard for Text and Emoji](https://home.unicode.org/)来找到具体的符号对应表
		- 只是一个符号集，不规定符号的二进制代码如何存储
	- UTF-8：是 Unicode 的一种实现方式，其他还有 UTF-16、UTF-32 等![[Pasted image 20250517171140.png]]
- 对的文件进行编码的方式：
	- ANSI：对英文文件是 ASCII 编码，对简体中文文件是 GB2312 编码，繁体中文会采用 Big5 码
	- Unicode 编码：即 UCS-2 编码，直接用两个字节存入字符
	- UTF-8 编码
- 一般读取时，转换为 Unicode 编码，保存时转换为 UTF-8 编码
- 服务器一般将 Unicode 转换为 UTF-8 再传输给浏览器

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
		-  为什么使用conda：create an environment within your computer and install software that can only be run from within one environment
			- This is particularly useful when running different versions of software and to avoid incompatibility issues

```
solver: libmamba
channels:
  - https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free
  - defaults
restore_free_channel: true
auto_activate_base: false
```

conda problem:
1. mamba can not work
	1. figure out in the file: failed
2. uninstall conda and memba
