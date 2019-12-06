## UNION 联合查询
介绍：将多个没有任何关系的表信息进行并排输出，且查询信息一致时，就需要union，求其并集。
```sql
SELECT * 
FROM employees 
WHERE email LIKE '%a%' OR department_id >90

# UNION
SELECT * FROM employees WHERE email LIKE '%a%' 
UNION
SELECT * FROM employees WHERE department_id >90
```
- 注意：
    - UNION会自动去重，如果不想去重，则需要增加 UNION ALL 关键字。