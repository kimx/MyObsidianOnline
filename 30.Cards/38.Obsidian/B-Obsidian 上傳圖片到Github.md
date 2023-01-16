---
aliases : []
created: 2023-01-05
updated: 2023-01-05
type: blog
status: 🟩
publish: true
---
### Metadata
Tags:: #🗂️/🌲
Topics:: [[BlogNote]] [[Obsidian]]

# 前言
在Obsidian將複製的圖片貼到筆記裡時，照預設的方式，會放到相對應或你指定的本機目錄內。目前有些筆記需要分享出去或公開的Blog，在轉出去的過程，針對那些在本機的圖片，需要再處理一次，轉成網路的位置，處理一次就令我頭痛了。所以之後的筆記只要是插入圖片，都是來自網路資源。

插入來自網路圖片，代表著勢必要先上傳到網路某個空間，且支援公開的靜態資源，然後取得URL，再放到筆記內.....這個作法，太土炮，作個幾次，就想翻筆電了XD。
本文會介紹如何在寫筆記的過程，將複製的圖片貼到筆記時，先上傳圖片到Github上，並取得圖片在Github上公開的URL，貼到筆記內。

# 如何使用
## 前置設定
1. 先到Gitthub建立一個respository，本文: ObsidianAssets。
2. 到 [Github個人設定](https://github.com/settings/tokens)，建立Token ，只會顯示1次，要保存好。
	- ![upgit_20230105_1672907943.png](https://raw.githubusercontent.com/kimx/ObsidianAssets/master/2023/01/upgit_20230105_1672907943.png)

 3. [下載Upgit](https://github.com/pluveto/upgit/releases)，upgit_win_amd64.exe(windows)，放到你指定的位置，例如:D:\obsiaian\tools\upgit.exe
 4. 在剛的位置，新增新增config.toml，並將github的資訊填入

``` 
# 預設上傳者
default_uploader = "github" 
# 圖片位置設定
rename = "{year}/{month}/upgit_{year}{month}{day}_{unix_ts}{ext}" 
[output_formats] 
"bbcode" = "[img]{url}[/img]" 
"html" = '<img src="{url}" />' 
"markdown-simple" = "![]({url})" 

# Github 上傳者
[uploaders.github] 
# 保存文件的分支，例如 master 或 main 
branch = "master" 

pat = "你的Token" 
# 您的respository 
repo = "ObsidianAssets" 
# 您的 Gtihub 用户名  
username = "kimx"
```
5. 設定好後，先測試command，是否可以上傳，成功的話，會以markdown格式存在你的剪貼簿上。
```
D:\obsiaian\tools\upgit.exe :clipboard -f markdown
```

## Obsidian設定
1. 安裝PlugIn : Shell Command。
2. 設定Shell 
	- 設定Commnad ![[Pasted image 20230105165541.png]]
	- 點選工具圖示，設定Output，指定到目前位置 ![upgit_20230105_1672909056.png](https://raw.githubusercontent.com/kimx/ObsidianAssets/master/2023/01/upgit_20230105_1672909056.png)

	- 最後指定快捷鍵ALT+ V ![upgit_20230105_1672909124.png](https://raw.githubusercontent.com/kimx/ObsidianAssets/master/2023/01/upgit_20230105_1672909124.png)
3. 大功告成，此時你按ALR+V就可以直接將剪貼簿的圖片，上傳到github上，並以markdown格式插入，如下圖。![upgit_20230105_1672909375.png](https://raw.githubusercontent.com/kimx/ObsidianAssets/master/2023/01/upgit_20230105_1672909375.png)


# 總結
透過這樣的方式，未來你的筆記，只要是有支援markdown格式的，就可以無痛接軌的分享出去。ps:本文的圖片也是以**此方式上傳**的。

# 其他
- 一個Repository限制5G，但這是寫強烈建議，一般建議是1G以下。

# 參考來源
- [文章](http://jdev.tw/blog/6982)
- [影片教學](https://www.youtube.com/watch?v=nGII-khqm2o)