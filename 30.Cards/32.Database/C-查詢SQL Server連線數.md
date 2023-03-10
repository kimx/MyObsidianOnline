---
aliases : []
created: 2023-02-14
updated: 2023-02-14
type: card/blog
status: 🟩
---
### Metadata
Tags:: #🗂️/🌱️
Topics:: [[SqlServer]]


# Foreword
- 測試Dapper在AddScope時,先打開連線時，會不會殘留時，查詢連線數。
	- 在AddScope時Open在結束時會自動dispose，跟using一致，已驗證過連線數。

# Content
- 查詢連線數
```
SELECT DB_NAME(dbid) as DBName,
       COUNT(dbid) as NumberOfConnections      
FROM sys.sysprocesses
WHERE dbid > 0
GROUP BY dbid, loginame
```
- 查詢連線數Join資料庫名稱
```
select a.dbid,b.name, count(a.dbid) as TotalConnections
from sys.sysprocesses a
inner join sys.databases b on a.dbid = b.database_id
group by a.dbid, b.name
```
- 查詢某一資料庫的連線資訊
```
SELECT DB_NAME(dbid) as DBName,login_time,last_batch,program_name,hostname,loginame,status
FROM sys.sysprocesses
WHERE DB_NAME(dbid)='MTG_Financial_DEV'
order by dbid;
```

# See Also
- 

# Reference
- [SQL Query to Check Number of Connections on Database](https://social.technet.microsoft.com/wiki/contents/articles/22702.sql-query-to-check-number-of-connections-on-database.aspx)