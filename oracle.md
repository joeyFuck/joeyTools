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

9 聚合函数 -- LISTAGG
 聚合
select LISTAGG (NAME,'-') REGION_NAME from T1 t

 聚合+排序
select LISTAGG (NAME,'-') within group(order by r1 DESC) REGION_NAME from T1 t
 
 聚合+排序+其他分组列
select t.code, LISTAGG (NAME,'-') within group(order by r1 DESC) REGION_NAME from T1 t group by t.code

 聚合+排序+任意列(比直接在多表关联查询中使用聚合子查询要快的多)
select t.code, t.c1,t.c21,m.c_name, 
LISTAGG (NAME,'-') within group(order by r1 DESC) over(PARTITION BY t.code) REGION_NAME 
from T1 t
left join T2 m ON m.code = t.code
 
 直接在多表关联查询中使用聚合子查询 (较慢)
SELECT distinct t.f_code doc_id,T.*,B.D_NAME,U.EM_USERNAME,
    (
         select LISTAGG (O_NAME,',') from tcrt_document_obj_map where F_CODE = t.F_CODE
    ) OBJ_NAME,
              
FROM TCRT_DOCUMENT T
LEFT JOIN TXF_DIR_MNODE B ON T.D_ID=B.D_ID
LEFT JOIN TSYS_USER U ON U.EM_ID = T.F_UPLOADER
left join tcrt_document_obj_map m on m.f_code = t.f_code

多表关联查询中使用聚合+分析函数(较快)
SELECT distinct t.f_code doc_id,T.*,B.D_NAME,U.EM_USERNAME, 

   listagg (distinct m.O_NAME, ',') WITHIN GROUP (ORDER BY m.O_NAME)  over(PARTITION BY m.f_code) OBJ_NAME
 
FROM TCRT_DOCUMENT T
LEFT JOIN TXF_DIR_MNODE B ON T.D_ID=B.D_ID
LEFT JOIN TSYS_USER U ON U.EM_ID = T.F_UPLOADER
left join tcrt_document_obj_map m on m.f_code = t.f_code



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



