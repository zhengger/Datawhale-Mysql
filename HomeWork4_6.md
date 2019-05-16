## 项目三：超过5名学生的课（难度：简单）
//登陆
MyMac:bin zheng$ mysql -u root -p

//创建如下所示的courses 表 ，有: student (学生) 和 class (课程)。

mysql> create table courses(
    -> student varchar(40) not null,
    -> class varchar(40) not null,
    -> id int not null,
    -> primary key(id)
    -> ) charset=utf8;
Query OK, 0 rows affected, 1 warning (0.12 sec)

mysql> insert into courses(student, class, id) values ('A', 'Math', 1);
Query OK, 1 row affected (0.00 sec)

mysql> insert into courses(student, class, id) values ('B', 'ENGLISH', 2);
Query OK, 1 row affected (0.02 sec)

mysql> insert into courses(student, class, id) values ('C', 'Math', 3);
Query OK, 1 row affected (0.00 sec)

mysql> insert into courses(student, class, id) values ('D', 'Biology', 4);
Query OK, 1 row affected (0.00 sec)

mysql> insert into courses(student, class, id) values ('E', 'Math', 5);
Query OK, 1 row affected (0.01 sec)

mysql> insert into courses(student, class, id) values ('F', 'Computer', 6);
Query OK, 1 row affected (0.01 sec)

mysql> insert into courses(student, class, id) values ('G', 'Math', 7);
Query OK, 1 row affected (0.00 sec)

mysql> insert into courses(student, class, id) values ('H', 'Computer', 8);
Query OK, 1 row affected (0.01 sec)

mysql> insert into courses(student, class, id) values ('I', 'Math', 9);
Query OK, 1 row affected (0.10 sec)

mysql> insert into courses(student, class, id) values ('J', 'Math', 10);

mysql> select * from courses;
+---------+----------+----+
| student | class    | id |
+---------+----------+----+
| A       | Math     |  1 |
| B       | ENGLISH  |  2 |
| C       | Math     |  3 |
| D       | Biology  |  4 |
| E       | Math     |  5 |
| F       | Computer |  6 |
| G       | Math     |  7 |
| H       | Computer |  8 |
| I       | Math     |  9 |
| J       | Math     | 10 |
+---------+----------+----+
10 rows in set (0.00 sec)


//编写一个 SQL 查询，列出所有超过或等于5名学生的课。
mysql> select class, count(*) from courses group by class having count(*)>5;
+-------+----------+
| class | count(*) |
+-------+----------+
| Math  |        6 |
+-------+----------+
1 row in set (0.01 sec)



## 项目四：交换工资（难度：简单）

mysql> create table salary(
    -> id INT not null,
    -> name varchar(40) not null,
    -> sex varchar(20) not null,
    -> salary int not null
    -> ) charset=utf8;
Query OK, 0 rows affected, 1 warning (0.12 sec)

mysql> select * from salary;
Empty set (0.00 sec)

mysql> insert into salary values (1, 'A', 'm', 2500 ), (2, 'B', 'f', 1500), (3, 'C', 'f', 5500), (4, 'D', 'f', 500), (5, 'E', 'm', 1000);
Query OK, 5 rows affected (0.00 sec)
Records: 5  Duplicates: 0  Warnings: 0

mysql> select * from salary;
+----+------+-----+--------+
| id | name | sex | salary |
+----+------+-----+--------+
|  1 | A    | m   |   2500 |
|  2 | B    | f   |   1500 |
|  3 | C    | f   |   5500 |
|  4 | D    | f   |    500 |
|  5 | E    | m   |   1000 |
+----+------+-----+--------+
5 rows in set (0.00 sec)

mysql> update salary set sex=if(sex='f', 'm', 'f');
Query OK, 5 rows affected (0.01 sec)
Rows matched: 5  Changed: 5  Warnings: 0

mysql> select * from salary;
+----+------+-----+--------+
| id | name | sex | salary |
+----+------+-----+--------+
|  1 | A    | f   |   2500 |
|  2 | B    | m   |   1500 |
|  3 | C    | m   |   5500 |
|  4 | D    | m   |    500 |
|  5 | E    | f   |   1000 |
+----+------+-----+--------+
5 rows in set (0.00 sec)


## 项目五：组合两张表 （难度：简单）

mysql> insert into person (1, 'Tom', 'Hank'), (2, 'Frank', 'Richard'), (3, 'Tate', 'Sharon');
ERROR 1064 (42000): You have an error in your SQL syntax; check the manual that corresponds to your MySQL server version for the right syntax to use near '1, 'Tom', 'Hank'), (2, 'Frank', 'Richard'), (3, 'Tate', 'Sharon')' at line 1
mysql> insert into person values (1, 'Tom', 'Hank'), (2, 'Frank', 'Richard'), (3, 'Tate', 'Sharon');
Query OK, 3 rows affected (0.01 sec)
Records: 3  Duplicates: 0  Warnings: 0

mysql> select * from person;
+----------+-----------+----------+
| PersonId | FirstName | LastName |
+----------+-----------+----------+
|        1 | Tom       | Hank     |
|        2 | Frank     | Richard  |
|        3 | Tate      | Sharon   |
+----------+-----------+----------+
3 rows in set (0.00 sec)

mysql> create table address(
    -> AddressId int(10) not null,
    -> PersonId int(10) not null,
    -> City varchar(40) not null,
    -> State varchar(40) not null,
    -> primary key(AddressId)
    -> )charset=utf8;
Query OK, 0 rows affected, 1 warning (0.01 sec)

mysql> insert into address (23, 1, 'HK', 'China'), (24, 2, 'WD', 'US'), (25, 3, 'PR', 'France');
ERROR 1064 (42000): You have an error in your SQL syntax; check the manual that corresponds to your MySQL server version for the right syntax to use near '23, 1, 'HK', 'China'), (24, 2, 'WD', 'US'), (25, 3, 'PR', 'France')' at line 1
mysql> insert into address values (23, 1, 'HK', 'China'), (24, 2, 'WD', 'US'), (25, 3, 'PR', 'France');
Query OK, 3 rows affected (0.00 sec)
Records: 3  Duplicates: 0  Warnings: 0

mysql> select * from address;
+-----------+----------+------+--------+
| AddressId | PersonId | City | State  |
+-----------+----------+------+--------+
|        23 |        1 | HK   | China  |
|        24 |        2 | WD   | US     |
|        25 |        3 | PR   | France |
+-----------+----------+------+--------+
3 rows in set (0.00 sec)

mysql> select p.FirstName, p.LastName, a.City, a.State from person p RIGHT JOIN address a on p.PersonId = a.PersonId; 
+-----------+----------+------+--------+
| FirstName | LastName | City | State  |
+-----------+----------+------+--------+
| Tom       | Hank     | HK   | China  |
| Frank     | Richard  | WD   | US     |
| Tate      | Sharon   | PR   | France |
+-----------+----------+------+--------+
3 rows in set (0.00 sec)

mysql> use email;
ERROR 1049 (42000): Unknown database 'email'
mysql> show databases;
+--------------------+
| Database           |
+--------------------+
| 5students          |
| information_schema |
| MyFirstDB          |
| mysql              |
| performance_schema |
| sys                |
| yiibaidb           |
+--------------------+
7 rows in set (0.00 sec)



## 项目六：删除重复的邮箱（难度：简单）

mysql> create table email( id int not null, email varchar(40) not null, primary key(id))charset=utf8;
Query OK, 0 rows affected, 1 warning (0.12 sec)

mysql> insert email values (1, 'a@b.com'), (2, 'c@d.com'), (3, 'a@b.com');
Query OK, 3 rows affected (0.01 sec)
Records: 3  Duplicates: 0  Warnings: 0

mysql> select * from email;
+----+---------+
| id | email   |
+----+---------+
|  1 | a@b.com |
|  2 | c@d.com |
|  3 | a@b.com |
+----+---------+
3 rows in set (0.01 sec)

