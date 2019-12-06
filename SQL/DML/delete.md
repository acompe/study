## 删除数据 delete
#### 方式一 DELETE
- 单表删除
```sql
DELETE FROM 表名 
WHERE 筛选条件
```
- 多表删除
```sql
# 192
DELETE 要删的表的别名 
FROM 表1 别名，表2 别名
WHERE 连接条件
AND 筛选条件

# 199
DELETE 要删的表的别名 
FROM 表1 别名
INNER | LEFT | RIGHT | FULL JOIN 表2 别名
ON 连接条件
WHERE 筛选条件 
```
#### 方式二 TRUNCATE
介绍：清空表。
```sql
TRUNCATE TABLE 表名;
```