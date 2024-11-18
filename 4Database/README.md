分享：
- Neo4j：NOSQL图形数据库，基于Java，擅长复杂关系类数据的存储
	- 环境配置：JDK配置、DeskTop版本
- Key-Value存储：
	- Redis：docker连接
	- 哈希表组织键值对，key太多使用链式重复（哈希冲突）、ReHash（哈希桶扩容，但会导致阻塞）、渐进式ReHash
	- 持久化：Hash表要在内存中，如何存到磁盘中，AOF+RDB混合
		- AOF：将成功执行的命令保存，AOF Rewrite
		- RDB(Redis DataBase)：将哈希表内容写到磁盘
- 跨NoSQL数据库分布式事务
- 文档存储数据库：MongoDB
- 列存储技术
- 传统数据库实战经验
- xml数据库

# class

[[0数据库简介]]
[[1关系数据库基本理论]]
[[2数据库设计]]
[[3分布式数据库]]
[[4面向对象数据库]]
[[5Key-Value模式]]
[[6云计算]]

# 考试

题目：
- 40分简答
- 60分综合：
	- 课堂上讲的
	- 作业题