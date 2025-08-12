---
aliases: 
created: 2025-05-29
updated: 2025-05-29
type: card
status: 🟩
tags:
  - 🗂️/🌱️
topics:
  - "[[VsCode]]"
  - "[[AI]]"
  - "[[Github]]"
publish: true
---
# Foreword
- 使用Github Copilot，以加入SQL Server MCP 為例
# Content
- CTRL+SHIFT+P: 進入Command
- MCP Add Server
	- 選NPM Package
	- 輸入: @donggyunryu/mcp-sql
		- [從這裡取得](https://mcp.so/server/mcp-sql-server/ryudg?tab=tools)
	- 輸入資料庫連線資訊
	- 最後問你要設存儲存設定，user/workspace，這裡選後者，在此專案使用就好。
	- 在.vscode目錄會產生mcp.json
- 最後切換到agent mode，會看到工具圖示裡的功能清單
	- ![[Pasted image 20250529150219.png]]
# Question
- 

# Other
- 一開始測試連本機會失敗，localhost可以連，但localhost, 1433不行，解決方式，將Server的TCP/IP打開
	- "C:\Windows\SysWOW64\SQLServerManager14.msc"
- ![[Pasted image 20250529150425.png]]

# Reference
- https://www.youtube.com/watch?v=dutyOc_cAEU