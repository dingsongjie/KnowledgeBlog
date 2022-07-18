# $lookup

Mongodb $lookup操作符本质上是一个 left outer join 操作，在实现层面目前只支持 Nested Loop Join，所以查询的性能直接和驱动表（主表）的数据条数有关。比如两个集合，A有 10000条数据，B有2000条数据，在mongodb里直接A $lookup B,这样数据库总共会查询 A表10000次，每条查询出来的数据又会去B表匹配。如果A表数据上万，即使B表的关联查询字段有索引总体速度还是会很慢，所以在mongodb中 $lookup 操作一定要用 较小的 collection $lookup 较大的collection。一般的left join 的场景下基本上都会分页，所以可以在 $lookup 前 添加 $limit操作符，限制驱动表的大小，但是对于 inner join 且 需要对 A $lookup B 结果再进行分页的情况下，mongodb的性能会很差.
