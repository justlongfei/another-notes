- #mysql
- mysql中执行ddl，有时候会卡住，通过执行
  ```sql
  select * from information_schema.processlist where command != "Sleep";
  ```
  能够看到ddl表现为`Waiting for table metadata lock`。
- 通过执行下面这条sql，可以看到mysql当中未提交的事务的thread id，通过第二条sql可以查看该thread id的具体信息
  ```sql
  select * from information_schema.innodb_trx\G
  select * from information_schema.processlist where id = 430\G
  ```
- 参考资料