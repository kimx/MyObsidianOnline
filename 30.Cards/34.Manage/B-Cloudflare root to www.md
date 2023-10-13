---
aliases : []
created: 2023-08-09
updated: 2023-08-09
type: blog
status: 🟩
publish: true
---
### Metadata
Tags:: #🗂️/🌲
Topics:: [[DNS]] [[Notion]] [[BlogNote]]

# 前言
工作有一需求，需要將root 導向www，例如: kimx.info to www.kimx.info 。此方式個人知道的解決方式，有2種:
1. 在IIS設定Rewrite。
2. 在DNS 服務商設定 (本文針對Cloudflare)。ps: 要看是否有支援。
# 使用方式
1. 如下圖，設定root 並啟用代理，此為給Cloudflare的Page Rule轉發用。
![upgit_20230809_1691557770.png](https://raw.githubusercontent.com/kimx/ObsidianAssets/master/2023/08/upgit_20230809_1691557770.png)

2. 設定Page Rule 將root 轉到www
![upgit_20230809_1691557697.png](https://raw.githubusercontent.com/kimx/ObsidianAssets/master/2023/08/upgit_20230809_1691557697.png)
# 總結
- 這樣的設定比去IIS設定方便許多，省下Rewrite及Bining等設定，也比較好管理。

# 相關參考
- https://developers.cloudflare.com/support/page-rules/configuring-url-forwarding-or-redirects-with-page-rules/

