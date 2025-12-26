---
created: 2025-12-25
updated: 2025-12-25
status:
tags:
  - ✅/🟨
topics:
  - "[[react]]"
  - "[[2025]]"
keywords:
publish: true
---
# 學習來源
- https://www.youtube.com/watch?v=aBTiZfShe-4
# 已實作範例
- https://github.com/kimx/my-react-todo
# 如何開始
## 建立專案
```
npm create vite@latest my-react-app -- --template react
或是用選技術、語言，


# 進入資料夾
cd my-react-app
```
## 安裝與執行

```
# 安裝所有依賴組件（採購員開始幹活）
npm install

# 啟動開發伺服器
npm run dev

```
# 開發工具
- 使用Cursor / VScode都可以
## 安裝套件
```
ES7+ React/Redux/React-Native snippets
ESLint
React Native Tools
```
## 啟用偵錯
- vscode目錄建立2個檔案
### tasks.json
```
{
	"version": "2.0.0",
	"tasks": [
		{
			"label": "npm: dev",
			"type": "shell",
			"command": "npm run dev -- --port 3000",
			"problemMatcher": [],
			"detail": "執行 npm run dev 啟動開發伺服器（端口 3000）",
			"options": {
				"cwd": "${workspaceFolder}"
			},
			"group": {
				"kind": "build",
				"isDefault": true
			}
		},
		{
			"type": "npm",
			"script": "dev",
			"problemMatcher": [],
			"label": "npm: dev",
			"detail": "vite"
		}
	]
}
```
### launch.json
1. 上方功能列 Run/ Add Configuration : launch chrome，內容如下
```
{
    // Use IntelliSense to learn about possible attributes.
    // Hover to view descriptions of existing attributes.
    // For more information, visit: https://go.microsoft.com/fwlink/?linkid=830387
    "version": "0.2.0",
    "configurations": [
        {
            "name": "Launch Chrome",
            "request": "launch",
            "type": "chrome",
            "url": "http://localhost:3000",
            "webRoot": "${workspaceFolder}",
            "preLaunchTask": "npm: dev"
        }
    ]
}
```
# 重點記錄
- Class 元件，已過時，現在都用Functional 元件
- userEffect: Init,變動事件
- 
# 其他
- 30天學習: https://www.youtube.com/watch?v=Vg2R57g4J0g&list=PLdJUpeaDa6nz9Y3l6TR7XGQHXYorsqXv-&index=14