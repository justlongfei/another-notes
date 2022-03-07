- #mysql #Database
- 可以使用如下sql，从sql mode中删除某个mode：
  ```sql
  -- 禁用only_full_group_by
  SET sql_mode=(SELECT REPLACE(@@sql_mode,'ONLY_FULL_GROUP_BY',''));
  ```