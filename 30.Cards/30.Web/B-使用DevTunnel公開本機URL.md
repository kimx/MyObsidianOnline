---
aliases: 
created: 2023-10-13
updated: 2023-10-13
type: blog
status: 🟩
tags:
  - 🗂️/🌲️
topics:
  - "[[Visual Studio]]"
publish: true
---
# Foreword
- 使用微軟提供的Dev Tunnels取代之前使用NGROK的方式，將本機開發的URL公開在外部網路。
- 此方式為方便與外部服務整合測試，例如:LineAPI
- Dev Tunnels 有2種使用方式，以下會介紹何使用

# 1. Visual Studio 2022 .NetCore程式
- 內建就有Dev Tunnels功能，第一次使用先建立tunnels![upgit_20231013_1697163135.png](https://raw.githubusercontent.com/kimx/ObsidianAssets/master/2023/10/upgit_20231013_1697163135.png)
![upgit_20231013_1697163277.png](https://raw.githubusercontent.com/kimx/ObsidianAssets/master/2023/10/upgit_20231013_1697163277.png)

- 選擇建立好的通道，執行網頁即會出現外部URL![upgit_20231013_1697163356.png](https://raw.githubusercontent.com/kimx/ObsidianAssets/master/2023/10/upgit_20231013_1697163356.png) ![upgit_20231013_1697163381.png](https://raw.githubusercontent.com/kimx/ObsidianAssets/master/2023/10/upgit_20231013_1697163381.png)

# 2. 非.Net Core程式 (.Net Framework)

## 安裝 dev tunnels 程式
- 裝完後**重開機**，環境變數位罝才會生效
```
winget install Microsoft.devtunnel
```

## 登入
- 第一次使用，需要登入Github或微軟帳號
```
devtunnel user login
```
- ![upgit_20231013_1697160121.png](https://raw.githubusercontent.com/kimx/ObsidianAssets/master/2023/10/upgit_20231013_1697160121.png)
- 執行本機程式，<font color="#ff0000">http</font> port 50893 ps:**不能使用<font color="#ff0000">https**</font> 
   ![upgit_20231013_1697162566.png](https://raw.githubusercontent.com/kimx/ObsidianAssets/master/2023/10/upgit_20231013_1697162566.png)

- 執行devtunnel 將本機程式公開，並允許匿使用者可以瀏覽
```
devtunnel host -p 50893 --allow-anonymous
```
- 執行後，取得公開的URL，大功告成
  ![upgit_20231013_1697162746.png](https://raw.githubusercontent.com/kimx/ObsidianAssets/master/2023/10/upgit_20231013_1697162746.png)

	- 進入後按Continue 
	  ![upgit_20231013_1697162714.png](https://raw.githubusercontent.com/kimx/ObsidianAssets/master/2023/10/upgit_20231013_1697162714.png)
	- ![upgit_20231013_1697165346.png](https://raw.githubusercontent.com/kimx/ObsidianAssets/master/2023/10/upgit_20231013_1697165346.png)


# Reference
- [Dev Tunnels Visual Studio in 10 Minutes or Less](https://www.youtube.com/watch?v=kdaHwOkQf7c)
- [[@David]] [董大偉使用DevTunnel取代NGROK](https://www.youtube.com/watch?v=vrHz75qNQik)