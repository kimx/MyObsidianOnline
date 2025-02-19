---
aliases : []
created: 2023-03-31
updated: 2023-03-31
type: MOC
status: 🟩
publish: true
---
### Metadata
- Tags:: #🗺️
- Topics:: 

# 指令
- 強制覆蓋本地的分支
```
git pull -f origin kim-whitebox-2:kim-whitebox-2
```
- 關於hotfix to develop : 參考chatgpt，試用rebase及cherry-pickup後，cherry-pickup的方式會比較好理解、操作，歷史資訊也比較容易懂。
	- [[B-git 挑選特定commit合併]]
# 其他
- https://cynthiachuang.github.io/Git-Force-to-Push-Commit-to-a-Remote-Repository-and-Overwrite-Local-Repository/
# 救回已刪除的分支
- [[2025-01-03]] : 目前在Visual Studio的git介面，有設定遠方分支刪除時，在取得版本，本地對應的分支也會刪除。
	- 昨天以為有一分支沒有用，就把它刪除了，後來發現需要它時，試了一堆方式救不回來。
	- 最後想到，在CI上有取得該分支發行過，遠端進ap1後，使用git checkout 該分支，成功救回。 
- 後記:後來發現[Azure Devops有救回功能](https://learn.microsoft.com/zh-tw/azure/devops/repos/git/restore-deleted-branch?view=azure-devops)...
