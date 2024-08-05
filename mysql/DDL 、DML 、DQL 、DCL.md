DDL：Data Definition Language 定义/改表表的结构

DML : Data manipulation Language 数据操作，增删改

DQL : Data Query Language  数据查询 查询操作

DCL : Data Control Language   数据控制，主要是设置/更改用户权限什么的

每一个来个例子

```sql
DDL 
-- 创建数据库
CREATE DATABASE IF NOT EXISTS mydatabase;
-- 创建数据库表
CREATE TABLE t_user IF NOT EXISTS{
id LONG PRIMARY KEY,
name VARCHAR(50),
address VARCHAR(50),
salary DECIMAL(15,20)     -- 这里decemal(m,d)m是数字的最大位数，d是小数点后面的位数
													-- m是1到65，d是0到30
}
-- 修改表结构
-- 添加列 ADD
ALTER TABLE t_user ADD phone VARCHAR(11)
-- 修改列的类型 MODIFY
ALTER TABLE t_user MODIFY salary DECIMAL(15,15) 【这里可以更改约束】
-- 删除表
DROP TABLE t_user 
-- 删除数据库
DROP DATABASE mydatabase
```

```sql
DML
-- 增
INSERT INTO t_user(name,address) values ("张三","东方明珠")
-- 删
DELETE FROM t_user WHERE id = 1
-- 改
UPDATE t_user SET name = 张四 WHERE address = '东方明珠'
```

```sql
DCL 粗略讲
3个关键字
GRANT  用来授权访问数据库的权限
GRANT permission ON object TO user;  -- object表示授权的数据库对象，可以是表、视图、存储过程等；user表示被授权的用户或用户组。
REVOKE  用来撤销废除访问数据库的权限
REVOKE permission ON object FROM user; 

DENY  用来限制用户或角色对某些数据库对象的访问权限
语法不要求掌握
```

--------------------------------------------------------------------------------------------------------









```sql
DQL【重点】
-- 别名
StudentHomeword as sh  或者 StudentHomeword  sh
SELECT *, salary*12 as "年薪" FROM t_user
-- 去除重复行输出
SELECT DISTINCT 列名,[列名,列名] from XXX    -- 这里多个列就是用来判断是否重复,比如3个列，2行对象，前2列全相同，第3列不同
-- 查询常数，常常在整个表的人都有相同值的情况用
SELECT *,"macbook" as "电脑" from XXX
-- 查询里进行非空判断再进行运算，避免NULL运算
IFNULL(salary,1000)-- 后面是为空时的默认
-- 查看表结构
DESC tablename
```

```sql
-- 条件过滤
<> !=  前面是标准写法，后面是为了迎合
<=>  判断相等，不过可以判断NULL
IS NULL
IS NOT NULL
Between AND  左右都是闭合的
NOT Between AND 
IN () 是否在一组值里
NOT IN ()
LIKE 
NOT LIKE 
```

```sql
sql运算符
%,MOD 取模运算（就是取余数）
+，-，*，/   --注意，在sql语句里面就算【分母是0】，不会报错，会得到 【NULL】
DIV 整除
```

---

###### 模糊查询

```mysql
_ 只能占位一个
% 能占位0或多个
like _ _ a  --a结尾的3个字符
like %a     --a结尾的任意长度的字符
```

----

###### 特殊比较

```sql
(a,b)=(x,y) 等同于  a=x AND b=y
(a,b)<=>(x,y) 等同于 a<=>x AND b<=>y
(a,b)<>(x,y)  等同于 a<>x OR b<>y
```

```
XOR 异或
```

符号优先级

```
取反和取负最高，其他的都能看懂，最后OR AND这些最低
```

###### 分组查询

```sql
SELECT FROM 
WHERE 
GROUP BY 分组字段，聚合函数       --这里一定要逗号
HAVING   #having是分组后的
```

###### 顺序查询

```sql
SELECT FROM 
WHERE 
ORDER BY 排序列 ASC/DESC , 排序列2 ASC/DESC
```

###### 分页查询

```sql
LIMIT 开始的行 偏移量  #必须放最后
```

公式

```sql
(page-1)*size,size
```

