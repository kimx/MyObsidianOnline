---
aliases : []
created: 2023-01-11
updated: 2023-01-11
type: blog
status: 🟩
publish: false
---
### Metadata
Tags:: #🗂️/🌲 
Topics:: [[git]] [[BlogNote]]

# 前言
你是否會常commit了變更後，發現少寫了什麼或某段程式寫錯了，然後就會修改後，再commit一次，假設你又跟我一樣常犯傻，剛的情況又來一次的話， list就會長得如下3個commit，多了v2,v3 。![upgit_20230111_1673418098.png](https://raw.githubusercontent.com/kimx/ObsidianAssets/master/2023/01/upgit_20230111_1673418098.png)

# 解決方式
針對commit了，又後悔想修改的話，針對幾個情境的解決方式。
## 1. 修改/新增併入最近的commit
接續**前言**述，最近的commit為"訂單新增API v3"，如圖，我想再將修改內容，併入v3的commit。![upgit_20230111_1673418942.png](https://raw.githubusercontent.com/kimx/ObsidianAssets/master/2023/01/upgit_20230111_1673418942.png)

### 使用方式
1. 將修改的先加入暫存區 (同Visual Studio 加入到stage)
>git add --all

2. 簽入加上參數 --amend --no-edit
> git commit --amend --no-edit
- --amend: 將暫存區的加入最近一次的commit
- --no-eidt: 不需要commit message
commit沒有增加，但內容已由v3變成 **v3-1**
![upgit_20230111_1673419666.png](https://raw.githubusercontent.com/kimx/ObsidianAssets/master/2023/01/upgit_20230111_1673419666.png)

## 2.修改最近commit的訊息
有時簽入時，才發現訊息寫錯了，想修改該如何做? 本例示範將"訂單新增API v3" 改成"訂單新增API v3 **OK**"
### 使用方式
簽入加上參數 --amend  **-m** 參數
>git commit --amend -m "訂單新增API v3 OK"

一樣是3個commit，但最後一個訊息已加上"OK"

![upgit_20230111_1673420127.png](https://raw.githubusercontent.com/kimx/ObsidianAssets/master/2023/01/upgit_20230111_1673420127.png)

## 注意事項
上述的兩種方式，其實都是撒掉前一次的commit，再換一個新的commit，仔細看的話，ID是不一樣的。在本地的commit可以任意使用，但針對**已push出去的commit**，儘量**不要這樣用**，以免造成別人在處理衝突的困擾。

# 總結
以上兩個指令，可以大量減少一些不必要的commit，讓整個歷史記錄更清楚明瞭。

# 相關參考
- [git 修改歷史訊息](https://note.kimx.info/2020/12/git.html)


