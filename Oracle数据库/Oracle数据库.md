# Oracle数据库

## 数据库的历史

自从有了人类就有了信息，声音、光线、触觉、嗅觉、味觉等等这些五官能感知的东西中都带有信息。运动员听到枪响就起跑，枪响表示起跑的信息；长城上燃起的狼烟是敌人来犯的信息；婴儿在不了解这个世界时，他们用嘴巴来感知这个世界，这些都是生活中的信息。在当今社会中我们经常说的信息化，就是收集有用的信息加以分析和判断用来指导我们的生活和生产，这些信息可能在报纸上、互联网上等等，当这些信息保存在互联网上时，它们就变成了一个个的数据，而这些变为数据的信息就需要管理起来，于是就有了专业管理数据的软件，就是各种信息管理系统，而在这些信息管理系统的底层往往使用是数据库。
在远古时代，人们用结绳记事时，绳结就是信息就是数据，它们的载体是绳子，绳子可以说是最简单的数据库了。后来人们有了纸和笔时，纸就是数据库了，有了计算机后，人们把数据储存到文件中，文件成了数据库，直到后来有了专业的软件来管理这些文件中的数据，这些软件就是数据库软件，而安装这些软件的计算机就成了数据库服务器。我们有时说的数据库可能是指保存数据的这些文件，也可能是指管理这些数据的软件，也可能是指服务器，具体要看语境。总之，数据是信息的载体，数据库是数据的仓库，数据库软件是管理数据仓库的软件，安装了数据库软件的计算机就是数据库服务器。这里有几个单词和它们对应，data,database,databaseSoft,databaseService
数据库有多种数据模型，不同的模型中数据的结构和操作数据的方法都不相同，不同的数据库软件会采用其中一种数据模型。目前用的比较多的数据模型有关系数据模型和非关系型数据模型，它们的代表是：Oracle、MySQL、SQLServer使用关系数据模型，H2、Redis、MongoDB等NoSQL数据模型，以键值对形式、文档形式或其它对象形式储存数据。

## 关系型数据库

1970年E.F.Codd’s发表了论文 <<relational model of data for large shared data banks>>大型共享型数据库的关系模型，为关系型数据库提供了基础理论，为关系型数据库的诞生创造了条件。
关系模型中主要有关系模式和关系两个概念，关系就是关系模式在某一时刻的状态或内容，关系模式是静态的稳定的，关系是动态的，随着时间变化而变化的，因为关系操作在不断的更新着数据库中的数据。
在关系型数据库出现前有网状数据库和层次数据库，用户在操作数据前要明确指定数据的位置和路径，需要明确数据的结构。关系型数据库中，用户操作数据时是非过程化的，不需要指定路径，由DBMS自己优化完成（Database Management System）
关系模型中无论是实体还是实体间的联系均由单一的结构类型——关系来表示。在实际的关系数据库中的关系也称表。一个关系数据库就是由若干个表组成。现在给关系模型下一个定义：关系模型是指用二维表的形式表示实体和实体间联系的数据模型。

## 几个概念

实体：现实中的具体事物或关系，如：学校、院系、学生、成绩信息、选课表信息。
表： 实体在数据库中的表现，由一条条记录组成。
行： 表格中的一条记录。
列： 组成行的一个属性。
主键：能唯一区分表中的某一行。
外键：其它表的主键在当前表中的列。

**school表：学校实体对应的表**

| 编号 | 名称     | 地址                    |
| ---- | -------- | ----------------------- |
| 1    | 北京大学 | 北京市海淀区颐和园路5号 |
| 2    | 清华大学 | 北京市海淀区双清路30号  |

编号是其中一个列
编号能唯一确定一行

**student表：学生实体对应的表**


| 编号 | 学号 | 姓名 | 年龄 | 班级 |
| ---- | ---- | ---- | ---- | ---- |
| 1    | 2001 | 赵一 | 18   | 202001|
| 2    | 2002 | 钱二 | 18   |202001 |
| 3    | 2003 | 孙三 | 18   |202002 |

编号是表的主键，能唯一确定一条记录，学号列也可以，学号可以是表中的候选主键

**course 课程表**

| 编号 | 名称   |
| ---- | ------ |
| 1    | Java   |
| 2    | C      |
| 3    | Oracle |

**score成绩表**

| 学生编号 | 课程编号 | 成绩 |
| -------- | -------- | -------- |
| 1        | 1        | 100  |
| 1        | 2        | 90   |
| 1        | 3        | 88   |
| 2        | 1        | 90   |
| 2        | 2        | 90   |
| 2        | 3        | 95   |

成绩表中学生编号和课程编号共同作为主键（联合主键）

**clazz 班级表**

| 编号   | 名称     |
| ------ | -------- |
| 202001 | 软件一班 |
| 202002 | 软件二班 |

编号在clazz表中是主键，在student表中班级列是student表的外键

## 三范式

数据在数据库中会占用大量空间，为了节省空间，同时也为了让数据更安全更合理，在设计表时要用三范式来规范一下。
为了简单理解一下三范式，记住以下几点，这在考试中是非常有用的。
一范式：字段不可再拆分
二范式：表中要有主键
三范式：表中不能用别的表的非主键
以上的描述是简要描述，按照一些教材的描述是比较复杂的，下面来详细介绍一下各个范式。
一范式（1NF）：字段不可拆分
这个比较好理解，比如下表中：
student

| 编号 | 姓名       | 联系方式                        |
| ---- | ---------- | ------------------------------- |
| 1    | 常熟阿庆嫂 | 2826109xx，17788990011，leadxxx |

上面的表不符合1NF，姓名列中的常熟阿庆嫂有两个信息，一个是地名常熟，一个是姓名阿庆嫂
联系方式列中，分别有QQ号，手机号，微信号，所以这个表可以设计成这样
student

| 编号 | 姓名   | 地址 | QQ        | 电话        | 微信    |
| ---- | ------ | ---- | --------- | ----------- | ------- |
| 1    | 阿庆嫂 | 常熟 | 2826109xx | 17788990011 | leadxxx |

这样设计就符合一范式，因为每个列都不能再拆分了。
再来看一下第二范式：表中要有主键
表中要有主键，是为了让主键能唯一确定一条记录，如果表中的记录有重复
或者没有重复，但没有主键信息也不行，当然要符合二范式，首先要符合一范式

| 姓名 | 地址 | 性别 | 年龄 |
| ---- | ---- | ---- | ---- |
| 小红 | 下元 | 女   | 10   |
| 小红 | 下元 | 女   | 20   |
| 小明 | 小店 | 男   | 8    |
| 小明 | 小店 | 男   | 8    |

以上的记录中有两个问题：1.小红的两条记录虽然没有重复，但是也没有主键，
就算是设置主键也是“姓名+地址+性别+年龄”共同组成主键，这样才能保证没有
重复记录。2.小明的那两条记录重复了，但现实中可能是两个人，只是信息巧合了
。所以要对该表进行整改，给这个表加一个“编号”列作为主键。

| 编号 | 姓名 | 地址 | 性别 | 年龄 |
| ---- | ---- | ---- | ---- | ---- |
| 1    | 小红 | 下元 | 女   | 10   |
| 2    | 小红 | 下元 | 女   | 20   |
| 3    | 小明 | 小店 | 男   | 8    |
| 4    | 小明 | 小店 | 男   | 8    |

这样增加“编号”列，作为主键，就满足了第二范式。
再来看一下第三范式：表中不能有别的表的非主键列
这句话在一些资料中讲的是：

> 第三范式(Third Normal Form,3rd NF)就是指表中的所有数据元素不但要能唯一地被主关键字所标识,而且它们之间还必须相互独立,不存在其他的函数关系。也就是说，对于一个满足2nd NF 的数据结构来说，表中有可能存在某些数据元素依赖于其他非关键字数据元素的现象,必须消除。

这样的描述可能不太好理解，其实就是别的表中的字段只允许它们的主键出现在当前表中，其它字段不能出现，如下表：

| 编号 | 姓名 | 性别 | 班级编号 | 班级名称 |
| ---- | ---- | ---- | -------- | -------- |
| 1    | 赵一 | 女   | 202001   | 软件一班 |
| 2    | 钱二 | 男   | 202001   | 软件一班 |

这个表当然是满足了一、二范式，但是不满足三范式，存在两个问题：1.“班级名称”这一列没有必要出现，因为会造成数据冗余，浪费了空间，只要有“班级编号”就能确定是哪个班了。2.如果在“班级”表中修改了班级名称“软件一班”改为“软件工程一班”后，还要修改上面这个表中的“班级名称”的这一列，造成性能低下，如果要是这个表中有上亿条记录的话，修改也会花费一定的时间。但是，如果不修改这个表，会造成“202001”这个班的名称在系统中不统一，造成数据不一致，这对一个系统来说是不允许的。
出现上述原因是因为表中出现了“班级”表不是主键的“班级名称”这一列，把这一列去掉就可以了，另外，“班级编号”在班级表中是主键，在当前表中就应该是外键了。外键的好处是：如果依赖的表中没有相应的主键记录，则当前表就无法添加记录，这就是外键依赖，当然要删除依赖表中的记录时，如果记录有被依赖的情况，则要么报错不能删除，要么级联删除当前表中的记录，保证了数据的安全，避免了依赖不存在的问题。
班级表

| 编号（PK） | 名称     |
| ---------- | -------- |
| 202001     | 软件一班 |

学生表

| 编号（PK) | 名称 | 班级编号（FK） |
| --------- | ---- | -------------- |
| 1         | 赵一 | 202001         |
| 2         | 钱二 | 202002         |

上面的班级表中不存在记录“202002”这个班级，所以“2，钱二，202002”是无法保存的。如果“学生”表中的外键“班级编号”列设置了外键级联删除，则删除班级表中的“202001”记录时，会级联删除“学生”表中的所有“班级编号”是202001的记录。但是，如果外键列设置的不是级联删除，则删除班级表中的记录“202001”时，数据库会报错。
三范式也不只有三种范式，其实还有巴斯-科德范式(BCNF)、第四范式(4NF)和第五范式(5NF,又称完美范式)，我们知道范式是为了解决数据冗余的问题，但是范式太高的话，又会影响数据查询的性能，所以，一般做到三范式就可以了。

## 数据库的约束

数据库的约束主要是为了保证数据的有效性，从而保证了数据的安全性。约束有以下几点：

- 主键约束
- 唯一约束
- 默认约束
- 检查约束
- 外键约束
  主键约束：保证数据的唯一性，并且主键列数据不能为空。
  唯一约束：保证数据的唯一性，唯一约束的列可以为空。表中有些列不是主键，但也是每条记录唯一的，比如学生表中的学
  号不重复，但是因为数据库设计时建议用非业务性列作主键，所以一般会用一个id作主键。
  默认约束：保证数据的完整性，如果没有填入信息时，会使用默认信息填入，保证数据的完整性。
  检查约束：保证数据的有效性，让值在有效范围内取值，如：性别[0,1]，年龄[1-60]等。
  外键约束：保证数据的完整性，互相依赖的数据不能缺失。比如学生依赖班级表，班级表数据删除后，学生记录就没有了班
  级信息。

## DBA常用操作

### 管理员登录

sqlplus / as sysdba
这样登录是管理员登录，免密码，拥有最高权限，它采用的是操作系统的验证，所以只要能正常登录操作系统，就可以用这个命令登录Oracle数据库。但是，有时候我们登录操作系统的用户因为权限原因不能这样登录数据库，就要解决操作系统用户权限的问题。找到Oracle的安装目录，如：F:\app\DELL\product\11.2.0\dbhome_1\database这个目录下的一个文件oradba.exe，在文件上右键选择以管理员身份运行即可解决权限不足的问题。

### 创建用户

create user user1 identified by user1;
user1是用户名，identified by user1是指定密码。
如果建错用户怎么办？可以删除
drop user user1;
如果user1下已经有用户新建的对象，这样删除会失败，要加一个参数
drop user user1 cascade;
删除用户级联删除其下的对象

### 权限设置

刚创建的用户没有任何权限，不能登录，不能操作数据库，权限可以是单独的权限，具体的权限，也可以角色，角色是若干权限的集合，Oracle有自带的权限，connect/resource/dba，如果需要定制权限集合，我们可以自定义角色，让角色拥有自己的权限。
grant connect to user1;
给user1指定connect的角色（可以登录，访问别人的表进行select/insert/update/delete，可以创建表、视图、序列、同义词、会话等)
grant resource to user1
resource可以创建数据库对象，但是没有登录权限，不能创建会话。
grant dba to user1;
dba权限是最高的
回收权限：
revoke dba from user1;

### 导入导出

## SQL

SQL是数据库比较重要的知识，可以分为：

### DDL

所有的对数据库对象的操作语句
create database , alter database , create table ,alter table drop table,create index等

#### 表空间

保证用户有创建表空间的权限：grant create tablespace to user1;
create tablespace tabsp1 datafile ‘data1.dbf’ size 1m;
执行完这条SQL，在数据库目录下创建一个data1.dbf文件
F:\app\DELL\product\11.2.0\dbhome_1\database\DATA1.DBF
如果表空间满了可以扩容，扩容表空间文件需要用户有相应的权限：
grant alter database to user1;（用sys用户登录分配权限）
alter database datafile ‘data1.dbf’ resize 2m; 可以观察data1.dbf已经变大了
以上是一种方法，还可以用下面的方法修改表空间：
grant alter tablespace to user1;先保证用户有相应权限
alter tablespace tabsp1 add datafile ‘data2.dbf’ size 1m;增加一个数据文件给表空间
以上是正常数据表空间，还可以创建临时表空间，正常数据存放正常数据表空间，临时表空间供数据库存放临时数据用。Oracle临时表空间主要用来做查询和存放一些缓冲区数据。临时表空间消耗的主要原因是需要对查询的中间结果进行排序。
create temporary tablespace tmpsp1 tempfile ‘tmp1.dbf’ size 2m;创建表空间语句
创建用户时指定表空间，如果没有指定表空间时，创建的用户使用的是系统表空间，不建议使用系统表空间，如果用户使用自己的表空间时，可以在删除用户时把表空间也删除，这样比较彻底。当然，可以多个用户共用一个表空间，这个另当别论。
create user user2 identified by user2 default tablespace tabsp1 temporary tablespace tmpsp1;
以上语句是创建user2用户指定密码和默认表空间临时表空间。

删除表空间：

```sql
--删除空的表空间，但是不包含物理文件
drop tablespace tablespace_name;
--删除空表空间，包含物理文件
drop tablespace tablespace_name including datafiles;
--删除非空表空间，但是不包含物理文件
drop tablespace tablespace_name including contents;
--删除非空表空间，包含物理文件
drop tablespace tablespace_name including contents and datafiles;
--如果其他表空间中的表有外键等约束关联到了本表空间中的表的字段，就要加上CASCADE CONSTRAINTS
drop tablespace tablespace_name including contents and datafiles CASCADE CONSTRAINTS;
12345678910
```

#### 表

建表前要先了解Oracle的数据类型，因为要为列指定合适的数据类型，数据类型有以下几种：

| 类型      | 说明                                                         |
| --------- | ------------------------------------------------------------ |
| number    | 数字类型                                                     |
| char      | 定长字符型                                                   |
| varchar   | 变长字符型，最大4000                                         |
| date      | 日期类型                                                     |
| TIMESTAMP | 时间戳（可精确到毫秒）                                       |
| blob      | 二进制数据（Binary Large Object)保存音视频4G                 |
| clob      | 字符型数据（Character Large Object）保存文档，支持定长和变长字符集 |
| bfile     | 二进制文件（文件在数据库外的磁盘上）                         |

char和varchar：
关于varchar长度的说明，varchar和char的区别是char长度是固定的，内容不够列的宽度也会占用列的宽度，比如一个字段是char型，长度是20，username char(20),则无论username内容是多少，都会占用20个固定的宽度，就算username是一个字符也是如此，如果某些列的数据长度是比较固定某个长度的，则最好使用此类型。varchar的长度是变化的，如果实际数据内容不足列的宽度则只占用合适的空间来存放数据，会大大地节省数据库空间。但是，varchar更适合列比较大的，如果varchar(2)这样列比较小的就没有意义了，它反而还要花费额外的空间来记录该列的数据实际长度，数据库在处理varchar列时要进行额外的计算处理，并存储数据的实际长度，在效率上不如char性能高。
varchar最大4000。这个4000可能是4000字节也可能是4000字符，取决于参数NLS_LENGTH_SEMANTICS的设置，这个参数有两个选项，BYPE，CHAR，如果是BYTE则是4000字节，可以放4000个英文和数字，但汉字或其他字符就不一定了，肯定的是只会小于4000，如果是汉字占三个字节，则能放4000/3个字符。
alter session set NLS_LENGTH_SEMANTICS=‘CHAR’;可以修改这个参数 =‘CHAR’ 或 =‘BYTE’
number类型：
number可以指定精度，如果没有指定默认的是38位。number(5)是一个5位数据的整数，number(5,2)是一个总长为5位，小数位为2位，整数位是3位，如：123.23，123.2也可以，123.2345也可以，因为小数位会自动四舍五入为123.23，但是整数位不能随意写，如1234.1虽然整体长度是5位数字，但是除去小数位规定的2位，整数位只能是3位数，1234超出3位，所以是不符合规范的。number(5,-2)也是可以的，如果第2个参数是负数，则没有小数，并且整数位的后2位会忽略，数字的整体长度为第一个参数减去第二个参数5-(-2)=7，1234567是可以的。

| 列           | 结果                                           |
| ------------ | ---------------------------------------------- |
| number(1,1)  | 错误:1，2 正确0.1，0.11，0.15                  |
| number(3,2)  | 错误：12，12.1 正确:1.12,1.15555               |
| number(3,-2) | 错误：123456 正确:12345(结果:12300),12(结果:0) |

[定长和变长字符集](https://www.cnblogs.com/yelongsan/p/6290206.html)，感兴趣的可以了解一下。

建表：
可以在建表时指定主键或其他各种约束，也可以在建好表后，修改表时增加这些约束。
create table table_name(colname datatype[,…])

```sql
-- 最简单的表
create table t1(id number);
-- 指定id最长3位数字，username可变长，最长20
create table t2(id number(3),username varchar(20),birthday date);
1234
```

修改表：
alter table tablename …

```sql
-- 给表增加列
alter table t1 add c3 char(10);
-- 给表增加主键，主键没有指定名称
alter table t1 add primary key(c1);
-- 删除刚才增加的主键约束
alter table t1 drop primary key;
-- 给表增加主键，指定主键名称
alter table t1 add constraint t1_pk primary key(c1);
-- 删除指定名称的主键
alter table t1 drop constraint t1_pk;
12345678910
```

如果t1表中的c3列是char型，长度是2
insert into t1(c3) values(‘1’);
c3列长度是2，插入的值是1个长度，但因为列类型是char型，所以实际长度变成了‘1 ’值中有空格。
修改列的宽度时，不能小于2。
alter table t1 modify c3 char(3);

```sql
-- 创建表时没有指定任何约束
create table t_user(id char(32),name char(10),password char(8),sex number(1),age number(2));
-- 添加主键约束
alter table t_user add constraint pk_user primary key(id);
-- 添加唯一约束
alter table t_user add constraint unq_user unique(name);
-- 添加列的默认值
alter table t_user modify password default '12345678';
-- 添加表的检查约束
alter table t_user add constraint chk_user_sex check(sex=0 or sex=1);
12345678910
```

删除表：
drop table tablename;

```sql
drop table t1;
1
```

### DML

对数据的操作，增删改
insert into table,update table,delete from table
insert into table_name [(c1[,…])] values(v1[,…])

```sql
-- 只写了id和name列，其他列没有指定值
insert into t_user(id,name) values('a1b1','admin');
-- 如果没有指定列，只有values，则values的顺序要按钮列的顺序来写
-- id,name,password,sex,age
insert into t_user values('a1b1','admin','12345678',0,10);
12345
```

update table_name set col1=v1[,…] [where col=v]

```sql
-- 更新数据指定id为'a1b1'的记录
update t_user set name='admin_new',age=11 where id='a1b1';
12
```

delete from table_name [where col=v]

```sql
delete from t_user;
1
```

这里有一个trunc的操作，此操作也是针对表记录的，是清空表中的所有记录，而不是delete所有，它们的区别是：delete删除记录后不会释放表所占的空间，在给表中增加记录时，有一个数据指针会依次变化增高位置，delete后这个指针并没有回落，以前数据占用的空间还在，数据也在，只是做了逻辑删除，我们看不到数据而已，但是通过数据恢复操作还可以恢复这些数据，有点类似Windows操作系统的回收站情形。但是trunc操作表后，会立即释放表空间，就像清空回收站的操作一样，所以数据是不可再恢复的。

### DQL

对数据的查询， 这个是SQL的主要内容，有单表查询，多表查询，嵌套查询，排序 ，分页，去重，结果合并等内容。
select col1[,…] from table_name [ where col1=xx,…]
SQL查询语句可以很简单也可以很复杂

#### 单表查询

- 简单查询
  select * from t_user;
  这是最简单的SQL语句，查询所有列时可以用 "*"来代替，但是，在规范上不建议使用*查询，这样会让数据库去数据仓库获取字段信息然后执行查询，在性能上会有所降低，不如下面的SQL效率高：
  select id,name,password,age,sex from t_user;
- 别名
  对一些字段比较长或是经过运算得出的查询结果可以用别名作为查询结果显示，如：
  select sal,sal+100 from emp;
  emp表是Oracle自带用户scott下的一张表，scott用户下的表和数据可以供我们学习DQL来使用，此处的这条SQL是查询emp（员工表）中的所有员工工资和加100元后的结果，第二列sal+100作为结果列的显示可以使用别名，别名是在列或表达后加as关键字或不加也可以
  select sal,sal+100 as sal2,sal+100 sal3 from emp;
  以上两种写法都可以。
- 条件过滤
  如果只要查部分数据，可以使用where条件进行过滤
  select empno,ename,sal from emp where sal>=3000
  查询员工工资大于等于3000的员工的编号和姓名及工资信息
- 去重
  查看emp表中部门共有几个
  select deptno from emp;
  得到的数据会有大量重复的，如果去重可以用distinct关键字
  select distinct deptno from emp;
  ![img](https://img-blog.csdnimg.cn/20201216154431554.png)
  distinct关键字会对它后面跟着的所有字段进行过滤
  ![img](https://img-blog.csdnimg.cn/20201216155030416.png)
  没有过滤之前有14条记录，其中标红色的是重复的，加上distinct后，变成了12条
  ![img](https://img-blog.csdnimg.cn/20201216155150349.png)
- 排序
  order by 字段名[,…] [ asc|desc] 默认是升序asc，desc是降序
  按照工资进行由高到低排序:
  select sal from emp order by sal desc;
  order by 可以同时使用多个字段，如：部门升序，sal降序

![img](https://img-blog.csdnimg.cn/20201216155927874.png)

- 分页 

  有时表中记录过多，不想全部查询出来，如果是在网页上加载表中上千万条数据，会是一个非常不好的用户体验，此时可以使用分页技术，一次显示一页数据，然后逐次分页显示。Oracle中分页用到一个伪列（物理不存在的列，Oracle对结果进行计算得到的临时列）rownum来进行分页处理。如果一个查询结果是14条，则rownum从1到14显示。 select empno,rownum from emp;

  

   ![img](https://img-blog.csdnimg.cn/20201216160433600.png) 

- 如果一页显示3条记录，则分页的SQL可以这样写: 

  ``` 
  SELECT *
  FROM   (SELECT empno,
                 ROWNUM NO
          FROM   emp)t
  WHERE  t.no > ( 4 - 1 ) * 3
         AND t.no <= 4 * 3;
  
  SELECT t2.*
  FROM   (SELECT t1.*,
                 ROWNUM rn
          FROM   (SELECT empno
                  FROM   emp
                  ORDER  BY empno) t1) t2
  WHERE  t2.rn > 9
         AND t2.rn <= 12;
  
  SELECT empno,
         ROWNUM NO
  FROM   emp
  
  ```

  

  以上SQL中第三条是没有分页，可以看到empno在表中本身是升序的，rownum从1到14 以上第一条SQL是分页的，没有排序，结果也是正确的，第二条SQL是分页后的排序，结果和第一条SQL一样。 如果排序字段是sal，结只能用第二条SQL，因为只有这样才能保证是排序后的分页，第一条SQL不适用，排序sal后，rownum就乱了，分页的结果不正确。

  #### 多表查询 

  查询员工编号、姓名、部门编号、部门名称信息，因为部门名称不在员工表中，部门表中又没有员工信息，所以需要两张表共同完成查询，为了让员工表中的部门编号和部门表中的部门名称一一对应，需要对这两张表中的deptno员工编号字段进行关联，这儿的关联有四种关联关系：1.内连接；2.左外连接；3.右外连接；4：全外连接。 

  + 内连接 

  select 表1.*，表2.* from 表1 inner join 表2 on 表1.列1=表2.列1 inner join （inner可以省略) on后面的表1中的列1和表2中的列1是两个表之间的桥梁列 select empno,ename,d.deptno,dname from emp inner join dept d on emp.deptno=d.deptno; select empno,ename,d.deptno,dname from emp join dept d on emp.deptno=d.deptno; 内连接可以写成以下这种形式，这也是普通使用的形式，反而inner join使用的少。 select empno,ename,d.deptno,dname from emp,dept d where emp.deptno = d.deptno; 这种写法是把多表写在from关键字后面，用逗号隔开，连接条件写在where子句中。

  - 左外连接 

    select 表1.*，表2.* from 表1 left outer join 表2 on 表1.列1=表2.列1 left outer join （outer可以省略) on后面的表1中的列1和表2中的列1是两个表之间的桥梁列 可以获得left表中所有的记录，即便右表中没有和它对应的记录左表也显示。

    ``` 
    -- 没有指定部门信息，如果用普通的内联则不会显示这条记录
    insert into emp (empno,ename) values(8000,'newemp');
    select empno,ename,d.deptno,dname from emp left outer join dept d on emp.deptno=d.deptno;
    ```

     在上述SQL中，如果emp表中有一个员工没有设置部门信息，也会显示出来这个员工信息，只不过这个记录中只有员工信息没有部门信息。![img](https://img-blog.csdnimg.cn/20201217105656697.png)

- 右外连接

  右外连接和左外连接原理是一样的，如果 A left outer join B，则A表是左表，B表是右表，会显示A中所有记录，B中有关联的记录，如果把B和A换一下位位置，则显示B表所有记录，A表显示关联记录，如果不换A和B的位置，还想显示B表所有记录，则把left关键字换成right就可以。

  ``` 
  select empno,ename,d.deptno,dname 
  from emp right outer join dept d 
  on emp.deptno=d.deptno;
  ```

  ![img](https://img-blog.csdnimg.cn/20201217140709531.png)

- 全外连接

  如果说左外连接是集合1，右外连接是集合2，则全外连接就是两个集合的并集。
  关键字是full outer join，outer可以省略

  ```sql
  select empno,ename,d.deptno,dname
  from emp full outer join dept d 
  on emp.deptno=d.deptno;
  
  ```

  ![img](https://img-blog.csdnimg.cn/20201217141231913.png)

### TCL

增加修改和删除数据后（DML语句）要进行commit或rollback才能使数据永久生效
commit是提交修改结果，rollback是撤销修改，恢复修改前的数据。
对事务的操作

### DCL

grant 角色/权限 to 用户; 分配角色或权限
revoke 角色/权限 from 用户; 回收角色或权限
对权限的操作，grant 和revoke语句



## 内置函数

在学习函数时有必要认识Oracle的一个特殊表dual（虚表），这个表不存在物理的表，只是方便用来测试或使SQL语句完整，通常不需要指定具体的业务表时，可以跟在from后面使SQL完整。
select 表达式 from dual;

### 单行函数

#### 字符函数

| 函数                                | 说明                                                         |
| ----------------------------------- | ------------------------------------------------------------ |
| ascii(x)                            | 返回x的ascii值 select ascii(‘a’) from dual;-- 97             |
| concat(x,y)                         | 返回x和y的拼起来的字符串 select concat(‘a’,‘b’) from dual;–ab |
| instr(strObj,strSearch[,start[,n]]) | 在strObj中查找strSearch内容，从start位置开始找起，返回第n个结果的索引，start和n默认为1，可以不指定 select instr(‘a1a2a3a4’,‘a’) from dual;–1 索引从1开始 select instr(‘a1a2a3a4’,‘a’,2) from dual;-- 从索引2开始找a，结果是3 select instr(‘a1a2a3a4’,‘a’,2,2) from dual;-- 从索引2开始返回第二个结果，索引为5 |
| length(x)                           | x的长度 select length(‘abc’) from dual;-- 3                  |
| lower(x)                            | x的小写形式 select lower(‘aBcD’) from dual;-- abcd           |
| upper(x)                            | x的大写形式 select upper(‘aBcD’) from dual;-- ABCD           |
| ltrim(x[,str])                      | 去掉左边的字符串，默认是空格 select length(ltrim(’ abc’)) from dual;-- 3，因为结果是’abc’去掉了左边的空格 select length(ltrim(’***abc’,’*’)) from dual; – 去掉字符串中的* 结果为3 |
| rtrim(x[,str])                      | 类似于ltrim，该函数是去掉右边的字符                          |
| trim(x[,str])                       | 去掉左右两边的字符                                           |
| replace(strObj,old,new)             | 替换字符中的old为new select replace(‘a1a1a1’,‘1’,‘a’) from dual;-- aaaaaa |
| substr(strObj,star[,length])        | 从strObj中截取字符串,star是开始位置，length可以省略，默认从star位置截取到strObj最后 select substr(‘abcdefg’,2) from dual;-- bcdefg select substr(‘abcdefg’,2,4) from dual;-- bcde |

#### 数字函数

| 函数         | 说明                                                         |
| ------------ | ------------------------------------------------------------ |
| abs(x)       | 取x的绝对值 select abs(-1) from dual;-- 1                    |
| ceil(x)      | 大于或等于x的最小值 select ceil(1.1) from dual;-- 2 select ceil(-1.9) from dual;-- -1 |
| floor(x)     | 返回小于或等于x的最大值 select floor(1.9) from dual;–1 select floor(-1.1) from dual;-- -2 |
| round(x[,y]) | 在y位上四舍五入，y可以省略，默认取值并四舍五入 select round(3.45),round(3.51),round(3.4444,2),round(3.5555,2) from dual;-- 3,4,3.44,3.56 |
| trunc(x[,y]) | 在y位上截断，y省略的话是取整，不会四舍五入，只是简单截断     |
| mod(x,y)     | 求x除以y的余数 select mod(5,2) from dual;-- 1                |
