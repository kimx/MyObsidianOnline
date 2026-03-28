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
- 續前一篇 [Docker Image To GCP Cloud Run](https://note.kimx.info/2026/03/docker-image-to-gcp-cloud-run.html)
- 本文記錄，將一個.NET Web程式，使用docker image放到Azure Container上。
- 由於Azure Container Registry，沒有免費的，本文採docker hub的方式(有免費額度)
	- ps: GCP Azure Container，有每月前0.5G

# 使用方式

## 推送到Docker Hub
- 先到docker.com 註冊帳號
	- 用command 登入，或直接用docker for window登入
```
docker login
```

- Build image
```
docker build -f AzureConatinerLab/Dockerfile -t azurecontainerlab .
```
- 標記並推送到 Docker Hub 
```
docker tag azurecontainerlab:latest kimxinfo/azurecontainerlab:latest
docker push kimxinfo/azurecontainerlab:latest
```
## Azure Container App
- 建立 Container App，輸入Hub上的image
	- ![upgit_20260328_1774685251.png](https://raw.githubusercontent.com/kimx/ObsidianAssets/master/2026/03/upgit_20260328_1774685251.png)
- 設定 Ingress
	- ![upgit_20260328_1774685301.png](https://raw.githubusercontent.com/kimx/ObsidianAssets/master/2026/03/upgit_20260328_1774685301.png)
- 完成後，Overview 可以使用Application Url瀏覽
	- ![upgit_20260328_1774685472.png](https://raw.githubusercontent.com/kimx/ObsidianAssets/master/2026/03/upgit_20260328_1774685472.png)

## 其他
- 如果希望服務閒置時不持續計費，可以保留 `Min replicas = 0`
	- ![upgit_20260328_1774685603.png](https://raw.githubusercontent.com/kimx/ObsidianAssets/master/2026/03/upgit_20260328_1774685603.png)
## 免費額度
- **請求次數**：每月前 **200 萬次** 請求免費。
- **CPU 資源**：每月前 **180,000 vCPU-秒** 免費。
- **記憶體資源**：每月前 **360,000 GiB-秒** 免費。
- **特點**：支援「縮減至零 (Scale to Zero)」，沒流量時不計費。
# 總結
- 本文重點是 Docker Hub + Azure Container App 的串接
# 相關參考
- [Docker Image To GCP Cloud Run](https://note.kimx.info/2026/03/docker-image-to-gcp-cloud-run.html)

