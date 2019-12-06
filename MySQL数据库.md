# 1 mysql的安装与配置

## 1.1 登录与退出
	 -mysql -uroot -proot -h127.0.0.1 -P3306
			 用户名  密码    主机地址     端口号

	 - exit
	 - quit
	 - \q

## 1.2 修改MySQL提示符 PROMPT
	 - PROMPT可以修改MySQL提示符
	 - PROMPT \u  ---显示用户
	 - PROMPT \h  ---显示主机地址
	 - PROMPT \d  ---显示当前使用的数据库
	 - PROMPT \D  ---显示当前时间

	 - 我习惯的提示符：
	 - \u@\h \d >

# 2 操作数据库

## 2.1 创建数据库
	 - {}----代表必选项 
	 - []----代表可选项
	 - 
	 - CREATE ｛DATABASE | SCHEMA｝[IF NOT EXIST] db_name [DEFAULT] CHARACTER SET [=] charset_name;

	 - IF NOT EXIST：在数据库已经存在的情况下,创建时加上这句话,就不会报错,但是会产生警告信息；
	 - 利用SHOW WARNINGS；命令来查看警告信息。

	 - 
	 -e.g. CREATE DATABASE t1 DEFAULT CHARACTER SET = UTF8;

## 2.2  查看当前服务器下的数据库列表
	 - SHOW {DATABASES | SCHEMAS} [LIKE 'pattern' | WHERE expr]

	 - e.g. SHOW DATABASES t1;

## 2.3 查看创建数据库时的信息
	 - SHOW CREATE DATABASE t2;

## 2.4 修改数据库编码方式
	 - ALTER {DATABASE | SCHEMA} [db_name] [DEFAULT] CHARACTER SET [=] charset_name;

## 2.5 删除数据库
	 - DROP {DATABASE | SCHEMA} [IF EXISTS] db_name;

# 3 数据类型

## 3.1 整形（有符号和无符号）
	 - TINYINT   相当于java中的byte
	 - SMALLINT  相当于java中的short
	 - MEDIUMINT 3个字节
	 - INT       4个字节
	 - BIGINT    相当于java中的long

## 3.2 浮点型
	 - FLOAT[(M,D)] 
	 - M是数字总位数,D是小数点后面的位数
	 - 如果MD被省略,则根据硬件允许的限制来保存值.
	 - 单精度浮点精确到大约7位小数位

	 - DOUBLE[(M,D)]
	 - 双精度浮点
	 - 精度：1.79e+308

## 3.3 日期时间型
	 - YEAR			年
	 - TIME			月
	 - DATE 		1000/1/1-9999/12/31
	 - DATETIME		1000/1/1 00:00:00 -9999/12/31 23:59:59
	 - TIMESTAMP	1970/1/1 -2037

## 3.4 字符型
	 - CHAR     					0-255		定长类型
	 - VARCHAR  					0-65535		变长类型
	 - TINYTEXT 				2^8
	 - TEXT     				2^16
	 - MEDIUMTEXT 				2^24
	 - LONGTEXT 				2^32
	 - ENUM('value1','value2')
	 - SET('value1','value2')