# 使用 PostgreSQL 的 RUM 索引和全文搜索

> 原文：<https://medium.datadriveninvestor.com/the-rum-index-and-full-text-search-using-postgresql-1c08fb3bf540?source=collection_archive---------2----------------------->

![](img/f0d7fbeccf5599c9fce735d2f0551960.png)

*通过 Digoal。*

[全文搜索](https://www.techopedia.com/definition/17113/full-text-search?spm=a2c41.13532596.0.0)和[模糊查询](https://www.elastic.co/guide/en/elasticsearch/reference/current/query-dsl-fuzzy-query.html?spm=a2c41.13532596.0.0)是两种极其常见和广泛使用的查询类型。事实上，这两种类型的查询恰好也是许多现代在线搜索引擎的主干部分。

通常，当我们想到搜索引擎时，我们只是认为它们满足了我们的搜索需求，而没有考虑后台发生的事情。但是，在现实中，有很多事情正在进行，除了数据同步到搜索引擎，还有同步延迟，更新，甚至数据一致性的问题要处理。

[](https://www.datadriveninvestor.com/2019/02/25/6-alternatives-to-the-yahoo-finance-api/) [## 雅虎财经 API |数据驱动投资者的 6 种替代方案

### 长期以来，雅虎金融 API 一直是许多数据驱动型投资者的可靠工具。许多人依赖于他们的…

www.datadriveninvestor.com](https://www.datadriveninvestor.com/2019/02/25/6-alternatives-to-the-yahoo-finance-api/) 

当你花一分钟去思考这一切的时候，所有这些都是相当令人印象深刻的。

好了，现在让我们来看看这一切是如何与 [PostgreSQL](https://www.postgresql.org/?spm=a2c41.13532596.0.0) 一起工作的。PostgreSQL 内置的全文搜索数据类型和对全模糊查询的索引支持可以满足您的所有需求，整个系统的效率也相当不错。例如，在 10 亿个令牌中进行搜索，可以在几毫秒内返回结果。

接下来，除此之外，最近更新的 [PostgreSQL 9.6](https://www.postgresql.org/about/news/1703/?spm=a2c41.13532596.0.0) 在 PosgreSQL 的全文搜索功能和优化方面做了许多增强。此外， [RUM 插件](https://github.com/postgrespro/rum?spm=a2c41.13532596.0.0)，正如[PG 社区的核心提交者 Oleg Bartunov](https://twitter.com/obartunov?spm=a2c41.13532596.0.0&lang=en) 所说，在某种程度上打开了潘多拉的盒子，因为它大大提高了 PostgreSQL 的搜索效率，甚至比 [GIN](https://hashrocket.com/blog/posts/exploring-postgres-gin-index?spm=a2c41.13532596.0.0) 还要好。

# 方案

考虑下面的场景，看看 PostgreSQL 的更新如何帮助提供一些强大的优化。

这是一个常见的场景。很多用户会用逗号分隔要搜索的元素，以字符串的形式存储在数据库中，然后用模糊查询来检索数据。

```
create table test(c1 text);
insert into test values ('1,100,2331,344,502,.........');
insert ............
.....
```

接下来，对于这些数据库中的 1000 万条这样的记录，基于元素的组合来执行查询。

```
select * from test where c1 like '%1%' or c1 like '%502%' and c1 like '%2331%';
```

然而，所有这些导致查询效率非常低。这是有问题的。如果要在毫秒内返回数据，几乎是不可想象的。然而，PostgreSQL 的更新可以帮助解决这种情况。

# PostgreSQL 数组

首先，PostgreSQL 中的[数组](https://www.postgresql.org/docs/9.1/arrays.html)可以满足上述场景。

```
create table arr_test(c1 int[]);create index idx_arr_test on arr_test using gin(c1);insert into arr_test values(array[1,100,2331,344,502,......]);
......
```

PostgreSQL 数组支持 GIN 索引，这允许更快的搜索。例如，下面的搜索在 1000 万条记录中搜索包含 1 或 2 的记录。只用了几毫秒就完成了。

```
postgres=# explain analyze select * from arr_test where c1 && array[1,2] order by c1 offset 19000 limit 100;
                                                                QUERY PLAN                                                                 
-------------------------------------------------------------------------------------------------------------------------------------------
 Limit  (cost=112837.69..112837.94 rows=100 width=424) (actual time=91.440..91.475 rows=100 loops=1)
   ->  Sort  (cost=112790.19..113039.57 rows=99750 width=424) (actual time=82.915..90.477 rows=19100 loops=1)
         Sort Key: c1
         Sort Method: external merge  Disk: 8440kB
         ->  Bitmap Heap Scan on arr_test  (cost=816.06..93595.94 rows=99750 width=424) (actual time=9.180..37.380 rows=19925 loops=1)
               Recheck Cond: (c1 && '{1,2}'::integer[])
               Heap Blocks: exact=19605
               ->  Bitmap Index Scan on idx_arr_test  (cost=0.00..791.12 rows=99750 width=0) (actual time=5.196..5.196 rows=19925 loops=1)
                     Index Cond: (c1 && '{1,2}'::integer[])
 Planning time: 0.131 ms
 Execution time: 93.929 ms
(11 rows)
```

# PostgreSQL 全文搜索

PostgreSQL 还支持全文搜索。您可以将元素存储为一个`tsvector`并使用`tsquery`进行查询。

```
postgres=# create table gin_test(c1 tsvector);
CREATE TABLEpostgres=# create index idx_gin_test on gin_test using gin (c1) ;
CREATE INDEX
```

这些 PostgreSQL 全文搜索还支持索引来加速查询。例如，您可以搜索 1000 万条记录中包含 1 或 2 的记录。

# 朗姆酒如何改变一切

当使用 GIN 索引时，扫描方法是[位图](https://www.techopedia.com/definition/792/bitmap-bmp)，因此结果需要执行一个`SORT`动作。但是同样地，如果你有一个相当大的列表，这可能会非常耗时。

而 PostgreSQL 9.6 的插件`[RUM](https://github.com/postgrespro/rum)` index 接口为全文搜索提供了更强大的支持，直接使用`INDEX SCAN`接口，无需`SORT`。换句话说，RUM 还实现了`<=>`文本相似性属性检索。

Prostgres Professional 的首席执行官和 PG 社区的核心委员 Oleg Bartunov 说，朗姆酒在许多方面都打开了潘多拉的盒子。除了 PostgreSQL 9.6 在全文搜索优化方面取得了长足的进步之外，RUM 也是一个重要的甚至是巨大的变化——它真正改变了一切。

为了更好地理解 RUM，让我们忘记搜索引擎，转而使用 PostgreSQL，体验它的一些特性。首先让我们测试朗姆酒。

```
postgres=# create table rum_test(c1 tsvector);
CREATE TABLEpostgres=# CREATE INDEX rumidx ON rum_test USING rum (c1 rum_tsvector_ops);
CREATE INDEX
```

有关本文的更多信息，您也可以查看我最近的文章[PostgreSQL 文本数据库的相似性分析](https://www.alibabacloud.com/blog/similarity-analysis-for-postgresql-text-databases_595341)。

# 比较:数组与全文搜索以及 GIN 与 RUM

做了上面的简单测试之后，我们再来比较一下数组 GIN 索引、全文搜索 GIN 索引和全文搜索 RUM 索引。每个的表结构如下:

```
postgres=# create table rum_test(c1 tsvector);
CREATE TABLEpostgres=# create table gin_test(c1 tsvector);
CREATE TABLEpostgres=# create table arr_test(c1 int[]);
CREATE TABLE
```

插入 1000 万条记录，每个字段有 100 个随机值，相当于在 10 亿个随机值中执行匹配操作。对所有人都这样做:

```
$ vi test.sql
insert into rum_test select to_tsvector(string_agg(c1::text,',')) from  (select (100000*random())::int from generate_series(1,100)) t(c1);$ pgbench -M prepared -n -r -P 1 -f ./test.sql -c 50 -j 50 -t 200000 $ vi test.sql
insert into gin_test select to_tsvector(string_agg(c1::text,',')) from  (select (100000*random())::int from generate_series(1,100)) t(c1);$ pgbench -M prepared -n -r -P 1 -f ./test.sql -c 50 -j 50 -t 200000 $ vi test.sql
insert into arr_test select array_agg(c1) from  (select (100000*random())::int from generate_series(1,100)) t(c1);$ pgbench -M prepared -n -r -P 1 -f ./test.sql -c 50 -j 50 -t 200000
```

接下来，为它们分别创建一个索引:

```
postgres=# set maintenance_work_mem ='64GB';
SET
postgres=# CREATE INDEX rumidx ON rum_test USING rum (c1 rum_tsvector_ops);
CREATE INDEXpostgres=# create index idx_gin_test on gin_test using gin (c1) ;
CREATE INDEXpostgres=# create index idx_arr_test on arr_test using gin (c1) ;
CREATE INDEX
```

## 比较查询效率

现在我们来比较一下查询效率。查询包含 1 或 2 的记录。

```
Full-text search type with rum index:
postgres=# explain analyze select * from rum_test where c1 @@ to_tsquery('English','1 | 2');
                                                            QUERY PLAN                                                            
----------------------------------------------------------------------------------------------------------------------------------
 Index Scan using rumidx on rum_test  (cost=16.00..99121.61 rows=99749 width=1387) (actual time=6.403..24.981 rows=19840 loops=1)
   Index Cond: (c1 @@ '''1'' | ''2'''::tsquery)
 Planning time: 0.075 ms
 Execution time: 26.086 ms
(4 rows)Full-text search with GIN ind
postgres=# explain analyze select * from gin_test where c1 @@ to_tsquery('english','1 | 2');
                                                          QUERY PLAN                                                           
-------------------------------------------------------------------------------------------------------------------------------
 Bitmap Heap Scan on gin_test  (cost=816.06..99386.94 rows=99750 width=1387) (actual time=9.551..34.121 rows=19847 loops=1)
   Recheck Cond: (c1 @@ '''1'' | ''2'''::tsquery)
   Heap Blocks: exact=19764
   ->  Bitmap Index Scan on idx_gin_test  (cost=0.00..791.12 rows=99750 width=0) (actual time=5.554..5.554 rows=19847 loops=1)
         Index Cond: (c1 @@ '''1'' | ''2'''::tsquery)
 Planning time: 0.113 ms
 Execution time: 35.279 ms
(7 rows)Array with Gin index:postgres=# explain analyze select * from arr_test where c1 && array[1,2];
                                                          QUERY PLAN                                                           
-------------------------------------------------------------------------------------------------------------------------------
 Bitmap Heap Scan on arr_test  (cost=816.06..93595.94 rows=99750 width=424) (actual time=9.148..31.648 rows=19925 loops=1)
   Recheck Cond: (c1 && '{1,2}'::integer[])
   Heap Blocks: exact=19605
   ->  Bitmap Index Scan on idx_arr_test  (cost=0.00..791.12 rows=99750 width=0) (actual time=5.214..5.214 rows=19925 loops=1)
         Index Cond: (c1 && '{1,2}'::integer[])
 Planning time: 0.095 ms
 Execution time: 32.810 ms
(7 rows)
```

现在对输出进行排序:

```
Full-text search with rum index:
postgres=# explain analyze select * from rum_test where c1 @@ to_tsquery('english','1 | 2') order by c1 <=> to_tsquery('english','1 | 2') offset 19000 limit 100;
                                                               QUERY PLAN                                                                
-----------------------------------------------------------------------------------------------------------------------------------------
 Limit  (cost=18988.45..19088.30 rows=100 width=1391) (actual time=58.912..59.165 rows=100 loops=1)
   ->  Index Scan using rumidx on rum_test  (cost=16.00..99620.35 rows=99749 width=1391) (actual time=16.426..57.892 rows=19100 loops=1)
         Index Cond: (c1 @@ '''1'' | ''2'''::tsquery)
         Order By: (c1 <=> '''1'' | ''2'''::tsquery)
 Planning time: 0.133 ms
 Execution time: 59.220 ms
(6 rows)Full-text search with GIN index:
postgres=# explain analyze select * from gin_test where c1 @@ to_tsquery('english','1 | 2') order by c1 offset 19000 limit 100;
                                                                QUERY PLAN                                                                 
-------------------------------------------------------------------------------------------------------------------------------------------
 Limit  (cost=176684.69..176684.94 rows=100 width=1387) (actual time=117.809..117.865 rows=100 loops=1)
   ->  Sort  (cost=176637.19..176886.57 rows=99750 width=1387) (actual time=94.889..116.929 rows=19100 loops=1)
         Sort Key: c1
         Sort Method: external merge  Disk: 26968kB
         ->  Bitmap Heap Scan on gin_test  (cost=816.06..99386.94 rows=99750 width=1387) (actual time=9.625..38.336 rows=19847 loops=1)
               Recheck Cond: (c1 @@ '''1'' | ''2'''::tsquery)
               Heap Blocks: exact=19764
               ->  Bitmap Index Scan on idx_gin_test  (cost=0.00..791.12 rows=99750 width=0) (actual time=5.610..5.610 rows=19847 loops=1)
                     Index Cond: (c1 @@ '''1'' | ''2'''::tsquery)
 Planning time: 0.134 ms
 Execution time: 126.122 ms
(11 rows)Array with GIN index:postgres=# explain analyze select * from arr_test where c1 && array[1,2] order by c1 offset 19000 limit 100;
                                                                QUERY PLAN                                                                 
-------------------------------------------------------------------------------------------------------------------------------------------
 Limit  (cost=112837.69..112837.94 rows=100 width=424) (actual time=90.619..90.656 rows=100 loops=1)
   ->  Sort  (cost=112790.19..113039.57 rows=99750 width=424) (actual time=82.067..89.622 rows=19100 loops=1)
         Sort Key: c1
         Sort Method: external merge  Disk: 8440kB
         ->  Bitmap Heap Scan on arr_test  (cost=816.06..93595.94 rows=99750 width=424) (actual time=9.087..36.870 rows=19925 loops=1)
               Recheck Cond: (c1 && '{1,2}'::integer[])
               Heap Blocks: exact=19605
               ->  Bitmap Index Scan on idx_arr_test  (cost=0.00..791.12 rows=99750 width=0) (actual time=5.138..5.138 rows=19925 loops=1)
                     Index Cond: (c1 && '{1,2}'::integer[])
 Planning time: 0.122 ms
 Execution time: 93.057 ms
(11 rows)
```

# 朗姆酒的一些附加功能

Rum 搜索支持相似度排名，这在搜索中很有用。相似性得分指示文本和搜索条件之间的相似性。

```
// Word Breaking example
postgres=#  select * from to_tsvector('jiebacfg', 'Xiao Ming graduated with a master's degree from the Institute of Computing Technology of the Chinese Academy of Sciences, and later went on to study at Kyoto University in Japan.');
                                   to_tsvector                                    
----------------------------------------------------------------------------------
 'Chinese Academy of Sciences':5 'Xiao Ming':1 'Kyoto University':10 'graduated':3 'study':11 'master's degree':2 'Institute of Computing Technology':6
(1 row)
// With Similarities
postgres=#  select * from rum_ts_distance(to_tsvector('jiebacfg', 'Xiao Ming graduated with a master's degree from the Institute of Computing Technology of the Chinese Academy of Sciences, and later went on to study at Kyoto University in Japan.') , to_tsquery('Institute of Computing Technology'));
 rum_ts_distance 
-----------------
         16.4493
(1 row)
// Without similarities
postgres=#  select * from rum_ts_distance(to_tsvector('jiebacfg', 'Xiao Ming graduated with a master's degree from the Institute of Computing Technology of the Chinese Academy of Sciences, and later went on to study at Kyoto University in Japan.') , to_tsquery('Computing Technology'));
 rum_ts_distance 
-----------------
        Infinity
(1 row)
// One or the other has similarities
postgres=# select * from rum_ts_distance(to_tsvector('jiebacfg', 'Xiao Ming graduated with a master's degree from the Institute of Computing Technology of the Chinese Academy of Sciences, and later went on to study at Kyoto University in Japan.') , to_tsquery('The Institute of Computing Technology | master's degree'));
 rum_ts_distance 
-----------------
         8.22467
(1 row)
// Both have similarities
postgres=# select * from rum_ts_distance(to_tsvector('jiebacfg', 'Xiao Ming graduated with a master's degree from the Institute of Computing Technology of the Chinese Academy of Sciences, and later went on to study at Kyoto University in Japan.') , to_tsquery('Institute of Computing Technology & master's degree'));
 rum_ts_distance 
-----------------
         32.8987
(1 row)
// Order
postgres=# create table test15(c1 tsvector);
CREATE TABLE
postgres=# insert into test15 values (to_tsvector('jiebacfg', 'hello china, i''m digoal')), (to_tsvector('jiebacfg', 'hello world, i''m postgresql')), (to_tsvector('jiebacfg', 'how are you, i''m digoal'));
INSERT 0 3
postgres=# select * from test15;
                         c1                          
-----------------------------------------------------
 ' ':2,5,9 'china':3 'digoal':10 'hello':1 'm':8
 ' ':2,5,9 'hello':1 'm':8 'postgresql':10 'world':3
 ' ':2,4,7,11 'digoal':12 'm':10
(3 rows)
postgres=# create index idx_test15 on test15 using rum(c1 rum_tsvector_ops);
CREATE INDEX
postgres=# select *,c1 <=> to_tsquery('hello') from test15;
                         c1                          | ?column? 
-----------------------------------------------------+----------
 ' ':2,5,9 'china':3 'digoal':10 'hello':1 'm':8     |  16.4493
 ' ':2,5,9 'hello':1 'm':8 'postgresql':10 'world':3 |  16.4493
 ' ':2,4,7,11 'digoal':12 'm':10                     | Infinity
(3 rows)
postgres=# explain select *,c1 <=> to_tsquery('postgresql') from test15 order by c1 <=> to_tsquery('postgresql');
                                   QUERY PLAN                                   
--------------------------------------------------------------------------------
 Index Scan using idx_test15 on test15  (cost=3600.25..3609.06 rows=3 width=36)
   Order By: (c1 <=> to_tsquery('postgresql'::text))
(2 rows)
```

# 摘要

总结我们的比较，RUM 非常强大，支持相似性搜索和非位图扫描。在查询效率方面，我们在这里自己的比较中的输出结果显示，RUM 的效率是 GIN 和简单数组查询的两倍。因此，如您所见，PostgreSQL 9.6 带来了许多好东西。当然，让我和许多其他开发人员兴奋的是朗姆酒。

# 原始资料

[](https://www.alibabacloud.com/blog/the-rum-index-and-full-text-search-using-postgresql_595343?spm=a2c41.13532596.0.0) [## 使用 PostgreSQL 的 RUM 索引和全文搜索

### PostgreSQL 9.6 最近的更新在全文搜索方面做了很多增强，也为我们带来了 RUM 插件…

www.alibabacloud.com](https://www.alibabacloud.com/blog/the-rum-index-and-full-text-search-using-postgresql_595343?spm=a2c41.13532596.0.0)