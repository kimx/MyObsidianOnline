---
aliases : []
created: 2023-07-18
updated: 2023-07-18
type: blog
status: 🟩
publish: true
---
### Metadata
Tags:: #🗂️/🌲
Topics::  [[Deploy]] [[Visual Studio]] [[Github]]

# 前言
目前開發的專案，發行工作大部分是由CI來處理，但在某些狀況下，為求快速，會直接在Visual Studio上，發行到測試主機上。天下武功、唯快不破......，但"快"容易打破碗。

今天同事A，在本機發行時，並未取得遠端開發分支來合併，導致同事B在測試時，發生鬼打牆事件。為避免之後還有此情況，在發行檔案內，加了一個發行前，先取得分支來合併的設定。

# 使用方式
打開.pubxml 增加如下
```
  <PropertyGroup>
  .......以上略
    <PipelineDependsOn>
      CustomActionsBeforeBuild;
      $(PipelineDependsOn);
    </PipelineDependsOn>
  </PropertyGroup>

  <Target Name="CustomActionsBeforeBuild" BeforeTargets="BeforeBuild">
    <Message Text="********************************** BeforeBuild-發行前 取得遠端Main，合併到目前分支 ***********************************" Importance="high"/>
    <Exec Command="git merge origin/main"/>
  </Target>
```

# 測試
發行程式，在"輸出"視窗，可以看到在建置時，觸發了commad的訊息。
![upgit_20230718_1689663883.png](https://raw.githubusercontent.com/kimx/ObsidianAssets/master/2023/07/upgit_20230718_1689663883.png)


# 總結
- 只要是人為的操作，難免會有操作錯誤的行為，所以可以透過設定自動化來解決的工作，可以省下日後不少麻煩。

# 相關參考
- https://stackoverflow.com/questions/35688836/how-to-redirect-powershell-errors-in-pubxml-file-to-error-window
- Github [原始檔下載](https://github.com/kimx/PublishBeforeBuildLab)
