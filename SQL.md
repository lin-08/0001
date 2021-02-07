# SQL<b>
SQL (结构化查询语言)是用于执行查询的语法。但是 SQL 语言也包含用于更新、插入和删除记录的语法。
可以把 SQL 分为两个部分：数据操作语言 (DML) 和 数据定义语言 (DDL)。
<br>tips:①sql对大小写不敏感②条件值周围使用的是单引号(大部分数据库系统也接受双引号)③如果是数值，不要使用引号
## 数据库
- 数据库表：一个数据库通常包含一个或多个表。每个表由一个名字标识。表包含带有数据的记录（行）。
- 数据库管理系统(DBMS):一种可以访问数据库中数据的计算机程序。不同的 DBMS 提供不同的函数供查询、提交以及修改数据。
- 关系数据库管理系统(RDBMS): 也是一种数据库管理系统，其数据库是根据数据间的关系来组织和访问数据的

## 打开命令窗口
- 开始菜单 --> MySQL 5.6 Command Line Client
- cmd --> mysql -h localhost -P 3306 -u root -proot 或 mysql -u root -proot
## 查询和更新指令：<br><b>
- SELECT - 从数据库表中获取数据<br>①`SELECT 列名称 FROM 表名称`
<br>②`SELECT * FROM 表名称` (星号（*）是选取所有列的快捷方式。)
<br>例:`SELECT LastName,FirstName FROM Persons`从名为 "Persons" 的数据库表,获取名为 "LastName" 和 "FirstName" 的列的内容
<br>③`SELECT DISTINCT 列名称 FROM 表名称` (关键词 DISTINCT 用于返回唯一不同的值。)
<br>④`SELECT 列名称 FROM 表名称 WHERE 列 运算符 值`
<br>例：`SELECT * FROM Persons WHERE City='Beijing'`
⑤AND 和 OR 运算符
<br>例：`SELECT * FROM Persons WHERE (FirstName='Thomas' OR FirstName='William') AND LastName='Carter'`
<br>⑥ORDER BY 语句和DESC 关键字(ORDER BY 语句默认按照升序对记录进行排序,ASC升序，DESC则按照降序排序)
<br>例：`SELECT Company, OrderNumber FROM Orders ORDER BY Company DESC, OrderNumber ASC`
 
- UPDATE - 更新数据库表中的数据
<br>`UPDATE 表名称 SET 列名称 = 新值 WHERE 列名称 = 某值`
<br>例：`UPDATE Person SET Address = 'Zhongshan 23', City = 'Nanjing' WHERE LastName = 'Wilson'`(在Lastname为Wilson的Address列中更新为Zhongshan 23，City列中更新为Nanjing)

- DELETE - 从数据库表中删除数据
<br>①`DELETE FROM 表名称 WHERE 列名称 = 值`
例：`DELETE FROM Person WHERE LastName = 'Wilson' `
<br>②`DELETE FROM table_name` 或者 `DELETE * FROM table_name`

- INSERT INTO - 向数据库表中插入数据
<br>①`INSERT INTO table_name (列1, 列2,...) VALUES (值1, 值2,....)`
<br>②`INSERT INTO 表名称 VALUES (值1, 值2,....)`
<br>例：`INSERT INTO Persons (LastName, Address) VALUES ('Wilson', 'Champs-Elysees')`在Lastname列添加Wilson，在Addresss列添加Champs-Elysees
## 符号/关键字
- 操作符
  - <>或者!= :不等于
  - BETWEEN：在 WHERE 子句中使用，作用是选取介于两个值之间的数据范围
<br>例：`SELECT * FROM Persons
WHERE LastName
BETWEEN 'Adams' AND 'Carter'`以字母顺序显示介于 "Adams"（包括）和 "Carter"（不包括）之间的
  - LIKE：用于在 WHERE 子句中搜索列中的指定模式
<br>例：`SELECT column_name(s)
FROM table_name
WHERE column_name LIKE 'pattern'`
  - IN：允许在 WHERE 子句中规定多个值
<br>例：`- SELECT * FROM Persons
WHERE LastName IN ('Adams','Carter')`选取姓氏为 Adams 和 Carter 的人
  - UNION：用于合并两个或多个 SELECT 语句的结果集
</b><br>要求：UNION 内部的 SELECT 语句必须拥有相同数量的列。列也必须拥有相似的数据类型。同时，每条 SELECT 语句中的列的顺序必须相同。
<br></b>ps：UNION 结果集中的列名总是等于 UNION 中第一个 SELECT 语句中的列名<b>
  - UNION ALL：UNION 命令只会选取不同的值，而UNION ALL会列出所有的值
  - IS NULL 和 IS NOT NULL
<br>例：`SELECT LastName,FirstName,Address FROM Persons
WHERE Address IS NULL`选取地址为空值的数据

- 通配符
  - `"%"` 可用于定义通配符（模式中缺少的一个或多个字符字母）
<br>- 'N%'：以 "N" 开始的
<br>- '%g'：以 "g" 结尾的
<br>- '%lon%'：包含"lon"的
  - `"_"`：仅替代一个字符
<br>例：` SELECT * FROM Persons
WHERE LastName LIKE 'C_r_er'`
  - `"[charlist]"`：字符列中的任何单一字符
<br>例：`SELECT * FROM Persons
WHERE City LIKE '[ALN]%'`选取居住的城市以 "A" 或 "L" 或 "N" 开头的
  - `"[^charlist]或者[!charlist]"`：不在字符列中的任何单一字符
<br>例：`SELECT * FROM Persons
WHERE City LIKE '[!ALN]%'`选取居住的城市不以 "A" 或 "L" 或 "N" 开头的

-  NOT 关键字：否定


## MySQL 数据类型
### Text 类型：
- CHAR(size)：保存固定长度的字符串（可包含字母、数字以及特殊字符）。在括号中指定字符串的长度。最多 255 个字符。
- VARCHAR(size)：保存可变长度的字符串（可包含字母、数字以及特殊字符）。在括号中指定字符串的最大长度。最多 255 个字符。
<br>(注释：如果值的长度大于 255，则被转换为 TEXT 类型)
- TINYTEXT：存放最大长度为 255 个字符的字符串。
- TEXT：存放最大长度为 65,535 个字符的字符串。
- BLOB：用于 BLOBs (Binary Large OBjects)。存放最多 65,535 字节的数据。
- MEDIUMTEXT：存放最大长度为 16,777,215 个字符的字符串。
- MEDIUMBLOB：用于 BLOBs (Binary Large OBjects)。存放最多 16,777,215 字节的数据。
- LONGTEXT：存放最大长度为 4,294,967,295 个字符的字符串。
- LONGBLOB：用于 BLOBs (Binary Large OBjects)。存放最多 4,294,967,295 字节的数据。
- ENUM(x,y,z,etc.)：允许你输入可能值的列表。可以在 ENUM 列表中列出最大 65535 个值。如果列表中不存在插入的值，则插入空值。
可以按照此格式输入可能的值：ENUM('X','Y','Z')<br>(注释：这些值是按照你输入的顺序存储的)
- SET:与 ENUM 类似，SET 最多只能包含 64 个列表项，不过 SET 可存储一个以上

### Number 类型：
- TINYINT(size)：-128 到 127 常规。0 到 255 无符号*。在括号中规定最大位数。
- SMALLINT(size)：-32768 到 32767 常规。0 到 65535 无符号*。在括号中规定最大位数。
- MEDIUMINT(size)：-8388608 到 8388607 普通。0 to 16777215 无符号*。在括号中规定最大位数。
- INT(size)：-2147483648 到 2147483647 常规。0 到 4294967295 无符号*。在括号中规定最大位数。
- BIGINT(size)：-9223372036854775808 到 9223372036854775807 常规。0 到 18446744073709551615 无符号*。在括号中规定最大位数。
- FLOAT(size,d)：带有浮动小数点的小数字。在括号中规定最大位数。在 d 参数中规定小数点右侧的最大位数。
- DOUBLE(size,d)：带有浮动小数点的大数字。在括号中规定最大位数。在 d 参数中规定小数点右侧的最大位数。
- DECIMAL(size,d)：作为字符串存储的 DOUBLE 类型，允许固定的小数点。
### Date 类型：
- DATE()：日期。格式：YYYY-MM-DD
注释：支持的范围是从 '1000-01-01' 到 '9999-12-31'
- DATETIME()：*日期和时间的组合。格式：YYYY-MM-DD HH:MM:SS
<br>(注释：支持的范围是从 '1000-01-01 00:00:00' 到 '9999-12-31 23:59:59')
- TIMESTAMP()：*时间戳。TIMESTAMP 值使用 Unix 纪元('1970-01-01 00:00:00' UTC) 至今的描述来存储。格式：YYYY-MM-DD HH:MM:SS
<br>(注释：支持的范围是从 '1970-01-01 00:00:01' UTC 到 '2038-01-09 03:14:07' UTC)
- TIME():时间。格式：HH:MM:SS 
<br>(注释：支持的范围是从 '-838:59:59' 到 '838:59:59')
- YEAR():2 位或 4 位格式的年。
<br>(注释：4 位格式所允许的值：1901 到 2155。2 位格式所允许的值：70 到 69，表示从 1970 到 2069。)

## DDL语句
  SQL 的数据定义语言 (DDL) 部分使我们有能力创建或删除表格。我们也可以定义索引（键），规定表之间的链接，以及施加表间的约束。

- CREATE DATABASE ：创建新数据库
- ALTER DATABASE ：修改数据库
- CREATE TABLE ：创建新表
<br>例：`CREATE TABLE 表名称
(
列名称1 数据类型,
列名称2 数据类型,
列名称3 数据类型,
....
)`
- ALTER TABLE：变更（改变）数据库表
<br>例：`ALTER TABLE table_name
ADD/DROP column_name datatype` 在表中添加/删除列
<br>例：`ALTER TABLE table_name
ALTER COLUMN column_name datatype` 改变表中列的数据类型
- CREATE INDEX：用于在表中创建索引，用户无法看到索引(搜索键)
<br>例：`CREATE UNIQUE INDEX PersonIndex
ON Person (LastName) `：创建唯一索引
<br>例：`CREATE INDEX PersonIndex
ON Person (LastName DESC) `：以降序索引
<br>例：`CREATE INDEX PersonIndex
ON Person (LastName, FirstName)`：创建多个索引
- DROP：删除索引、表和数据库
<br>例：` DROP TABLE 表名称/DATABASE 数据库名称`
<br>例：`ALTER TABLE table_name DROP INDEX index_name`


## 其他
- TOP：用于规定要返回的记录的数目
<br>例：`SELECT TOP number|percent column_name(s)FROM table_name`:返回头几行|前百分之几行的数据
<br>例：`SELECT TOP 50 PERCENT * FROM Persons` OR `SELECT TOP 2 * FROM Persons`
- Alias：使用别名
 - 表别名：SELECT column_name(s) FROM table_name AS alias_name
 - 列别名：SELECT column_name AS alias_name FROM table_name
<br>例：`SELECT po.OrderID, p.LastName, p.FirstName
FROM Persons AS p, Product_Orders AS po
WHERE p.LastName='Adams' AND p.FirstName='John'`将表"Persons" 和 "Product_Orders"分别指定别名为"p" 和 "po"，并列出"John Adams"的相关数据
- JOIN：用于根据两个或多个表中的列之间的关系，从这些表中查询数据
 - INNER JOIN: 如果表中有至少一个匹配，则返回行
<br>例：`SELECT Persons.LastName, Persons.FirstName, Orders.OrderNo
FROM Persons
INNER JOIN Orders
ON Persons.Id_P = Orders.Id_P`
 - LEFT JOIN: 即使右表中没有匹配，也从左表返回所有的行(以左表选取的列为准，加入右表选出的列)
 - RIGHT JOIN: 即使左表中没有匹配，也从右表返回所有的行(以右表选取的列为准加入左表选出的列)
 - FULL JOIN: 只要其中一个表中存在匹配，就返回行(相当于LEFT JOIN和RIGHT JOIN的合并结果)
- SELECT INTO：语句可用于创建表的备份复件
<br>例：`SELECT Persons.LastName,Orders.OrderNo
INTO Persons_Order_Backup
FROM Persons
INNER JOIN Orders
ON Persons.Id_P=Orders.Id_P`
(`从persons与orders连接的表中选出Id_P相同的人的LastName和OrderNo放入Persons_Order_Backup表中`)
<br>例：`SELECT LastName,Firstname
INTO Persons_backup
FROM Persons
WHERE City='Beijing'`
(`从persons表中选出住在北京的人的LastName和FirstName放入Persons_backup`)
- TRUNCATE:仅仅删除表格中的数据
<br>例：TRUNCATE TABLE 表名称
- AUTO INCREMENT 字段：会在新记录插入表中时生成一个唯一的数字
<br>例：`CREATE TABLE Persons
(
P_Id int NOT NULL AUTO_INCREMENT,
LastName varchar(255) NOT NULL,
PRIMARY KEY (P_Id)
)`
<br>例：`ALTER TABLE Persons AUTO_INCREMENT=100`让 AUTO_INCREMENT 序列以100起始(默认地，AUTO_INCREMENT 的开始值是 1，每条新记录递增 1。)
- 视图
<br>视图是基于 SQL 语句的结果集的可视化的表。
视图包含行和列，就像一个真实的表。视图中的字段就是来自一个或多个数据库中的真实的表中的字段。我们可以向视图添加 SQL 函数、WHERE 以及 JOIN 语句，我们也可以提交数据，就像这些来自于某个单一的表。


## 约束 (Constraints）
 - NOT NULL：强制列不接受 NULL 值。这意味着，如果不向字段添加值，就无法插入新记录或者更新记录。
 - UNIQUE：唯一标识数据库表中的每条记录
<br>例：` CREATE TABLE Persons
(
Id_P int NOT NULL,
LastName varchar(255) NOT NULL,
FirstName varchar(255),
Address varchar(255),
City varchar(255),
CONSTRAINT uc_PersonID UNIQUE (Id_P,LastName)
)`创建表时为 UNIQUE 约束命名，并为多个列定义 UNIQUE 约束
<br>例：`ALTER TABLE Persons
ADD CONSTRAINT uc_PersonID UNIQUE (Id_P,LastName)`
<br>例：`ALTER TABLE Persons
DROP INDEX uc_PersonID 或 ALTER TABLE Persons
DROP CONSTRAINT uc_PersonID`撤销 UNIQUE 约束
 - PRIMARY KEY：唯一标识数据库表中的每条记录。主键必须包含唯一且不为空的值。每个表都应该有且只有一个主键。
 <br>（UNIQUE 和 PRIMARY KEY 约束语法相似，均为列或列集合提供了唯一性的保证。
PRIMARY KEY 拥有自动定义的 UNIQUE 约束。每个表可以有多个 UNIQUE 约束，但是每个表只能有一个 PRIMARY KE）
 - FOREIGN KEY：一个表中的 FOREIGN KEY 指向另一个表中的 PRIMARY KEY。FOREIGN KEY 约束用于预防破坏表之间连接的动作，还能防止非法数据插入外键列，因为它必须是它指向的那个表中的值之一。
 例：`CREATE TABLE Orders
(
Id_O int NOT NULL,
OrderNo int NOT NULL,
Id_P int,
PRIMARY KEY (Id_O),
FOREIGN KEY (Id_P) REFERENCES Persons(Id_P)
)`
<br>例：`CREATE TABLE Orders
(
Id_O int NOT NULL,
OrderNo int NOT NULL,
Id_P int,
PRIMARY KEY (Id_O),
CONSTRAINT fk_PerOrders FOREIGN KEY (Id_P)
REFERENCES Persons(Id_P)
)`命名约束以及定义多列约束
 - CHECK：用于限制列中的值的范围
例：`CREATE TABLE Persons
(
Id_P int NOT NULL,
LastName varchar(255) NOT NULL,
FirstName varchar(255),
Address varchar(255),
City varchar(255),
CONSTRAINT chk_Person CHECK (Id_P>0 AND City='Sandnes')
)`
 - DEFAULT：用于向列中插入默认值
 例：`CREATE TABLE Persons
(
Id_P int NOT NULL,
LastName varchar(255) NOT NULL,
FirstName varchar(255),
Address varchar(255),
City varchar(255) DEFAULT 'Sandnes'
)`(还可以通过使用类似 GETDATE() 这样的函数，DEFAULT 约束也可以用于插入系统值)
<br>例：`ALTER TABLE Persons
ALTER City SET DEFAULT 'SANDNES'`
<br>例：`ALTER TABLE Persons
ALTER City DROP DEFAULT`撤销

## 函数
-  Date 函数
 - GETDATE()：返回当前日期和时间
 - DATEPART()：返回日期/时间的单独部分
 - DATEADD()：在日期中添加或减去指定的时间间隔
 - DATEDIFF()：返回两个日期之间的时间
 - CONVERT()：用不同的格式显示日期/时间
 -  Date 数据类型:
<br>DATE - 格式:YYYY-MM-DD
<br>DATETIME - 格式: YYYY-MM-DD HH:MM:SS
<br>TIMESTAMP - 格式: YYYY-MM-DD HH:MM:SS
<br>YEAR - 格式：YYYY 或 YY
-  ISNULL()、NVL()、IFNULL() 和 COALESCE() 函数(相同作用用于不同数据库)：用于规定如何处理 NULL 值，将NULL值返回0便于计算


