## 更新数据 update
#### 单表修改
```sql
UPDATE 表名
SET 列1 = 值1，列2= 值2
WHERE id = id值
```
#### 多表修改
```sql
# 192
UPDATE 表名 别名，表名，别名
SET 列1 = 值1， 列2= 值2
WHERE 连接条件
AND 筛选条件

# 199 
UPDATE 表名 别名
INNER | LEFT | RIGHT | FULL JOIN 表名2 别名2
ON 连接条件
SET 列1 = 值1，列2 = 值2
WHERE 筛选条件
```