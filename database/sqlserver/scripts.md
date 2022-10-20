# Scripts



| 名称                         | 脚本                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
| -------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 查看锁及语句                     | <pre class="language-javascript"><code class="lang-javascript">select * from
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
| 查看1                        | <pre class="language-javascript"><code class="lang-javascript">function getReadableFileSizeString(fileSizeInBytes) {

    var i = -1;
    var byteUnits = [' kB', ' MB', ' GB', ' TB', 'PB', 'EB', 'ZB', 'YB'];
    do {
        fileSizeInBytes = fileSizeInBytes / 1024;
        i++;
    } while (fileSizeInBytes > 1024);

    return Math.max(fileSizeInBytes, 0.1).toFixed(1) + byteUnits[i];
};
var collectionNames = db.getCollectionNames(), stats = [];
collectionNames.forEach(function (n) { stats.push(db[n].stats()); });
stats = stats.sort(function(a, b) { return b['size'] - a['size']; });
for (var c in stats) { 
print(stats[c]['ns'] + ": " + getReadableFileSizeString(stats[c]['size']) + " (" + getReadableFileSizeString(stats[c]['storageSize']) + ")" + " (" + getReadableFileSizeString(stats[c]['totalIndexSize']) + ")"); 
}</code></pre>                                                                                                                                                                                                                                                                           |
| 删除数据库中有名字特征的集合             | <pre class="language-javascript"><code class="lang-javascript">var collectionNames = db.getCollectionNames();
 for(var i = 0, len = collectionNames.length; i &#x3C; len ; i++){
  var collectionName = collectionNames[i];
   if(collectionName.endsWith('transformLog')||collectionName.endsWith('DataVersion')){ 
   print(collectionName); 
   db[collectionName].drop() 
   } 
 }</code></pre><p><code></code></p>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            |
| 获取当前实例featureCompatibility | <p></p><pre class="language-javascript"><code class="lang-javascript">db.adminCommand( { getParameter: 1, featureCompatibilityVersion: 1 } );</code></pre>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| 设置当前实例featureCompatibility | <pre class="language-javascript"><code class="lang-javascript">db.adminCommand( { setFeatureCompatibilityVersion: "4.0" } )</code></pre>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| 压缩当前集合空间                   | <p><code></code><br><code>db.runCommand( { compact: &#x3C;collection name> }</code> </p>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                           |
| 副本集主节点尝试降级从节点              | <pre><code>db.adminCommand( { replSetStepDown: 10 } )</code></pre>                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                 |
|                            |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |
|                            |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                    |

