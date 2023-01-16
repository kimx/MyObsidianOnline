---
aliases : []
created: 2023-01-13
updated: 2023-01-13
type: blog
status: 🟩
publish: true
---
### Metadata
Tags:: #🗂️/🌲
Topics:: [[Obsidian]] [[線上資源]]

# 前言
寫好的Obsidian 筆記想要公開在網站分享給別人，目前我使用的有幾種方式:
1. EverNote。
2. Notion。
3. Blogger。
以上三種在過程中，都需要一些小調整。若筆記有修改，除了Blogger會更新，通常也不會再去更新已分享出去的筆記。 若不想要那麼麻煩，Obsidian也有付費方式，可以發行。

參考此篇[10個如何將Obsidian公開在網路](https://beingpax.medium.com/7-obsidian-publish-alternatives-to-publish-your-notes-online-for-free-33db4fb06f5)，選定了一個功能較完整的版本，例如支援: Graphic 、左方選單、筆記之間的連結等。

# 架構
- 使用Netlify靜態網站，免費、支援自訂網域。
	- 個人使用起來比Github Page好用，易上手。
- 網站樣板[obsidian-zola](https://github.com/ppeetteerrs/obsidian-zola/tree/main)，透過javascript，將Obsidian筆記變成Html網頁顯示。
- Github，你的Obsidian儲存庫。
	- 你原本的Obsdian不用作修改，只需加一個netlify.toml即可。

# 使用方式
1. 在Github建一個新的Repository，將你Obsidian要公開的筆記及.obsidian資料夾複製過來，並新增檔案**Home.md**及**netlify.toml**，如下圖所示
- ![upgit_20230116_1673834658.png](https://raw.githubusercontent.com/kimx/ObsidianAssets/master/2023/01/upgit_20230116_1673834658.png)
- Home.md 不用修改，只是作為入口首頁。
- neltify.toml 修改參數:
	- REPO_URL : Github 位置
	- SITE_URL: netlify的URL
```
[build]
command = "rm -rf __obsidian __site && mkdir __obsidian && mv * __obsidian || true && git clone https://github.com/ppeetteerrs/obsidian-zola.git __site && __site/run.sh"
publish = "public"

[build.environment]
LANDING_BUTTON = "進入我的大腦"
LANDING_TITLE = "首頁標題"
LANDING_DESCRIPTION = "首頁副標題"
# 首面的筆記名稱
LANDING_PAGE = "home"
PYTHON_VERSION = "3.8"
# 你的Github儲存庫
REPO_URL = "https://github.com/kimx/NetlifyObsidianLab"
SITE_TITLE = "網站標題"
# (Optional) Site title in browser tab (leave blank to use SITE_TITLE)
SITE_TITLE_TAB = "Kimxinfo"
# (REQUIRED) Netlify site URL
SITE_URL = "https://kimxinfo-netlifyobsidianlab.netlify.app/"
# (Optional) Site Timezone
TIMEZONE = "Asia/Hong_Kong"
ZOLA_VERSION = "0.15.2"
SORT_BY = "title"
# (Optional) Google Analytics Measurement ID
GANALYTICS = ""
# (Optional, default true) Slugify URLs. Put "" to disable.
SLUGIFY = "y"
# (Optional, default true) Shows knowledge graph on home page. Put "" to disable.
HOME_GRAPH = "y"
# (Optional, default true) Shows knowledge graph on every page. Put "" to disable.
PAGE_GRAPH = "y"
# 左方選單是否展開
SIDEBAR_COLLAPSED = ""
# 頁尾資訊
FOOTER = ""
# (Optional, default main) Root section name.
ROOT_SECTION_NAME = "main"
# (Optional) visjs graph options. Can remove if desired.
GRAPH_OPTIONS = """
        {
        	nodes: {
        		shape: "dot",
        		color: isDark() ? "#8c8e91" : "#dee2e6",
        		font: {
        			face: "Inter",
        			color: isDark() ? "#c9cdd1" : "#616469",
        			strokeColor: isDark() ? "#c9cdd1" : "#616469",
        		},
        		scaling: {
        			label: {
        				enabled: true,
        			},
        		},
        	},
        	edges: {
        		color: { inherit: "both" },
        		width: 0.8,
        		smooth: {
        			type: "continuous",
        		},
        		hoverWidth: 4,
        	},
        	interaction: {
        		hover: true,
        	},
        	height: "100%",
        	width: "100%",
        	physics: {
        		solver: "repulsion",
        	},
        }
        """
```

2. 使用Github註冊[Netlify](https://www.netlify.com/)，加入新網站，選擇匯入來源Github![upgit_20230113_1673594927.png](https://raw.githubusercontent.com/kimx/ObsidianAssets/master/2023/01/upgit_20230113_1673594927.png)
- 匯進去時，會自動配給你一個URL，可以在Site settings修改，或者是使用你自己的Domain。![upgit_20230113_1673595030.png](https://raw.githubusercontent.com/kimx/ObsidianAssets/master/2023/01/upgit_20230113_1673595030.png)
- 本文設定為kimxinfo-netlifyobsidianlab，URL為https://kimxinfo-netlifyobsidianlab.netlify.app/，此URL要回填到neltify.toml的**SITE_URL**參數上。
3. 簽入Github後，會觸發建置，成功後自動部署。![[Pasted image 20230113153610.png]]
4. 檢視網站，點中間Button進入首頁![upgit_20230113_1673595449.png](https://raw.githubusercontent.com/kimx/ObsidianAssets/master/2023/01/upgit_20230113_1673595449.png)
![upgit_20230113_1673595512.png](https://raw.githubusercontent.com/kimx/ObsidianAssets/master/2023/01/upgit_20230113_1673595512.png)
ps: 小小缺點，左方選單，只會有一層，所有子目錄，都會被拉到第一層，無法搜尋中文。

# 總結
 - 透過這樣的方式，可以更快速、更方便管理Obsidian的分享筆記。
 - 可以在網頁上，使用大部分Obsidian的功能。

# 其他
- Netlify自訂Domain，[參考此篇](https://docs.netlify.com/domains-https/custom-domains/configure-external-dns/#configure-a-subdomain)，加一筆cname到dns。

# 相關參考
- [netlify 超佛心的靜態網站hosting服務](https://blog.alantsai.net/posts/2018/07/migrate-blog-to-ssg-demo-devops-8-netlify-free-static-site-hosting-service)
- [此筆記的Github位置](https://github.com/kimx/NetlifyObsidianLab)

# 您可能也會有興趣的其他文章
- [[C-我的Obsidian筆記使用方式]]