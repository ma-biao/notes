# 1、函数的使用

MySQL中提供了大量函数来简化用户对数据库的操作，比如字符串的处理、日期的运算、数值的运算等等。使用函数可以大大提高SELECT语句操作数据库的能力，同时也给数据的转换和处理提供了方便。（在sql中使用函数）


函数只是对查询结果中的数据进行处理，不会改变数据库中数据表的值。MySQL中的函数主要分为单行函数和多行函数两大类，下面我们将详细讲解这两大类函数。



# 2、单行函数

单行函数是指对每一条记录输入值进行计算，并得到相应的计算结果，然后返回给用户，也就是说，每条记录作为一个输入参数，经过函数计算得到每条记录的计算结果。

常用的单行函数主要包括字符串函数、数值函数、日期与时间函数、流程函数以及其他函数。

## 2.1 字符串函数

```sql
selelct ename,length(ename),substring(ename,2,3) from emp;
```

substring:字符串截取，2：从字符下标为2开始，截取长度3起，始位置为从1开始



## 2.2 数值函数

```sql
select abs(-5),ceil(5.3),floor(5.9),round(3.14) from dual; -- dual:伪表 select abs(-5) as 绝对值,ceil(5.3) as 向上取整,floor(5.9) as 向下取整,round(3.14) as 四舍五入; --
```



## 2.3 日期和时间函数

```sql
select now(),sysdate(),sleep(3),now(),sysdate() from dual
```



时间单位：

- FRAC_SECOND：表示间隔是毫秒
- SECOND：秒
- MINUTE：分钟
- HOUR：小时
- DAY：天
- WEEK：星期
- MONTH：月
- QUARTER：季度
- YEAR：年



- 日期差`timestampdiff(单位,a,b)`表示a-b，并且单位指定

  ```sql
  timestampdiff(minute, submit_time, start_time)
  ```

- 日期加上一段时间`TIMESTAMPADD(interval,int_expr,datetime_expr)`，其中interval为时间单位，int_expr整型表达式，表示时间长度，datetime_expr为具体时间表达式。

  ```sql
  select TIMESTAMPADD(MINUTE,30,'2012-08-24 09:00:00') -- 在2012-08-24 09:00:00基础上加上30分钟
  ```

- 计算某个日期前的日期具体时间：`DATE_SUB(date_time, INTERVAL time_size time_type)`，其中date_time为时间参考值，time_size具体时间数，time_type为最后获取时间的参数

  ```sql
  DATE_SUB(CURDATE(), INTERVAL 30 DAY) --获取当前日期30天前的日期
  ```

- 计算某个日期后的日期具体时间：`DATE_ADD(date_time, INTERVAL time_size time_type)`，用法同上。



## 2.4 流程函数

### 2.4.1 if相关

```sql
select empno,ename,job, case job when 'CLERK' then '店员' when 'SALESMAN' then '销售' when 'MANAGER' then '经理' else '其他'end '岗位', sal from emp;
```



### 2.4.2 case相关

```sql
select empno,ename,sal, case when sal<1000 then 'A' when sal<2000 then 'B' when sal<3000 then 'C' else 'D'end '工资等级', deptno from emp;
```



## 2.5 其他函数

```sql
select database(),user(),version() from dual;
```

查看数据库名、用户、mysql的版本



#3、多行函数

多行函数是指对一组数据进行运算，针对这一组数据（多行记录）只返回一个结果，也称为分组函数。



## 3.1 多行函数

```sql
select max(sal),min(sal),count(sal),sum(sal),avg(sal) from emp;
```



## 3.2 多行函数会自动忽略null值

 

## 3.3 max(),min(),count():针对所有类型 sum(),avg()只针对数值类型有效



## 3.4 count()函数：统计表的记录数

方式一：一般用count(*)统计记录数，因为表中的其他字段可能为空。

```sql
select count(*) from emp;
```



方式二：

```sql
select 1 from dual select 1 from emp; -- 有多少条记录，展示多少个1 select count(1) from emp
```

select count(1) from emp：查表中有多少记录