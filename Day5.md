# SQL
SQL (结构化查询语言)是用于执行查询的语法。但是 SQL 语言也包含用于更新、插入和删除记录的语法。
可以把 SQL 分为两个部分：数据操作语言 (DML) 和 数据定义语言 (DDL)。
<br>tips:①sql对大小写不敏感②条件值周围使用的是单引号(大部分数据库系统也接受双引号)③如果是数值，不要使用引号
## 数据库表
一个数据库通常包含一个或多个表。每个表由一个名字标识。表包含带有数据的记录（行）。

## DML
#### 查询和更新指令构成了 SQL 的 DML 部分：<br>
- SELECT - 从数据库表中获取数据<br>①`SELECT 列名称 FROM 表名称`
<br>②`SELECT * FROM 表名称` (星号（*）是选取所有列的快捷方式。)
<br>例:`SELECT LastName,FirstName FROM Persons`从名为 "Persons" 的数据库表,获取名为 "LastName" 和 "FirstName" 的列的内容
<br>③`SELECT DISTINCT 列名称 FROM 表名称` (关键词 DISTINCT 用于返回唯一不同的值。)
<br>④`SELECT 列名称 FROM 表名称 WHERE 列 运算符 值`
<br>例：`SELECT * FROM Persons WHERE City='Beijing'`
⑤AND 和 OR 运算符
<br>例：`SELECT * FROM Persons WHERE (FirstName='Thomas' OR FirstName='William') AND LastName='Carter'`
⑥ORDER BY 语句和DESC 关键字
 <br>  - ORDER BY 语句默认按照升序对记录进行排序,ASC升序，DESC则按照降序排序
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
- 操作符
<br><>或者!= :不等于
<br>BETWEEN：在某个范围内
<br>LIKE：搜索某种模式

## DDL
SQL 的数据定义语言 (DDL) 部分使我们有能力创建或删除表格。我们也可以定义索引（键），规定表之间的链接，以及施加表间的约束。
#### SQL 中最重要的 DDL 语句:
- CREATE DATABASE - 创建新数据库
- ALTER DATABASE - 修改数据库
- CREATE TABLE - 创建新表
- ALTER TABLE - 变更（改变）数据库表
- DROP TABLE - 删除表
- CREATE INDEX - 创建索引（搜索键）
- DROP INDEX - 删除索引

