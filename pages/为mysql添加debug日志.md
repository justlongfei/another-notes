- 参考 [[配置MySQL的vscode开发环境]]，编译debug版本的mysql
- 在`Query_block::prepare`函数的结尾添加如下代码
  ```c++
    String str = String(4096);
    this->print(thd, &str, QT_ORDINARY);
    DBUG_PRINT("info", ("query block is %s", str.c_ptr()));
  ```
- 使用mysql客户端连接server后执行如下sql：
  ```sql
  set debug ="debug=d,info,error,query,general,where:O,/tmp/mysqld.trace";
  ```
  这样便能将debug日志打印到指定的文件`/tmp/mysqld.trace`当中