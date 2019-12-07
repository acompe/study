# TPL (Transaction Processing Language)事务处理语言
介绍：它的语句能确保被DML语句影响的表的所有行及时得以更新 BEGIN TRANSACTION，COMMIT和ROLLBACK  
## 特点（ACID）
- A原子性 事务是不可分割的整体
- C一致性 从一个一致的状态切换到另一个一致的状态
- I隔离性 事务之间互不干扰，多个事务相互隔离。
- D永久性 一个事务提交后，永久化存储到磁盘中。
## 事务
- 隐式（自动）事务：没有明显的开启和提交，本身就式一条事务，可以自动提交。
    - INSERT
    - UPDATE
    - DELETE
- 显式事务：
```sql
SET autocommit = 0  # 关闭自动提交事务。
START TRANSACTION ; # 可以不写
...                 # 一组逻辑SQL
[SAVEPOIONT]        # 设置回滚点
...
COMMIT | ROLLBACK | ROLLBACK TO #事务提交或回滚     
```
## 问题
- 脏读
    - 一个事务读去了还没有提交的数据（更新）。
- 不可重复读
    - 一个事务多次查询同一份数据，结果不一致。
- 幻读
    - 一个事务读去了还没有提交的数据（插入）。
## 隔离级别
- read uncommitted
    - 读未提交
- read committed
    - 读已提交
- repeatable read
    - 可重读读
- serializable
    - 串行化