---
aliases:
created: 2025-12-26
updated: 2025-12-26
type: card
status: 🟩
tags:
  - 🗂️/🌱️
topics:
  - "[[Gemini]]"
  - "[[CLI]]"
publish: true
---
# 如何在 Windows 上使用？

在 Windows 上安裝 Gemini CLI 主要依賴 **Node.js** 環境。以下是具體步驟：

## 1. 安裝環境準備

你必須先安裝 **Node.js**（建議版本為 18 或 20 以上）：
- 前往 [Node.js 官網](https://nodejs.org/) 下載並安裝 **LTS 版本**。
- 安裝完成後，打開「命令提示字元 (CMD)」或「PowerShell」，輸入 `node -v` 確保安裝成功。
## 2. 安裝 Gemini CLI
在終端機中輸入以下指令進行全域安裝：
Bash
```
npm install -g @google/gemini-cli
```

## 3. 啟動與身份驗證

安裝完成後，直接輸入以下指令啟動：

Bash

```
gemini
```

啟動後，程式會引導你進行初始化：
- **選擇主題：** 選擇你喜歡的配色。
- **身份驗證：** 系統會詢問登入方式。
    
    - **選項 1 (Login with Google)：** 最推薦。使用個人 Google 帳號登入，通常有免費額度（每分鐘約 60 次請求，每天 1000 次）。
        
    - **選項 2 (API Key)：** 如果你有從 Google AI Studio 申請的 API Key，也可以選擇此項。
        
## 4. 開始使用

登入成功後，你就可以直接在終端機輸入問題。常用快捷操作包括：
- 輸入 `/help` 查看所有指令。
- 使用 `@` 符號來選取特定的本地檔案讓 Gemini 讀取。
- 輸入 `!` 切換到 **Shell 模式**，直接執行系統指令。