---
aliases:
created: 2025-12-22
updated: 2025-12-22
type: card
status: 🟩
tags:
  - 🗂️/🌱️
topics:
publish: true
---
# Foreword
- 在使用 Cursor/反重力 開發時遇到 GPU 占用 100% 的情況

# Content
- 關閉「硬體加速」可以強制 Cursor 不使用顯卡渲染介面。

1. 在 Cursor 中按下 `Ctrl + Shift + P` 。
2. 輸入 **`Preferences: Configure Runtime Arguments`** 並Enter。
3. 這會開啟一個 `argv.json` 檔案。
4. 去掉前面的註解符號 disable-hardware-acceleration，確保內容如下：
``` json
{
    "disable-hardware-acceleration": true
}
```
