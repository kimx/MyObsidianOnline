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
# Foreword
- Google 發布 Conductor，這是一款專為 Gemini CLI 設計的擴充套件，引入 Context-Driven Development ，把「共識」變成文件，讓每個人都在共識下 vibe 。
- 核心理念：先規劃，再建構。將專案上下文從聊天視窗抽離，轉化為持久保存在程式碼庫中的 Markdown 文件。📋

# 如何開始
確保已安裝 Conductor 擴充功能

```
gemini extensions install https://github.com/gemini-cli-extensions/conductor
```

1. 建立專案並初始化專案上下文
```
mkdir my-new-project
cd my-new-project

/conductor:setup
```

2 輸入需求描述，會引導你定義
- Product: 定義產品目標與用戶。
- Tech Stack: 指定你要使用的程式語言、資料庫與框架。
- Workflow: 設定團隊規範（例如是否使用 TDD 測試驅動開發）。
- 執行後產生的變化： Conductor 會自動在你的目錄中建立一個 conductor/ 資料夾，內含 product.md、tech-stack.md 等 Markdown 檔案。這些檔案讓 AI 之後能精確遵循你的要求。

3. 開始第一個工作，輸入如下，會請你輸入需求，並建立plan檔案

```
/conductor:newTrack
```
4. 確認後，開始實作
```
/conductor:implement
```
# See Also
- [[C-Gemini CLI]]

# Reference
- [Google Conductor Github](https://github.com/gemini-cli-extensions/conductor)
- [影片教學](https://www.youtube.com/watch?v=8BU92hInOsY)