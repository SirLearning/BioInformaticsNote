[[BioInformaticsNote/3Program/Database/README|README]]

MySQL 8 的新特性
- NoSQL
- 隐藏索引、降序索引
- JSON支持
- 安全和账户管理
- InnoDB
- 数据字典
- 原子数据定义语句
- 资源管理
- 字符集支持
- 优化器增强
- 通用表表达式
- 窗口函数
- 正则表达式
- 内部临时表
- 日志记录
- 备份锁
- 复制

移除的特性：
- 查询缓存
- 加密相关
- 空间函数相关
- \N 和 NULL
- mysql_install_db
- 通用分区处理程序
- 系统和状态变量信息
- mysql_plugin 工具

# 语言基础

MySQL language
- 默认字符集：utf8mb4
	- utf8mb4_0900_ai_ci
	- UTF-8 (8-bit Unicode Transformation Format) 通用转换格式：针对Unicode字符的一中变长字符编码
		- 英文：8 bit (1 byte)
		- 中文：24 bit (3 byte)
			- UTF-8编码中汉字字符占3字节，当遇到占4字节的UTF-8编码时，会导致存储异常。
- latin1
	- ISO 8859-1latin 1
	- 把位于128-255的字符用于拉丁字母表中特殊语言字符的编码
- GB2312：简体中文字符集
	- gb2312_chinese_ci
- GBK：对GB2312的扩展
	- gbk_chinese_ci
	- 2 byte：中英文都是
		- 中文最高位是1
	- 国家编码，通用性比UTF-8差
- latin1, GB2312, GBK 需要通过 Unicode 编码才能转换为 UTF-8

MySQL 字符集转换
- 如果设置表的MySQL默认字符集时 utf8mb4，且通过 UTF-8 编码发送查询，但存入数据库的数据仍然是乱码
	- 问题出在 connection 层上
- 字符集层次
	1. 服务器级：character_set_server, collation_server
	2. 客户端：character_set_client
		- 解释客户端发到服务器的SQL命令文字
	3. 连接级：character_set_connection, collation_connection
		- 处理SQL命令
	4. 结果级：character_set_result
	5. 数据库：character_set_system, collation_database，可以在 create table 时设定
		- 表的字符集
			- 字段的字符集

MySQL 语句：
- .sql 脚本文件
- 标识符：命名一些对象，通用明明规则为以字母或下划线开头
	- Linux 对大小写敏感
- 关键字

## 常用函数

数学函数

字符串函数

时间和日期函数

聚合函数：分组统计函数

其他函数：
- 系统信息函数
- 加密函数
- 格式化函数
- 窗口函数

# 基本操作

数据库管理：
- 数据库文件：InnoDB 将数据库表文件合并到 .ibd 文件中
- MySQL 自动建立的数据库
	- mysql：用户访问权限
	- information_schema：服务器所维护的所有其他数据库信息
	- performance_schema：收集数据库的服务器性能参数
	- sakila：官方测试用的数据库
	- sys：一系列存储过程、自定义函数以及视图，系统元数据信息
	- world：主要城市、国家和语言信息

存储引擎
- InnoDB
- MyISAM
- MEMORY

数据库设计过程：
1. 需求分析
	- 数据：
		- 数据名
		- 属性及其类型
		- 主关键字属性
	- 数据的特征：
		- 保密要求
		- 完整性约束条件
	- 数据量估计
	- 使用频率
	- 更改要求
2. 概念设计
	- E-R图
		- 每个实体或联系将映射为一个数据表
3. 逻辑设计
	- 特定 DBMS 下的应用视图
	- 结果时 DBMS 提供的数据定义语言 (DDL) 写成的数据模式
4. 物理设计
	- 设计数据的：存储形式、存取路径
	- 文件结构
	- 索引设计
	- 数据库的：内模式/存储模式
		- 影响数据库性能

数据库设计规范化
- 规范化规则
	- 应用程序在数据库中实现强制完整性
	- 很少包括执行设计4个以上表的查询
	- 设计一个好的基本关系
		- 每个基本关系独立表示一个实体
		- 尽量减少数据冗余
	- 范式 (Normal Form, NF)：满足一定条件的关系模式

数据库
- 创建：
- 管理：打开、修改、显示、删除

数据库表管理：对表结构 (Structure) 的操作
- InnoDB 表空间：
	- 共享表空间
	- 独立表空间
- 创建表
	- 临时表 `temporary`
	- 判断 `if not exists`
	- 字段定义
		- 是否可以是空值 `null | not null`
		- 默认值 `default default_value`
		- 自增值属性 `auto_increment`：必须被索引
		- 唯一性约束 `unique [key]`
		- 主键约束 `[primary] key`
		- 注释字符串 `comment 'string'`
		- 外键约束 `reference_definition`
	- 为相关字段指定索引 `index_definition`
	- 表的选项 `table_option`：存储引擎、字符集等
	- 表的查询语句 `select_statement`
- 查看表
	- `show tables`
	- 查看表的基本结构 `describe`
	- 查看表详细结构 `show create table`
- 修改表
	- 字段：添加、修改默认值、重命名、修改数据类型、删除
	- 表：重命名
	- 行：按字段排序
	- 字符集：修改默认、转换为二进制
- 删除表 `drop`
- 管理临时表
	- 临时表在连接MySQL期间存在，断开连接时自动删除

表数据操作：对数据记录 (Record) 的操作
- 表记录的插入
	- `insert into | replace into`
	- `load data infile 'filename.txt' into table tablename`
	- `set` 子句
	- 图片数据插入：`blob` 类型存储二进制文件
- 表记录的修改：`update table_name set ...`
- 表记录的删除：`delete`
	- `low_priority`降低 `delete` 操作的优先级
	- `quick` 修饰符：加快部分种类的删除操作的速度
	- `ignore`：忽略删除过程中的所有错误
	- `order by` 子句：各行按照子句中指定的顺序删除，只在与 `limit` 联合使用时起作用
	- `limit` 子句：被删除的行的最大值

表的数据完整性
- 非空约束`null | not null`
- 主键约束
	- 创建表时
	- 修改表的主键 `alter`
- 外键约束
	- 参照完整性约束：子表修改外键数据时，一定是存在与父表中的主键
	- 外键声明
	- 参照完整性定义：`delete` `update`
		- `restrict`
		- `cascade`
		- `no action`：和 `restric` 一样
	- 对已有的表添加外键
	- 创建表时创建外键
- 检查约束 `check`
- 唯一性约束 `unique`
	- 可以有多个
	- 使用 `null | not null` 声明时，可以取null
	- 和创建 `primary key` 时产生 `primary key` 约束一样，会自动产生 `unique` 索引

# 数据检索

基本查询语句

