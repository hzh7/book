# MySQL

## 增删改查

### 改

- update

```sql
UPDATE 表名称 SET 列名称 = 新值 WHERE 列名称 = 某值
```

- ALTER TABLE 语句 

    ALTER TABLE 语句用于在已有的表中添加、修改或删除列。

    如需在表中添加列，请使用下列语法:
    ```sql
    ALTER TABLE table_name
    ADD column_name datatype
    ```
    _Hiev sql中有区别：_
    ```sql
    ALTER TABLE hive_temp_advert.hzh_fot_test 
    ADD COLUMNS (advertiser_type int comment '广告主类型');
    ```
### 删

- 删除表中的列

```sql
ALTER TABLE table_name 
DROP COLUMN column_name
```
_注释：某些数据库系统不允许这种在数据库表中删除列的方式 (DROP COLUMN column_name)。_

要改变表中列的数据类型，请使用下列语法：
```sql
ALTER TABLE table_name
ALTER COLUMN column_name datatype
```

## 一些函数

### 时间转换函数

- UNIX时间戳转换为日期用函数： FROM_UNIXTIME()

```sql
select FROM_UNIXTIME(1156219870);
```
    输出：2006-08-22 12:11:10

- 日期转换为UNIX时间戳用函数： UNIX_TIMESTAMP()

```sql
    Select UNIX_TIMESTAMP('2006-11-04 12:23:00');
```
    输出：1162614180

## 一些技能

- [mysql分组取最大(最小、最新、前N条)条记录](https://my.oschina.net/dslcode/blog/2247977)

- 判断表中一个字段是否存在

    ```sql
    select count(*) from information_schema.columns where table_name = '表名' and column_name = '字段名'
    ```

- [Mybatis主键回写Model](https://blog.csdn.net/u010452388/article/details/80822657)

  ```sql
  <insert id="insert" parameterType="com.vip.imp.dmp.userattribute.entity.RtCrowdTag" keyColumn="id" keyProperty="id" useGeneratedKeys="true">
  ```

- 