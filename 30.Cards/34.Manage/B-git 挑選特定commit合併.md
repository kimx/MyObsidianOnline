---
aliases: 
created: 2024-08-28
updated: 2024-08-28
type: blog
status: 🟩
publish: true
---
### Metadata
Tags:: #🗂️/🌲 
Topics:: [[git]] [[BlogNote]]

# 前言
  - 目前的專案，git分支，切分為如下:
	- master : 由release併入，發行到PRD
	- release : 由develop併入，發行到QAS
	- develop : 由個別開發者併入。
- 問題來了! 這兩天併入到release的變更，只想挑最上方那一筆併入到master，其他的不可以併入。如下圖所示:
   ![upgit_20240828_1724824420.png](https://raw.githubusercontent.com/kimx/ObsidianAssets/master/2024/08/upgit_20240828_1724824420.png)

# 解決方式
- 使用cherry-pick 挑選某一筆的commit併入。
## 使用方式
1. 切換到master 或master checkout另一分支hoftix(本文使用此方式，可以避免操作錯誤，刪除就好) 。
2. 取得該筆的commit ID 8碼。
   ![upgit_20240828_1724825458.png](https://raw.githubusercontent.com/kimx/ObsidianAssets/master/2024/08/upgit_20240828_1724825458.png)

3. 在hotfix分支執行命令
```git
git cherry-pick e957cc4e
```
4. 完成畫面，只有Finished那筆commit併入
![upgit_20240828_1724825464.png](https://raw.githubusercontent.com/kimx/ObsidianAssets/master/2024/08/upgit_20240828_1724825464.png)

最後確認無誤的話，就可以從hotfix併入master。
# 總結
- cherry-pick 是一個很好的工具，可以幫助你精確地應用某些 commit，但在使用時需要小心，它不適合複雜的歷史操作，特別是處理依賴關係和衝突的情況。


