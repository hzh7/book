# HiveSQL

## 基础操作

- 插入数据
    ```sql
    insert into table hive_temp_advert.hzh_fot_test partition (dt = '20200607') values ('1', 'gg');
    ```
_into必须，括号必须_

## 一些技能

- 解析字段中的json数据
    ```sql
    get_json_object(activity_property,'$.factory') 
    -- 或者 --
    `lateral view` 如：
    SELECT 
        code, id, id_type,
        max(vers) as vers,
        max(hm) as hm
    from vipdw.ods_udp2usp_realtime_msg_kafkasource_5min t1
        lateral view json_tuple(t1.message,'code','id','idType','version') t2
        as code, id, id_type, vers
    where dt='${dt}' 
        and t1.hm in (select MAX(hm) from vipdw.ods_udp2usp_realtime_msg_kafkasource_5min where dt='${dt}' limit 1)
    group by 
        code, id, id_type
    ```