## 存储过程
#### 过程编写
```sql
CREATE PROCEDURE 存储过程名(参数列表)
BEGIN
# 这是一组合法有效的SQL语句
END 
```
- 参数列表
    - 参数模式
        - in ：传入值
        - out：返回值
        - inout：即传入、又输出。
    - 参数名
    - 参数类型
- 设置结束符号
    - delimiter 结束标记
    
#### 过程调用
```sql
CALL 存储过程名（参数）
```
#### 存储过程删除
```sql
DROP PROCEDURE 存储过程名；
# 只能删除一个，不能连续删除。
```

#### 查询存储过程
```sql
# 查看存储过程的创建
SHOW CREATE PROCEDURE 存储过程名  
```