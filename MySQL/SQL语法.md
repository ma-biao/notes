

# 1. 数据库操作

1. 创建：
   - 创建数据库：`create database 数据库名称;`
   - 创建数据库，判断不存在，再创建：`create database if not exists 数据库名称;`
   - 创建数据库，并指定字符集：`create database 数据库名称 character set 字符集名;`
2. 查询
   - 查询所有数据库的名称：`show databases;`
   - 查询某个数据库的创建语句：`show create database 数据库名称;`
3. 修改
   - 修改数据的字符集：`alter database 数据库名称 character set 字符集名称;`
4. 删除
   - 删除数据库：`drop database 数据库名称;`
   - 判断数据库存在，存在再删除：`drop database if exists 数据库名称;`
5. 使用数据库
   - 查询当前正在使用的数据库名称：`select database();`
   - 使用数据库：`use 数据库名称;`



# 2. 表操作

## 2.1 新建表

```sql
create table user_info_vip(
    id int(11) primary key auto_increment comment "自增ID",
    uid int(11) unique not null comment "用户ID",
    nick_name varchar(64) comment "昵称",
    achievement int(11) default 0 comment "成就值",
    level int(11) comment "用户等级",
    job varchar(32) comment "职业方向",
    register_time datetime default current_timestamp comment "注册时间"
)default charset=utf8
```



## 2.2 修改表

1.添加列
alter table 表名 add column 列名 类型 【first|after 字段名】;
2.修改列的类型或约束
alter table 表名 modify column 列名 新类型 【新约束】;
3.修改列名
alter table 表名 change column 旧列名 新列名 类型;
4 .删除列
alter table 表名 drop column 列名;
5.修改表名
alter table 表名 rename 【to】 新表名;
6.将某一列放到第一列
alter table 表名 modify column 列名 类型 first;