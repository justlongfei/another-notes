- 数据库以mysql为准
- 空集：empty_set
	- select 1 from dual where 1!=1;
- not in、null与empty_set
	- 1. empty_set not in (empty_set)  --> true
	  2. null not in (empty_set) --> true
	  3. null not in (non-empty) --> null
	- 4. not null not in (empty_set)  --> true
	  5. not null not in (non-empty) --> true/false/null
	- 结论：
		- whatever not in (empty_set) is always true