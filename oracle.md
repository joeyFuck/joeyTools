1 字符串转数字 to_number(regexp_substr(yhid,'[0-9]*[0-9]',1))

2 create tablespace flowable_engine datafile 'E:\app\hangjie.zhu\oradata\orclflowable\flowable_engine.dbf' size 150M; -- 在当前实例下建表空间

3 create user xcrsdb_engine_user1 identified by xcrsdb_engine_user1 default tablespace flowable_engine; --在当前实例下建用户


4 导出某个用户下的所有表
exp "XCRSDB_ENGINE_USER1/credit123@127.0.0.1:1521/orclflowable" file=f:\flowable20190926.dmp  owner=XCRSDB_ENGINE_USER1

导入
imp "xcrsdb_flowable/credit123@127.0.0.1:1521/orcl" file=f:\localhost20190926.dmp full=y ignore=y


5 账号被锁
用dba登陆
ALTER USER xcrsdb_zhj ACCOUNT UNLOCK;
commit;
然后修改密码，不修改密码，仍未解锁

6 导出dmp时，有些空表未导出（手动分配表空间）

select 'analyze table '||table_name||' compute statistics;' from user_tables;
--复制生成的所有语句一起执行
analyze table ACT_RU_VARIABLE compute statistics;--分析表以生成相关表的数据（-->user_tables）
--analyze ....
select 'alter table '||table_name||' allocate extent;' from user_tables where num_rows = 0 
--复制生成的所有语句一起执行
alter table ACT_EVT_LOG allocate extent; --给当前用户下的表分配空间
--alter ....

