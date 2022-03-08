title:: mysql的优化开关optimizer_switch

- #mysql #Database
- 官方说明
	- [Switchable Optimizations](https://dev.mysql.com/doc/refman/8.0/en/switchable-optimizations.html)
- 单独设置某个开关
	- `SET [GLOBAL|SESSION] optimizer_switch='command[,command]...';`
- 各个开关优化详情：
	- derived_merge
		- 是否将derived table或者view合并到外层query block当中去
		- [[mysql中derived table处理策略]]
		- 详情说明： [derived-table-optimization](https://dev.mysql.com/doc/refman/8.0/en/derived-table-optimization.html)