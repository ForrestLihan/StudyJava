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
	 
	 
## 4 操作数据表

## 4.1 创建数据表
	
	 - CREATE TABLE [IF NOT EXISTS] table_name (
	   column_name1 data_type [SIGNED | UNSIGNED] NOT NULL [AUTO_INCREMENT] PRIMARY KEY ,
	   column_name2 data_type [SIGNED | UNSIGNED] [NULL | NOT NULL] UNIQUE KEY ,
	   column_name3 data_type DEFAULT val,
	   column_name4 data_type...);
	 
	 - 主键约束（PRIMARY KEY）
	 - 一个记录表中只能存在一个主键,主键可以保证记录的唯一性,主键自动为NOT NULL

	 - 唯一约束（UNIQUE KEY）
	 - 唯一约束可以保证记录的唯一性,
	 - 唯一约束的字段可以为空,
	 - 每张数据表可以存在多个唯一约束.

	 - 默认约束(DEFAULT)
	 - 当插入记录时,如果没有明确为字段赋值,则自动赋予默认值.

	 - NOT NULL和NULL
	 - 设置该字段可以为空或者不能为空

	 - 自增
	 - AUTO_INCREMENT
	 - 将字段设置为自增变量,初始值为1,默认每次自增+1,必须和主键一块使用 	 

	 - e.g. CREATE TABLE tb_1(username VARCHAR(20),age INT UNSIGNED,salary FLOAT(8,2) UNSIGNED)

## 4.2 查看数据表列表
	 - SHOW TABLES [FROM db_name] [LIKE 'pattern' | WHERE expr];

## 4.3 查看数据表结构
	 - SHOW COLUMNS FROM tbl_name;
	 - 或者
	 - DESC tbl_name

## 4.4 插入数据
	 - INSERT [INTO] tbl_name[(column_name,...)] VALUES(value,...);
	 - 如果列名被省略,则需要给所有字段赋值。

## 4.5 查找数据
	 - SELECT expr,...FROM tbl_name;


# ------------------------------------------------

# 概念：
# 1. 约束
	 - 约束保证数据的完整性和一致性.
	 - 约束分为表级约束和列级约束.
	 - 约束类型包括:
	 - NOT NULL(非空约束)
	 - PRIMARY KEY(主键约束)
	 - UNIQUE KEY（唯一约束）
	 - DEFAULT(默认约束)
	 - FOREIGN KEY（外键约束）

## 1.1 外键约束（FOREIGN KEY）
	 - 保持数据一致性,完整性.
	 - 实现一对一或一对多关系.

	 - 外键约束的要求
	 - 1.父表和子表必须使用相同的存储引擎,而且禁止使用临时表.
	 - 2.数据表的存储引擎只能为InnoDB.
	 - 3.外键列和参照列必须具有相似的数据类型.其中数字的长度或是否有符号位必须相同;而字符的长度则可以不同.
	 - 4.外键列和参照列必须创建索引.如果参照列不存在索引的华,MySQL将自动创建索引.
	
	 - 子表：具有外键列的表称为子表
	 - 父表：具有参照列的表称为父表

	 - 外键列：曾经加过FOREIGN KEY的那一列称为外键列
	 - 参照列: 外键列参照的那一列为参照列.

	 - e.g.
		父表
		CREATE TABLE provinces(
		id INT UNSIGNED PRIMARY KEY AUTO_INCREMENT,
		pname VARCHAR(20) NOT NULL
		);

	 	子表
		CREATE TABLE users(
		id INT UNSIGNED PRIMARY KEY AUTO_INCREMENT,
		username VARCHAR(10) NOT NULL,
		pid INT UNSIGNED,
		FOREIGN KEY(pid) REFERENCES provinces(id)
		);

	 	-pid称为外键列,id称为参照列
		
		-通过：SHOW INDEXES FROM provinces[\G] 
		来显示参照列是否已经创建了索引
