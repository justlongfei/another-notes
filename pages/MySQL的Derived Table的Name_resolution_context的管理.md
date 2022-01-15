title:: MySQL的Derived Table的Name_resolution_context的管理

- 以下是一条嵌套的derived table：
  g1代表整条query，d1代表最外层的derived table，g2代表最外层子查询...
  ```sql
  g1 <--- select id
  d1 <--- from (
  g2 <---     select id
  d2 <---     from (
  g3 <---         select id
  d3 <---         from (
  g4 <---             select id from t
     <---          ) t1
     <---      ) t2
     <--- ) t3;
  ```
- 进入`PT_derived_table`的`contextualize`函数后，如果derived table没有lateral属性，就会`push_context`，处理完subquery后`pop_context`。
- step2：进入`PT_subquery`的`contextualize`函数，调用`new_query`创建一个新的query block，过程中会调用`set_context`初始化一个context，并`push_context`，子查询`contextualize`退出之前`pop_context`。
- `LEX`结构体中维护`Name_resolution_context`栈的状态在处理完`g4`后的状态如下图所示：
	- [[draws/2022-01-15-22-59-24.excalidraw]]
		- 左侧是`*NameResolutionContext`栈，用于维护标识符的解析context。MySQL在生成`Item_Ident`的时候，会从取栈顶的`context`作为其名称解析的context。
		- 每层DerivedTable（d1，d2等），其context指向的是更外层的query，如d2的context指向g1，而不是g2。也就是说，derived table的context是指：包含derived table所在from子句的外层context。
		- 隐藏信息：g(i+1)会以d(i)的context为自己的outer context。这样，我们在处理子查询的时候，其外层的context，就是更外层的query。