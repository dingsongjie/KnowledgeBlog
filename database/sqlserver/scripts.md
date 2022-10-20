# Scripts



| 名称        | 脚本                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| --------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 查看锁及语句    | <pre class="language-javascript"><code class="lang-javascript">select * from
(
SELECT 
db_name(rsc_dbid) AS 'DATABASE_NAME',
case rsc_type when 1 then 'null'
              when 2 then 'DATABASE' 
              WHEN 3 THEN 'FILE'
              WHEN 4 THEN 'INDEX'
              WHEN 5 THEN 'TABLE'
              WHEN 6 THEN 'PAGE'
              WHEN 7 THEN 'KEY'
              WHEN 8 THEN 'EXTEND'
              WHEN 9 THEN 'RID ( ROW ID)'
              WHEN 10 THEN 'APPLICATION' end  AS 'REQUEST_TYPE',

req_mode as Lock_Type,
rsc_objid as ID,
rsc_indid as INDEX_ID,
CASE req_ownertype WHEN 1 THEN 'TRANSACTION'
                   WHEN 2 THEN 'CURSOR'
                   WHEN 3 THEN 'SESSION'
                   WHEN 4 THEN 'ExSESSION' END AS 'REQUEST_OWNERTYPE',

OBJECT_NAME(rsc_objid ,rsc_dbid) AS 'OBJECT_NAME', 
PROCESS.HOSTNAME , 
PROCESS.program_name , 
PROCESS.nt_domain , 
PROCESS.nt_username , 
SQLTEXT.text 
FROM sys.syslockinfo LOCK JOIN 
     sys.sysprocesses PROCESS
  ON LOCK.req_spid = PROCESS.spid
CROSS APPLY sys.dm_exec_sql_text(PROCESS.SQL_HANDLE) SQLTEXT) AS ta</code></pre><p>```</p> |
| 查看基本的执行诊断 | <pre class="language-javascript"><code class="lang-javascript">  SET STATISTICS TIME ON
SET STATISTICS IO ON
  
SET STATISTICS IO OFF
SET STATISTICS TIME OFF</code></pre>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
|           |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
|           |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |

