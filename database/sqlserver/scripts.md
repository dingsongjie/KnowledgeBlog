# Scripts



| 名称              | 脚本                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| --------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 查看锁及语句          | <pre class="language-javascript"><code class="lang-javascript">select * from
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
CROSS APPLY sys.dm_exec_sql_text(PROCESS.SQL_HANDLE) SQLTEXT) AS ta
</code></pre><p>```</p>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| 查看基本的执行诊断       | <pre class="language-sql"><code class="lang-sql">SET STATISTICS TIME ON
SET STATISTICS IO ON
  
SET STATISTICS IO OFF
SET STATISTICS TIME OFF
</code></pre>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| 查看tempdb使用相关的语句 | <pre class="language-sql"><code class="lang-sql">SELECT
st.dbid AS QueryExecutionContextDBID,
DB_NAME(st.dbid) AS QueryExecContextDBNAME,
st.objectid AS ModuleObjectId,
SUBSTRING(st.TEXT,
dmv_er.statement_start_offset/2 + 1,
(CASE WHEN dmv_er.statement_end_offset = -1
THEN LEN(CONVERT(NVARCHAR(MAX),st.TEXT)) * 2
ELSE dmv_er.statement_end_offset
END - dmv_er.statement_start_offset)/2) AS Query_Text,
dmv_tsu.session_id ,
dmv_tsu.request_id,
dmv_tsu.exec_context_id,
(dmv_tsu.user_objects_alloc_page_count - dmv_tsu.user_objects_dealloc_page_count) AS OutStanding_user_objects_page_counts,
(dmv_tsu.internal_objects_alloc_page_count - dmv_tsu.internal_objects_dealloc_page_count) AS OutStanding_internal_objects_page_counts,
dmv_er.start_time,
dmv_er.command,
dmv_er.open_transaction_count,
dmv_er.percent_complete,
dmv_er.estimated_completion_time,
dmv_er.cpu_time,
dmv_er.total_elapsed_time,
dmv_er.reads,dmv_er.writes,
dmv_er.logical_reads,
dmv_er.granted_query_memory,
dmv_es.HOST_NAME,
dmv_es.login_name,
dmv_es.program_name
FROM sys.dm_db_task_space_usage dmv_tsu
INNER JOIN sys.dm_exec_requests dmv_er
ON (dmv_tsu.session_id = dmv_er.session_id AND dmv_tsu.request_id = dmv_er.request_id)
INNER JOIN sys.dm_exec_sessions dmv_es
ON (dmv_tsu.session_id = dmv_es.session_id)
CROSS APPLY sys.dm_exec_sql_text(dmv_er.sql_handle) st
WHERE (dmv_tsu.internal_objects_alloc_page_count + dmv_tsu.user_objects_alloc_page_count) > 0
ORDER BY (dmv_tsu.user_objects_alloc_page_count - dmv_tsu.user_objects_dealloc_page_count) + (dmv_tsu.internal_objects_alloc_page_count - dmv_tsu.internal_objects_dealloc_page_count) DESC
</code></pre> |
| 查看数据库id         | <pre class="language-sql"><code class="lang-sql">SELECT database_id, name
FROM sys.databases;
</code></pre>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
| 查看读写磁盘前10的语句    | <pre class="language-sql"><code class="lang-sql">SELECT TOP 10 qs.total_logical_reads, qs.total_logical_writes, qs.execution_count, st.text AS [SQL Text] FROM sys.dm_exec_query_stats AS qs CROSS APPLY sys.dm_exec_sql_text(qs.sql_handle) AS st ORDER BY (qs.total_logical_reads + qs.total_logical_writes) DESC;
</code></pre>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                             |
| 查看数据库文件磁盘读写延迟   | <pre class="language-sql"><code class="lang-sql">SELECT files.physical_name, files.name,
stats.num_of_writes, (1.0 * stats.io_stall_write_ms / stats.num_of_writes) AS avg_write_stall_ms,
stats.num_of_reads, (1.0 * stats.io_stall_read_ms / stats.num_of_reads) AS avg_read_stall_ms
FROM sys.dm_io_virtual_file_stats(2, NULL) as stats
INNER JOIN master.sys.master_files AS files
ON stats.database_id = files.database_id
AND stats.file_id = files.file_id
WHERE files.type_desc = 'ROWS'
</code></pre>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                |

