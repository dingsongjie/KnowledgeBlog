---
description: 数据库管理脚本
---

# admin scripts

| 名称                                       | 脚本                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| ---------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| 打印实例中所有数据库的存储大小-sizeOnDisk               | <pre class="language-javascript"><code class="lang-javascript">db.adminCommand("listDatabases").databases
    .sort(function(l, r) {
	return r.sizeOnDisk - l.sizeOnDisk})
    .forEach(function(d) {
	var sizeKB = d.sizeOnDisk/1024; 
	var sizeMB = sizeKB/1024; 
	var sizeGB = sizeMB/1024; 
	var output = (sizeKB > 1024 ? (sizeMB > 1024 ? sizeGB.toFixed(2) + " GB" : sizeMB.toFixed(2) + " MB") : sizeKB.toFixed(2) + " KB"); 
	print(d.name + " - " + output)
	});			 </code></pre><p>```</p>                                                                                                                                                                                                                                                                                                                                                                    |
| 打印数据库中集合的size,storageSize,totalIndexSize | <pre class="language-javascript"><code class="lang-javascript">function getReadableFileSizeString(fileSizeInBytes) {

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
}</code></pre> |
| 删除数据库中有名字特征的集合                           | <pre class="language-javascript"><code class="lang-javascript">var collectionNames = db.getCollectionNames();
 for(var i = 0, len = collectionNames.length; i &#x3C; len ; i++){
  var collectionName = collectionNames[i];
   if(collectionName.endsWith('transformLog')||collectionName.endsWith('DataVersion')){ 
   print(collectionName); 
   db[collectionName].drop() 
   } 
 }</code></pre><p><code></code></p>                                                                                                                                                                                                                                                                                                                                                                                                                                                  |
|                                          |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
|                                          |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
|                                          |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
|                                          |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
|                                          |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
|                                          |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |

