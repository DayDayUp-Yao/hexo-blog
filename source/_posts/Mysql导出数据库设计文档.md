title: MySQL导出数据库设计文档
author: Yao Fei
date: 2020-12-05 16:27:10
tags: MySQL
cover: http://yfmine.work:8080/images/1.jpg
coverWidth: 1440
coverHeight: 960
categories: 数据库相关
---


SELECT
    TABLE_NAME 表名,
    ORDINAL_POSITION 序号,
    COLUMN_NAME 字段名,
    COLUMN_TYPE 类型,
IF
    ( IS_NULLABLE = 'NO', 'M', '0' ) AS '限制',--  IS_NULLABLE = 'NO' 时，为必填，必填返回“是”，非必填返回空
    COLUMN_DEFAULT 默认值,
IF
    ( column_key = 'PRI', '*', '' ) AS '主键唯一', -- column_key='PRI' 时，为主键唯一索引，是返回“是”，否返回空
    COLUMN_COMMENT 注释
-- CHARACTER_MAXIMUM_LENGTH 字符串最大长度【以字符为单位】,
-- CHARACTER_OCTET_LENGTH 字符串最大长度【以字节为单位】,
-- CHARACTER_SET_NAME 字符串字符集名称,
-- COLLATION_NAME 字符串归类名称,
-- NUMERIC_PRECISION 数字精度,
-- NUMERIC_SCALE 数字刻度,
-- DATETIME_PRECISION 时间分数秒精度
    
FROM
    INFORMATION_SCHEMA.COLUMNS
    WHERE-- performance_schema 为数据库名称，到时候只需要修改成你要导出表结构的数据库即可
    table_schema = 'taizhouintegration' -- AND
-- events_errors_summary_by_account_by_error 为表名，到时候换成你要导出的表的名称
-- 如果不写的话，默认会查询出该数据库中所有表的表结构；这里如果指定表名，则可以导出单独一个表的表结构
-- table_name = 'events_errors_summary_by_thread_by_error'
    
ORDER BY
    TABLE_NAME,
    ORDINAL_POSITION
