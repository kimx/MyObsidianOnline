---
aliases: []
created: 2023-09-08
updated: 2023-09-08
type: MOC
status: 🟩
publish: true
tags:
  - 🗺️
topics:
---

# 基本資訊
- 清理Log
```
--https://itorz324.blogspot.com/2019/09/sql-server-logbig-ldf-file.html
USE MTG_Financial_DEV;
GO
-- changing the database recovery model to simple.
ALTER DATABASE MTG_Financial_DEV
SET RECOVERY SIMPLE;
GO
-- Shrink UserDB_log file to 20 MB.
DBCC SHRINKFILE (MTG_Financial_log, 20);
GO
-- changing the database recovery model to FULL.
ALTER DATABASE MTG_Financial_DEV
SET RECOVERY FULL;
GO
```

## 查詢預存的資訊
```
--查詢預存程序的參數（Parameters）
SELECT
    p.name AS ParameterName,
    TYPE_NAME(p.user_type_id) AS DataType,
    p.max_length,
    p.is_output
FROM sys.parameters p
INNER JOIN sys.objects o ON p.object_id = o.object_id
WHERE o.type = 'P'  -- 'P' 表示 Stored Procedure
  AND o.name = 'VCALENDAR_Query'
  AND SCHEMA_NAME(o.schema_id) = 'dbo'

--查詢預存程序的回傳欄位資訊（結果集欄位）
--ps: 動態的SQL無法使用
SELECT 
    name AS ColumnName,
    system_type_name AS DataType,
    is_nullable
FROM sys.dm_exec_describe_first_result_set(N'dbo.VCALENDAR_Query', NULL, 0);

```

# 效能
- [更新統計資訊 Statistics](https://chat.openai.com/share/da6476b5-e1b2-48c6-a5e5-43a1ee46b429) [[@Robin]]
	- [https://youtu.be/5Ti75MZ_Pr0?si=Bo0Im6Ks_x81eHrt](https://youtu.be/5Ti75MZ_Pr0?si=Bo0Im6Ks_x81eHrt "https://youtu.be/5Ti75MZ_Pr0?si=Bo0Im6Ks_x81eHrt")