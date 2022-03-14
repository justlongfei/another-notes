- ## 下载MySQL源码
  
  1. 点击下载 [mysql-boost-8.0.27.tar.gz](https://cdn.mysql.com//Downloads/MySQL-8.0/mysql-boost-8.0.27.tar.gz)
  
  2. 解压到开发目录下
- ## 配置vscode
  
  1. 安装插件
   C/C++（ms-vscode.cpptools）
   CMake Tools（ms-vscode.cmake-tools）
  
  2. 打开mysql源码目录
  
  3. 配置《settings.json》
  
   ```json
  {
    "cmake.configureOnOpen": true,
    "cmake.buildDirectory": "${workspaceFolder}/bld",
    "cmake.installPrefix": "${workspaceFolder}/inst",
    "cmake.configureArgs": [
        "-DWITH_UNIT_TESTS=OFF",
        "-DCMAKE_BUILD_TYPE=Debug",
        "-DWITH_BOOST=${workspaceFolder}/boost",
        "-DWITH_SSL=/usr/local/opt/openssl@1.1",
    ]
  }
  ```
- ## 通过cmake配置、编译MySQL
  
  1. ctrl+shift+P，输入CMake: Configure
  2. ctrl+shift+P，输入CMake: Set Build Target，选择mysqld
  3. ctrl+shift+P，输入CMake: Build
  📝 configure遇到的问题记录：
	- Could not find system OpenSSL
	  	通过brew安装openssl，并通过-DWITH_SSL指定位置
	- Could not run sw_vers
	  	最新的monterey上会遇到这个[BUG](https://bugs.mysql.com/bug.php?id=105464#c517341)
- 等待编译完成，需要较长的时间
## 初始化data目录

```bash
cd bld
bin/mysqld --initialize-insecure
```
## 启动MySQL

1. ctrl+shift+P，输入CMake: Set Debug Target，选择mysqld

2. ctrl+shift+P，输入CMake: Debug

3. 使用mysql client连接到mysqld

 ```bash
 cd bld
 bin/mysql -h127.0.0.1 -P3306 -uroot
 ```

 ```mysql
 mysql> select version();
 +--------------+
 | version()    |
 +--------------+
 | 8.0.25-debug |
 +--------------+
 1 row in set (0.01 sec)
 ```
- ## 指定命令行参数
	- 配置《launch.json》，配置完成后通过`f5`启动调试
	  ```json
	  {
	      "version": "0.2.0",
	      "configurations": [
	          {
	              "name": "Test open source MySQL(8.0.27)",
	              "type": "cppdbg",
	              "request": "launch",
	              // Resolved by CMake Tools:
	              "program": "${command:cmake.launchTargetPath}",
	              "args": [
	                  "--port", "4001",
	              ],
	              "stopAtEntry": false,
	              "cwd": "${workspaceFolder}",
	              "environment": [
	                  {
	                      // add the directory where our target was built to the PATHs
	                      // it gets resolved by CMake Tools:
	                      "name": "PATH",
	                      "value": "${env:PATH}:${command:cmake.getLaunchTargetDirectory}"
	                  },
	              ],
	              "externalConsole": false,
	              "MIMode": "lldb",
	              "setupCommands": [
	                  {
	                      "description": "Enable pretty-printing for gdb",
	                      "text": "-enable-pretty-printing",
	                      "ignoreFailures": true
	                  }
	              ]
	          }
	      ]
	  }
	  ```
- ## Ref
	- https://github.com/microsoft/vscode-cmake-tools/blob/main/docs/debug-launch.md