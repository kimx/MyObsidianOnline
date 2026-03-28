---
aliases: []
created: 2026-03-28
updated: 2026-03-28
type: blog
status: 🟥️
publish: true
tags:
  - 🗂️/🌲
topics:
---
# 前言
- 本文記錄，將一個.NET Web程式，使用docker image放到Cloud run上。

# 使用方式
## 本地初始化環境
- 安裝GCP CLI
```
(New-Object Net.WebClient).DownloadFile("https://dl.google.com/dl/cloudsdk/channels/rapid/GoogleCloudSDKInstaller.exe", "$env:Temp\GoogleCloudSDKInstaller.exe")

& $env:Temp\GoogleCloudSDKInstaller.exe
```
-  裝完後，會接著要你登入及選擇預設的專案(畫面..略)
- 啟用必要的 GCP 服務
```
gcloud services enable run.googleapis.com cloudbuild.googleapis.com
```
## Google Consle
- 建立 Artifact Registry repo
	- ![upgit_20260328_1774682191.png](https://raw.githubusercontent.com/kimx/ObsidianAssets/master/2026/03/upgit_20260328_1774682191.png)
	
- 設定 Docker 對 GCP Registry 的驗證
```
gcloud auth configure-docker asia-east1-docker.pkg.dev
```
-  Build image
```
docker build -f MondayAr/Dockerfile -t mondayart100 .
```
- 標記並推送 image 到 Artifact Registry
```
# 標記 image
docker tag mondayart100 asia-east1-docker.pkg.dev/gen-lang-client-xxxxx/monday-ar-t100/mondayart100:latest

# 推送至 GCP
docker push asia-east1-docker.pkg.dev/gen-lang-client-xxxxx/monday-ar-t100/mondayart100:latest
```
- 在 Cloud Run 建立服務，並選擇 Artifact Registry 裡的 image
	- ![upgit_20260328_1774682622.png](https://raw.githubusercontent.com/kimx/ObsidianAssets/master/2026/03/upgit_20260328_1774682622.png)
	- 設定個數量下限0，閒置不算費用。Ingress允許網路使用
		- ![upgit_20260328_1774682240.png](https://raw.githubusercontent.com/kimx/ObsidianAssets/master/2026/03/upgit_20260328_1774682240.png)
- 設定 `.env` 或其他環境變數
	- ![upgit_20260328_1774682743.png](https://raw.githubusercontent.com/kimx/ObsidianAssets/master/2026/03/upgit_20260328_1774682743.png)
- 完成，在服務可以取得網址
	- ![upgit_20260328_1774682847.png](https://raw.githubusercontent.com/kimx/ObsidianAssets/master/2026/03/upgit_20260328_1774682847.png)
## 後續更新
- 之後image更新，一樣先Build Image再標記並推送 image 到 Artifact Registry後。使用下列命令更新
```
gcloud run deploy mondayart100 --image asia-east1-docker.pkg.dev/gen-lang-client-xxxxx/monday-ar-t100/mondayart100:latest --region asia-east1
```
- ps: 也可以到Google Console設定。
# 總結
- 環境配置與授權、Docker 映像檔管理、Cloud Run 服務部署、版本更新機制。
- 本文不是AI寫的...。

# 相關參考
- [使用 Google Cloud CLI 安裝程式](https://docs.cloud.google.com/sdk/docs/downloads-interactive?hl=zh-tw)
