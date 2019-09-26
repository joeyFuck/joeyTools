1 字符串转数字 to_number(regexp_substr(yhid,'[0-9]*[0-9]',1))

create tablespace flowable_engine datafile 'E:\app\hangjie.zhu\oradata\orclflowable\flowable_engine.dbf' size 150M; -- 在当前实例下建表空间

create user xcrsdb_engine_user1 identified by xcrsdb_engine_user1 default tablespace flowable_engine; --在当前实例下建用户


导出某个用户下的所有表
exp "XCRSDB_ENGINE_USER1/credit123@127.0.0.1:1521/orclflowable" file=f:\flowable20190926.dmp  owner=XCRSDB_ENGINE_USER1

导入
imp "xcrsdb_flowable/credit123@127.0.0.1:1521/orcl" file=f:\localhost20190926.dmp full=y ignore=y


ALTER USER xcrsdb_zhj ACCOUNT UNLOCK;
commit;
然后修改密码，不修改密码，仍未解锁

