1 字符串转数字 to_number(regexp_substr(yhid,'[0-9]*[0-9]',1))

2 create tablespace flowable_engine datafile 'E:\app\hangjie.zhu\oradata\orclflowable\flowable_engine.dbf' size 150M; -- 在当前实例下建表空间

3 create user xcrsdb_engine_user1 identified by xcrsdb_engine_user1 default tablespace flowable_engine; --在当前实例下建用户

删除用户（即删库）
select username,sid,serial#,t.* from v$session t where username='PF_XCRMS' ;--
alter system kill session '9,27190' ;
alter user PF_XCRMS account UNLOCK
alter session set "_ORACLE_SCRIPT"=true; 
--drop user PF_XCRMS CASCADE

4 导出导入某个用户下的所有表

导出

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

7 NVL( string1, replace_Str) 

8 表被锁

  SELECT T2.USERNAME, T2.SID, T2.SERIAL#, T2.LOGON_TIME
    FROM V$LOCKED_OBJECT T1, V$SESSION T2
   WHERE T1.SESSION_ID = T2.SID
   ORDER BY T2.LOGON_TIME;

  alter system kill session '99,3783';

9 聚合函数
select LISTAGG (NAME,'-') within group(order by r1 DESC) REGION_NAME from t1

10 父子结构
select TR.NAME, ROWNUM RN from TREGION TR
CONNECT BY PRIOR TR.P_CODE = TR.CODE
START WITH TR.CODE = '440303'

PRIOR TR.P_CODE = TR.CODE
or
PRIOR TR.CODE = TR.P_CODE
决定了从上到下or从下到上查找

11 开窗函数
select A.O_CODE, A.O_GRADE, A.O_OUTLOOK, RANK() OVER(PARTITION BY A.O_CODE ORDER BY A.BASEDATE DESC) RN 
from TCORP_GRADE  A WHERE O_CODE = 'CP20170223112223450' 


12 闪回 flashback 针对某张表还原到某个时间节点
alter table tpool_bond_ext enable row movement;

flashback table tpool_bond_ext to timestamp 
to_timestamp('2015-06-04 17:00:00','yyyy-mm-dd HH24:MI:SS');



