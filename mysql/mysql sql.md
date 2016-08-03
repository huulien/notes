# mysql常用sql

## 锁相关sql

```sql
# 查询是否锁表
show OPEN TABLES where In_use > 0;
 
# 查看正在锁的事务
SELECT * FROM INFORMATION_SCHEMA.INNODB_LOCKS; 
  
# 查看等待锁的事务
SELECT * FROM INFORMATION_SCHEMA.INNODB_LOCK_WAITS; 
```