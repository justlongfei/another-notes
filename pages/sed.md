- 特指`gnu sed`
	- 中文：流式编辑器
	- 官网： [https://www.gnu.org/software/sed/](https://www.gnu.org/software/sed/)
	- 手册： [https://www.gnu.org/software/sed/manual/sed.html](https://www.gnu.org/software/sed/manual/sed.html)
- mac上自带sed，与`gnu sed`使用有点区别，可以使用`brew install gnu-sed`来安装`gnu sed`，`gnu sed`的名称为`gsed`，以区别mac自带的sed。
- `sed`常常需要与[[正则表达式]]搭配使用
- 介绍
	- 格式：`sed OPTIONS... [SCRIPT] [INPUTFILE...]`
	- 常用选项
		- `-n`：禁止sed输出
			- sed默认会将处理后的结果输出到终端，使用`-n`选项可以禁止sed输出结果
			- 使用`-n`和`p`命令常搭配起来输出一些过滤后的结果
		- `-i`：就地修改
			- 使用`-i[SUFFIX]`，那么会在修改之前将原始文件备份为`原始文件名[SUFFIX]`，如下：
			  ```bash
			  ❯ gsed -i.bar p foo
			  ❯ ls
			  foo  foo.bar
			  ```
		- `-e`和`-f`：指定操作
			- 通过`-e`指定command，通过`-f`指定包含命令的文件
			- `-e`和`-f`可以出现多次，sed会按照顺序执行指定的命令
			- 如果缺省`-e`和`-f`，那么sed会将出现的第一个参数当作命令脚本
		- `-E`：启用扩展的正则表达式语法
	- 地址
		- 地址是可选的，如果sed不指定地址，那么就是对文件的全部行执行操作
		- 通过数字指定操作的行或者范围
			- `'[n]command'`：n为数字，可选，对第n行进行操作
				- 比如删除第二行
				  ```bash
				  ❯ gsed -e '2d' foo
				  1 first line
				  3 third line
				  ```
			- `'[m,n]command'`：m，n为数字，表示对从第m行开始到第n行结束的闭区间范围的数据进行操作，`$`是一种特殊符号，表示文件的末尾。
				- 比如删除2～3行
				  ```bash
				  ❯ gsed -e '2,3d' foo
				  1 first line
				  ```
		- 通过文本指定操作匹配的行
			- 不显式指定行或者范围，而是通过指定正则表达式作为匹配规则，对匹配到的行做相应的操作
			- 格式：`'[/pattern]/command'`
			- 例：打印出文件中包含1或者2的行
			  ```bash
			  ❯ gsed -n -e '/[1|2]/p' foo
			  1 first line
			  2 second line
			  ```
	- 命令
		- 格式：
			- 单个命令 `[address]command`
			- 一组命令
			  ```bash
			  address {
			      command1
			      command2
			      ...
			  }
			  ```
		- 输出
			- `p`
				- 格式：`[address]p`
		- 替换
			- `s`：正则表达式匹配，并将匹配的内容做替换
				- 格式：`[address]s/pattern/replacement/flags`
			- `c`：行替换
				- 格式：`[address]c\用于替换的新文本`
			- `y`：字符转换，inchars和outchars一对一字符替换，如果两者长度不同，sed报错
				- 格式：`[address]y/inchars/outchars/`
		- 删除
			- `d`：行删除
				- 格式：`[address]d`
		- 插入
			- 格式：`[address](a/i) \新文本内容`
			- `a`：行后插入
			- `i`：行前插入