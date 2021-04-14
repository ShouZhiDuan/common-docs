# MySQL基础模块

## 1、预览图

![image-20210407134900293](C:\Users\dev\AppData\Roaming\Typora\typora-user-images\image-20210407134900293.png)

## 2、MySQL长连接时长查看

```properties
show global variables like 'wait_timeout'; -- 非交互式超时时间，如 JDBC 程序 
show global variables like 'interactive_timeout'; -- 交互式超时时间，如数据库工具
```

- 默认都是 28800 秒，8 小时

## 3、怎么查看 MySQL 当前有多少个连接？

- show global status like 'Thread%';

```properties
Threads_cached：缓存中的线程连接数。 
Threads_connected：当前打开的连接数。
Threads_created：为处理连接创建的线程数。 
Threads_running：非睡眠状态的连接数，通常指并发连接数。 
每产生一个连接或者一个会话，在服务端就会创建一个线程来处理。反过来，如果要 
杀死会话，就是 Kill 线程。
```

## 4、查看连接操作详情列表

- SHOW PROCESSLIST
  - ![image-20210406114530353](C:\Users\dev\AppData\Roaming\Typora\typora-user-images\image-20210406114530353.png)

- 常见的执行Command解释分析
  - https://dev.mysql.com/doc/refman/5.7/en/thread-commands.html
  - ![image-20210406114444877](C:\Users\dev\AppData\Roaming\Typora\typora-user-images\image-20210406114444877.png)

## 5、MySQL 服务允许的最大连接数是多少呢？       

- show variables like 'max_connections';
  - 在 5.7 版本中默认是 151 个，最大可以设置成 16384（2^14）。

## 6、SHOW参数说明

1、级别：会话 session 级别（默认）；全局 global 级别 

2、动态修改：set，重启后失效；永久生效，修改配置文件/etc/my.cnf 

set global max_connections = 1000;

## 7、MySQL 支持哪些通信协议呢？

- 第一种是 Unix Socket。
  - mysql.sock文件可以在my.cnf文件中找到配置的位置。或者select @@socket查询改文件的目录。
  - mysql -S /home/mysql/3306/mysql.sock -uroot -p（执行命令）

- 第二种方式，TCP/IP 协议。
  - mysql -h192.168.8.211 -uroot -p123456 （执行命令）

## 8、MySQL连接情况查看

- netstat -an | grep 6379
  - ![image-20210406180540065](C:\Users\dev\AppData\Roaming\Typora\typora-user-images\image-20210406180540065.png)

## 9、MySQL服务端常见参数设置列表

- SHOW VARIABLES;
  - ![image-20210406185158800](C:\Users\dev\AppData\Roaming\Typora\typora-user-images\image-20210406185158800.png)
- show variables like ‘max_allowed_packet’;查询具体的某个参数的值

## 10、MySQL缓存

- show variables like 'query_cache%';查看mysql是否开启缓存（MySQL 的缓存默认是关闭的）。
- MySQL8中缓存已被移除。

## 11、MySQL最后查询开销

- show status like 'Last_query_cost';

## 12、MySQL优化器

- SHOW VARIABLES LIKE 'optimizer_trace';
- set optimizer_trace="enabled=on";开启优化跟踪器，占用性能生产关闭。

## 13、MySQL查看数据库引擎

- show table status from `dsz-data-base`; 
  - `dsz-data-base`数据库名称
  - ![image-20210406200414124](C:\Users\dev\AppData\Roaming\Typora\typora-user-images\image-20210406200414124.png)

- show engines ;

  - 查询数据库所有的引擎列表。

    ![image-20210407093042631](C:\Users\dev\AppData\Roaming\Typora\typora-user-images\image-20210407093042631.png)

## 14、MySQL持久数据目录

- show variables like 'datadir';

  ![image-20210406200650948](C:\Users\dev\AppData\Roaming\Typora\typora-user-images\image-20210406200650948.png)

## 15、MySQL存储引擎InnoDB

- 读取的最小逻辑单远索引页、数据页。

- InnoDB 内存结构和磁盘结构

  - ![image-20210407095118618](C:\Users\dev\AppData\Roaming\Typora\typora-user-images\image-20210407095118618.png)

- 内存结构

  - **Buffer Pool** 缓存的是页面信息，包括数据页、索引页。SHOW STATUS LIKE '%innodb_buffer_pool%';

    Buffer Pool 默认大小是 128M（134217728 字节），可以调整。

  - **Change Buffer**

    - 如果这个数据页不是唯一索引，不存在数据重复的情况，也就不需要从磁盘加载索 

    引页判断数据是不是重复（唯一性检查）。这种情况下可以先把修改记录在内存的缓冲 

    池中，从而提升更新语句（Insert、Delete、Update）的执行速度。

    - 最后把 Change Buffer 记录到数据页的操作叫做 merge。什么时候发生 merge？ 

    有几种情况：在访问这个数据页的时候，或者通过后台线程、或者数据库 shut down、 

    redo log 写满时触发。

    - 如果数据库大部分索引都是非唯一索引，并且业务是写多读少，不会在写数据后立 

      刻读取，就可以使用 Change Buffer（写缓冲）。写多读少的业务，调大这个值：

      SHOW VARIABLES LIKE 'innodb_change_buffer_max_size';

      代表 Change Buffer 占 Buffer Pool 的比例，默认 25%。

  - **Log Buffer**[https://blog.csdn.net/suifeng629/article/details/102560575]

    - 如果 Buffer Pool 里面的脏页还没有刷入磁盘时，数据库宕机或者重 

      启，这些数据丢失。如果写操作写到一半，甚至可能会破坏数据文件导致数据库不可用。 

      为了避免这个问题，InnoDB 把所有对页面的修改操作专门写入一个日志文件，并且 

      在数据库启动时从这个文件进行恢复操作（实现 crash-safe）——用它来实现事务的持 

      久性。

    - 这 种 日 志 和 磁 盘 配 合 的 整 个 过 程 ， 其 实 就 是 MySQL 里 的 WAL 技 术 

      （Write-Ahead Logging），它的关键点就是先写日志，再写磁盘。

      **show variables like 'innodb_log%';**

      ![image-20210407101740570](C:\Users\dev\AppData\Roaming\Typora\typora-user-images\image-20210407101740570.png)

    - 当然 redo log 也不是每一次都直接写入磁盘，在 Buffer Pool 里面有一块内存区域 

      （Log Buffer）专门用来保存即将要写入日志文件的数据，默认 16M，它一样可以节省 

      磁盘 IO。**SHOW VARIABLES LIKE 'innodb_log_buffer_size';**

      log buffer 写入磁盘的时机，由一个参数控制，默认是 1。

      SHOW VARIABLES LIKE 'innodb_flush_log_at_trx_commit';

      https://dev.mysql.com/doc/refman/5.7/en/innodb-parameters.html#sysvar_innodb_flush_log_at_trx_commit

## 16、基础模块总结

- MySQL常见的日志

  - Redo Log(容灾备份) [https://blog.csdn.net/suifeng629/article/details/102560575]

  - Undo Log(事务回滚)

  - Bing Log(主从复制)

    

# MySQL索引模块

## 1、查看行格式

SHOW TABLE STATUS LIKE 'dsz_test';

## 2、索引结构演变

- 2分查找：只适合有序数组，更新性能能慢。
- 2叉树：树的深度太深，IO过多，极端情况下会斜树（等价于一条链表）。
- 平衡2叉树（AVL）：不会极端出现斜树，因为会产生自旋。但是输的深度，影响IO，存储效率也不高。树的左右两边高度差不能查过1，这也是自旋出发的机制。
- 多路平衡2叉树（B-Tree）：路数是磁块上节点的数量+1，大大减少了数的深度，提高IO性能。
- 多路平衡2叉树（B+Tree）：路数跟磁块上的节点数量相同，路数更多。磁块存储效率更高，而且叶子节点天然有序，便于排序范围查找。

## 3、索引类型

- 普通索引
- 唯一索引（主键索引是特殊的唯一索引不能为空）
- 全文索引：提升lke的性能

## 4、如果一张表没有主键怎么办？

- 1、如果我们定义了主键(PRIMARYKEY)，那么InnoDB会选择主键作为聚集索引。

- 2、如果没有显式定义主键，则InnoDB会选择第一个不包含有NULL值的唯一索引作为主键索引。
- 3、如果也没有这样的唯一索引，则InnoDB会选择内置6字节长的ROWID作为隐藏的聚集索引，它会随着行记录的写入而主键递增。
  - select _rowid name from t2查询行ID。

## 5、索引使用的原则

- 列的离散度

  > 列的重复值越多，离散度就越低，重复值越少，离散度就越高。

- 联合索引最左匹配原则

  > 最左的匹配的原则意思是如果创建了一个联合索引name,phone。在索引的匹配原则会先比较name然后在比较phone。如果where phone=137则不会走索引，带头的前面不能缺失，否则索引失效。

- 覆盖索引

  - 回表：非主键索引，我们先通过索引找到主键索引的键值，再通过主键值查出索引里面没

    有的数据，它比基于主键索引的查询多扫描了一棵索引树，这个过程就叫回表。

  - 如果查询需要返回的字段正好是where条件后的索引字段，这样就可以避免回表操作。直接由辅助索引就可以查询我们需要得到的数据。

- 索引条件下推

  - seto ptimizer_switch='index_condition_pushdown=on';开启索引下推。	

  - 索引的比较是在存储引擎进行的，数据记录的比较，是在Server层进行的。

  - 查看所有下推是否开启。show variables like 'optimizer_switch';

  - 索引条件下推（IndexConditionPushdown），5.6以后完善的功能。只适用于二

    级索引。ICP的目标是减少访问表的完整行的读数量从而减少I/O操作。

![image-20210407173509695](C:\Users\dev\AppData\Roaming\Typora\typora-user-images\image-20210407173509695.png)

## 6、索引的创建

- 1、在用于where判断order排序和join的（on）字段上创建索引。
- 2、索引的个数不要过多，影响更新操作性能。
- 3、区分度低的字段，例如性别，不要建索引。离散度太低，导致扫描行数过多。
- 4、频繁更新的值，不要作为主键或者索引。有可能会出现页分裂。
- 5、组合索引把散列性高（区分度高）的值放在前面。
- 6、尽量不用一些无序的比如UUID或者身份证作为索引。

## 7、什么情况会出现所有失效

- 1、索引列上使用函数（replace\SUBSTR\CONCAT\sumcountavg）、表达式、计算（+-*/）。

  > explain SELECT * FROM `t2` where id+1=4;

- 2、字符串不加引号，出现隐式转换。

  > explainSELECT*FROM`user_innodb`wherename=136;
  >
  > explainSELECT*FROM`user_innodb`wherename='136';

- 3、LIKE条件中前面带%

  > where条件中likeabc%，like%2673%，like%888都用不到索引吗？为什么？
  >
  > 过滤的开销太大，所以无法使用索引。这个时候可以用全文索引。

- 4、NOTLIKE不能

  > explain select * from employees where last_name not like 'wang';

- !=（<>）和NOTIN在某些情况下可以

  > explain select * from employees where emp_no not in (1)
  >
  > explain select * from employees where emp_no <> 1

## 8、前缀索引

- 概念：当字段值比较长的时候，建立索引会消耗很多的空间，搜索起来也会很慢。我们可以通过截取字段的前面一部分内容建立索引，这个就叫前缀索引。

- 怎么计算不同的长度的选择性呢？

  > select count(distinct address) / count(*) from shop; 重复比例计算
  >
  > 试探做法：
  >
  > select 
  >
  > count(distinct left(address,10))/count(*) as sub10, 
  >
  > count(distinct left(address,11))/count(*) as sub11, 
  >
  > count(distinct left(address,12))/count(*) as sub12, 
  >
  > count(distinct left(address,13))/count(*) as sub13 
  >
  > from shop;

## 9、索引模块总结

- 注意：一个SQL语句是否使用索引，跟数据库版本、数据量、数据选择度都有关系。其实，用不用索引，最终都是优化器说了算。
- 优化器：基于cost开销（CostBaseOptimizer），它不是基于规则（Rule-BasedOptimizer），也不是基于语义。怎么样开销小就怎么来。



# MySQL事务模块

## 1、事务的ACID

- 原子性：要不都成功，要不都失败。一个事务时不可被分割的。
- 一致性：数据库最终的结果，跟客户端逻辑操作结果一直。
- 持久性：事务一但提交，数据库相关的记录是物理存在的，除非人为删除。
- 隔离性：不同的事务之间是互相不干扰的，独立的。

##  2、数据库什么时候会出现事务

## 默认事务开启以及自动提交

```sql
执行已下语句会默认开启和提交
UPDATE dsz_test SET tes = '测试事务是否自动开启以及提交' WHERE id = 2016;
```

### 查询数据库版本信息

```tex
select version(); 
```

### 查询数据库引擎

```tex
show variables like '%engine%'; 
```

### 查询数据库是否开启事务自动提交

```tex
show variables like 'autocommit';
```

### 事务开启的两种方式

```tex
一种是用 begin；
一种是用 start transaction。
```

### 事务中断的两种方式

```tex
第一种：提交一个事务，在commit之前rollback，回滚的时候，事务也会结束。
第二种：客户端的连接断开的时候，事务也会结束。
```

## 3、事务并发会带来什么问题

### 事务面临的问题

- 脏读：A事务读到了B事务未提交的数据，导致了前后两次数据不一致。

- 不可重复读：A事务读到了B事务提交的数据，导致了前后两次数据不一致。

- 幻读：A事务执行了一个范围查询，此时B事务提交了一个插入操作，导致了A事务再次范围查询的时候结果记录不一致。

  ![image-20210408102621698](C:\Users\dev\AppData\Roaming\Typora\typora-user-images\image-20210408102621698.png)

### 不可重复读和幻读，的区别在那里呢？

> 不可重复读是修改或者删除，幻读是插入。

### 小结

> 我们刚才讲了事务并发带来的三大问题，现在来给大家总结一下。无论是脏 
>
> 读，还是不可重复读，还是幻读，它们都是数据库的读一致性的问题，都是在一个事务 
>
> 里面前后两次读取出现了不一致的情况。 
>
> 读一致性的问题，必须要由数据库提供一定的事务隔离机制来解决。就像我们去饭 
>
> 店吃饭，基本的设施和卫生保证都是饭店提供的。那么我们使用数据库，隔离性的问题 
>
> 也必须由数据库帮助我们来解决。



## 4、事务的隔离级别

### [参考文档](http://www.contrib.andrew.cmu.edu/~shadow/sql/sql1992.txt)

### 隔离级别

- **Read Uncommitted（未提交读）**

  > 一个事务可以读取到其他事务未提交的数据，会出现脏读，所以叫做 RU，它没有解决任何的问题。 

- **Read Committed（已提交读）**

  > 是一个事务只能读取到其他事务已提交的数据，不能读取到其他事务未提交的数据，它解决了脏读的问题， 但是会出现不可重复读的问题。

- **Repeatable Read (可重复读)**

  > 它解决了不可重复读的问题,也就是在同一个事务里面多次读取同样的数据结果是一样的，但是在这个级别下，没有定义解决幻读的问题。 

- **Serializable（串行化）**

  > 在这个隔离级别里面，所有的事务都是串行执行的，也就是对数据的操作需要排队，已经不存在事务的并发操作了，所以它解决了所有的问题。

## 5、MySQL InnoDB 对隔离级别的支持

### 不同隔离级别效果图

![image-20210408104758611](C:\Users\dev\AppData\Roaming\Typora\typora-user-images\image-20210408104758611.png)

> InnoDB 支持的四个隔离级别和 SQL92 定义的基本一致，隔离级别越高，事务的并发度就越低。唯一的区就在于，InnoDB 在 RR 的级别就解决了幻读的问题。这个也是 InnoDB 默认使用 RR 作为事务隔离级别的原因，既保证了数据的一致性，又支持较高的并发度。 

### 如何解决读一致性问题

- **1、LBCC串行化 **(Lock Based Concurrency Control) 

  > 我既然要保证前后两次读取数据一致，那么我读取数据的时候，锁定我要操作的数据，不允许其他的事务修改就行了。这种方案我们叫做基于锁的并发控制 Lock Based Concurrency Control（LBCC）。 
  >
  > 如果仅仅是基于锁来实现事务隔离，一个事务读取的时候不允许其他时候修改，那就意味着不支持并发的读写操作，而我们的大多数应用都是读多写少的，这样会极大地影响操作数据的效率。

- **2、MVCC**(Multi Version Concurrency Control)

  - 数据库行影藏的三个字段

    - **DB_ROW_ID** 行ID   6字节

    - **DB_TX_ID** 创建版本号   6字节

    - **DB_ROW_PTR** 删除版本号   7字节

      其实DB_TX_ID 和DB_ROW_PTR 是同一个全局的事务ID只是逻辑上做了两个字段区分。

  > ![image-20210408111819764](C:\Users\dev\AppData\Roaming\Typora\typora-user-images\image-20210408111819764.png)

​       [图片地址](https://www.processon.com/view/link/5d29999ee4b07917e2e09298)

- **3、MVCC小结**

  ![image-20210408113208826](C:\Users\dev\AppData\Roaming\Typora\typora-user-images\image-20210408113208826.png)

  由上图可知：创建版本较小&&(删除版本较大或者无删除版本号)。





## 6、锁的类型（InnoDB）

- **行锁 两种**

  - 共享锁(需要手动加锁)：select * from tset where id = 1 lock in share mode;不同事物之间该锁是可以同时获得的。

    ![image-20210408145000578](C:\Users\dev\AppData\Roaming\Typora\typora-user-images\image-20210408145000578.png)

  - 排他锁(两种加锁方式)：

    - 增删改：会默认加上排他锁。

    - 手动加锁：FOR UPDATE。

      ![image-20210408145030404](C:\Users\dev\AppData\Roaming\Typora\typora-user-images\image-20210408145030404.png)

- **表锁 两种**

  - 意向共享锁
  - 意向排他锁

  ![image-20210408150138339](C:\Users\dev\AppData\Roaming\Typora\typora-user-images\image-20210408150138339.png)

## 7、锁的原理（InnoDB）

> 1、为什么表里面没有索引的时候，锁住一行数据会导致锁表？ 或者说，如果锁住的是索引，一张表没有索引怎么办？ 所以，一张表有没有可能没有索引？ 
>
> 1）如果我们定义了主键(PRIMARY KEY)，那么 InnoDB 会选择主键作为聚集索引。 
>
> 2）如果没有显式定义主键，则 InnoDB 会选择第一个不包含有 NULL 值的唯一索引作为主键索引。 
>
> 3）如果也没有这样的唯一索引，则 InnoDB 会选择内置 6 字节长的ROWID 作为隐藏的聚集索引，它会随着行记录的写入而主键递增。 所以，为什么锁表，是因为查询没有使用索引，会进行全表扫描，然后把每一个隐 藏的聚集索引都锁住了。 
>
> 2、为什么通过唯一索引给数据行加锁，主键索引也会被锁住？ 
>
> 大家还记得在 InnoDB 里面，当我们使用辅助索引的时候，它是怎么检索数据的吗？ 
>
> 辅助索引的叶子节点存储的是什么内容？ 
>
> 在辅助索引里面，索引存储的是二级索引和主键的值。比如name=4，存储的是name 
>
> 的索引和主键 id 的值 4。 
>
> 而主键索引里面除了索引之外，还存储了完整的数据。所以我们通过辅助索引锁定 
>
> 一行数据的时候，它跟我们检索数据的步骤是一样的，会通过主键值找到主键索引，然后也锁定。



## 8、锁的算法（InnoDB）

![image-20210408170721443](C:\Users\dev\AppData\Roaming\Typora\typora-user-images\image-20210408170721443.png)



- **记录锁**

  - 锁住当前索引命中的当前的行，没有命中就退化成间隙锁。（查询、更新都会阻塞）

  ```tex
  当我们对于唯一性的索引（包括唯一索引和主键索引）使用等值查询，精准匹配到一条记录的时候，这个时候使用的就是记录锁。
  比如 where id = 1 4 7 10 。相当于就锁住当前索引所在的行。
  ```

- **间隙锁**

  - [间隙所案例分析](https://www.jianshu.com/p/32904ee07e56)

  - 查询没有命中的时候就会锁住间隙。（只有更新操作会阻塞，查询不会阻塞）

  ```tex
  当我们查询的记录不存在，没有命中任何一个 record，无论是用等值 查询还是范围查询的时候，它使用的都是间隙锁。 举个例子，where id >4 and id <7，where id = 6。
  重复一遍，当查询的记录不存在的时候，使用间隙锁。 
  注意，间隙锁主要是阻塞插入 insert。相同的间隙锁之间不冲突。查询是不会被阻塞的。
  
  Gap Lock 只在 RR(重复读) 中存在。如果要关闭间隙锁，就是把事务隔离级别设置成 RC， 并且把 innodb_locks_unsafe_for_binlog 设置为 ON。
  
  这种情况下除了外键约束和唯一性检查会加间隙锁，其他情况都不会用间隙锁。
  ```

- **临键锁**

  ```tex
  当我们使用了范围查询，不仅仅命中了 Record 记录，还包含了 Gap 间隙，在这种情况下我们使用的就是临键锁，它是MySQL里面默认的行锁算法，相当于记录锁加上间隙锁。
  
  临键锁，锁住最后一个 key 的下一个左开右闭的区间。
  ```






# MySQL优化模块

## 1、[Buffer Pool优化](https://blog.csdn.net/suo082407128/article/details/102580630)

- **innodb_buffer_pool_size** 默认128兆

  配置缓冲池的大小，在内存允许的情况下，DBA往往会建议调大这个参数，越多数据和索引放到内存里，数据库的性能会越好。

  ```properties
  SHOW VARIABLES LIKE 'innodb_buffer_pool_size'; 
  134217728byte=128M
  ```

- **innodb_old_blocks_pct** 默认37

  老生代占整个LRU链长度的比例，默认是37，即整个LRU中新生代与老生代长度比例是63:37。

  如果把这个参数设为100，就退化为普通LRU了。

  ```properties
  SHOW VARIABLES LIKE 'innodb_old_blocks_pct';
  innodb_old_blocks_pct=37 
  ```

- **innodb_old_blocks_time** 默认1s

  老生代停留时间窗口，单位是毫秒，默认是1000，即同时满足“被访问”与“在老生代停留时间超过1秒”两个条件，才会被插入到新生代头部。

  ```properties
  SHOW VARIABLES LIKE 'innodb_old_blocks_time';
  innodb_old_blocks_time=1000ms
  ```

- **总结**

  （1）缓冲池(buffer pool)是一种**常见的降低磁盘访问的机制；**

  （2）缓冲池通常**以页(page)为单位缓存数据；**

  （3）缓冲池的**常见管理算法是LRU**，memcache，OS，InnoDB都使用了这种算法；

  （4）InnoDB对普通LRU进行了优化：

  - 将缓冲池分为**老生代和新生代**，入缓冲池的页，优先进入老生代，页被访问，才进入新生代，以解决预读失效的问题
  - 页被访问，且在老生代**停留时间超过配置阈值**的，才进入新生代，以解决批量数据访问，大量热数据淘汰的问题

## 2、记一次SQL执行慢的原因排查

- **df -h  查看磁盘使用情况**

  ```
  [root@localhost /]# df -h
  Filesystem      Size  Used Avail Use% Mounted on
  /dev/sda1        40G   19G   22G  48% /
  devtmpfs        2.8G     0  2.8G   0% /dev
  tmpfs           2.8G     0  2.8G   0% /dev/shm
  tmpfs           2.8G  8.8M  2.8G   1% /run
  tmpfs           2.8G     0  2.8G   0% /sys/fs/cgroup
  tmpfs           567M     0  567M   0% /run/user/1000
  tmpfs           567M     0  567M   0% /run/user/0
  ```

- **free -h 查看内存使用情况**

  ```tex
  [root@localhost /]# free -h
                total        used        free      shared  buff/cache   available
  Mem:           5.5G        700M        4.3G        8.7M        574M        4.6G
  Swap:          2.0G          0B        2.0G
  ```

- **top 查看进程资源占用情况**

  ```tex
  [root@localhost /]# top
  top - 18:12:04 up 10:44,  
  1 user,  
  load average: 0.00, 0.01, 0.05
  Tasks:  97 total,   1 running,  96 sleeping,   0 stopped,   0 zombie
  %Cpu(s):  0.0 us,  0.2 sy,  0.0 ni, 99.8 id,  0.0 wa,  0.0 hi,  0.0 si,  0.0 st
  KiB Mem :  5799440 total,  4494216 free,   717016 used,   588208 buff/cache
  KiB Swap:  2097148 total,  2097148 free,        0 used.  4818928 avail Mem 
  
    PID USER      PR  NI    VIRT    RES    SHR S  %CPU %MEM     TIME+ COMMAND             4554 polkitd   20   0 1771428 438996  22964 S   0.7  7.6   5:19.28 mysqld             9 root      20   0       0      0      0 S   0.3  0.0   0:24.76 rcu_sched 
  ```

  































