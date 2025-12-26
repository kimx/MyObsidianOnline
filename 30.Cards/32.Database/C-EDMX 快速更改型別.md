---
aliases:
created: 2025-08-12
updated: 2025-08-12
type: card
status: 🟩
tags:
  - 🗂️/🌱️
topics:
  - "[[EF6]]"
  - "[[EDMX]]"
publish: true
---
# 前言
- 日前遇到某一資料表從int 改成numberic，透過edmx自動更新，無法反映回來，只能刪除整個資料表，再重加回來，費力又耗時。
# 解決方式
- 直接用notepad打開，手動修改XML，搜尋資料表關鍵字用EntityType Name="POGRVLN" 搜尋
- 第一個位置在edmx:StorageModels，找到欄位直接修改型別，將int改成numberic
```XML
 <Property Name="QTY" Type="numeric" Precision="12" Scale="3" />
```
![upgit_20250812_1754959337.png](https://raw.githubusercontent.com/kimx/ObsidianAssets/master/2025/08/upgit_20250812_1754959337.png)

- 第二個位置在edmx:ConceptualModels下，將Int32改成Decimal
```XML
<Property Name="QTY" Type="Decimal" Precision="12" Scale="3" />
```
![upgit_20250812_1754959156.png](https://raw.githubusercontent.com/kimx/ObsidianAssets/master/2025/08/upgit_20250812_1754959156.png)

- View 也是同上處理，但前提是View要先Alter一次，型別才會變更。