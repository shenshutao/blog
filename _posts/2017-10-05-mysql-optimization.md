---
layout: post
title: "Mysql 性能优化"
date:   2017-10-05 10:06:46 +0800
categories: mysql
---
# 概述
数据库的性能基于数据库层的几个因素，比如表，查询和配置。当然这些软件上的操作最终会落实到硬件层的CPU和IO操作。所以Mysql的数据库优化包括以下方面：
- 数据库层优化
- 硬件层优化
- 平衡便携性和性能


# 1.数据库层优化
- 表设计优化,列使用正确的类型
    + 更新操作较多，使用多表格少列的策略；查询操作较多，使用少表格多列策略。
    + 给列设置正确的类型
        + “性别”，“状态“，”国家“，你可以使用ENUM，而不是 VARCHAR。
        + 使用更小的列，搜索会更快。[Data Type Storage Requirements](https://dev.mysql.com/doc/refman/5.7/en/storage-requirements.html)
        + 固定长度的表会提高性能，因为这些固定的长度是很容易计算下一个数据的偏移量，所以读取的自然也会很快。
        + 使用PROCEDURE ANALYZE寻求建议，仅供参考，并不是非常准确，不过在5.7中添加了废弃警告，将在8.0被废除，可以期待其替代品出现。
- 索引的优化
    + 为经常使用的搜索字段建索引，可以搭配EXPLAIN来寻找你的搜索字段。
    + 在Join表的时候使用相当类型的例，并将其索引。
- 正确选择存储引擎 InnoDB / MyISAM
    + 总的来说InnoDB支持事务，MyISAM不支持，但对于查询有更好的效率。[MyISAM与InnoDB区别](http://www.jianshu.com/p/a957b18ba40d)
- 数据存储格式 （压缩）优化
    + 使用MyISAM的时候可以考虑这个问题。
- MySQL的锁策略优化
    [MySQL锁定机制简介](http://blog.csdn.net/zq602316498/article/details/49428825)
- 缓存配置优化
    缓存可以极大的提高查询效率
    + 缓存配置优化，主要是query_cache_size，query_cache_type，binlog_cache_size [](http://isky000.com/database/mysql-perfornamce-tuning-cache-parameter)
    + 优化查询语句，有些函数比如CURDATE()，NOW() 和 RAND()等会让查询缓存不起作用。


# 2.硬件层优化
- 磁盘搜索/寻道速度
- 磁盘读写速度
- CPU周期
- 内存带宽

# 3.可移植性和性能间的平衡
在一些可移植的SQL语句中，可以把一些提高性能的msyql的extensions以特别的形式放在注释里面，专门针对mysql进行一些优化。
```
/*! MySQL-specific code */
```