- repair table
	- 支持的引擎：MyISAM、ARCHIVE、CSV
	- repair table在某些场景下可能会导致data loss，因此需要先备份table数据
- mysqlcheck
	- lock table
	- time-consuming
	- mysqld必须处在运行状态
	- 可能会导致data loss，先backup
	- 用法：
	  ```bash
	  mysqlcheck [options] db_name [tbl_name ...]
	  mysqlcheck [options] --databases db_name ...
	  mysqlcheck [options] --all-databases
	  ```
- Ref：
	- [repair table](https://dev.mysql.com/doc/refman/8.0/en/repair-table.html)
	- [mysqlcheck](https://dev.mysql.com/doc/refman/8.0/en/mysqlcheck.html)