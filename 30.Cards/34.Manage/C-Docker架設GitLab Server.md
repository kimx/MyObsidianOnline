---
aliases : []
created: 2023-01-10
updated: 2023-01-10
type: card
status: 🟩
---
### Metadata
Tags:: #🗂️/🌱️
Topics:: [[DevOps]] [[Gitlab]] [[Docker]]
Links:: [[P-2023-01-專案-GitLab可行性測試]]

# Foreword
- Inspire by [[R-2023-01-09 Robin分享小朱devOps簡報]]
- 這篇記錄如何在Windows 11的Docker for Linux (Ubuntu)上安裝GitLab Server

# Content
## 1.建立docker-compose.yml
- GITLAB_OMNIBUS_CONFIG: 設定URL、root的密碼(<font color="#ff0000">強度要夠高</font>)及備份設定
- volumes : 設定與container對接的目錄位置
	- 本機Volume位置:  \\wsl.localhost\docker-desktop-data\data\docker\volumes
```
version: '3.6'
services:
  gitlab:
    hostname: GitLab
    restart: always
    environment:
      GITLAB_OMNIBUS_CONFIG: |
        external_url "http://localhost:8088/"
        gitlab_rails['initial_root_password'] = 'CK@kim28000543'
        gitlab_rails['manage_backup_path'] = true
        gitlab_rails['backup_path'] = "/var/opt/gitlab/backups"
        gitlab_rails['backup_archive_permissions'] = 0644
        gitlab_rails['backup_pg_schema'] = 'public'          
        gitlab_rails['backup_keep_time'] = 604800   
    ports:
      - "8088:8088"
      - "8089:22"
    volumes:
      - gitlab_config:/etc/gitlab
      - gitlab_logs:/var/log/gitlab
      - gitlab_data:/var/opt/gitlab
    image:
      gitlab/gitlab-ee:latest
volumes:
  gitlab_config:
  gitlab_logs:
  gitlab_data:
```
- 針對Volume的補充:分别2種
1. 使用絕對路徑，不使用冒號，使用最上層/是根目錄，如下範例
```
 services:
 ...
     volumes:
       - /d/dockers/data:/data    # D:/dockers/data = Docker的/data
````

2.使用相對的Volume，如下的Service內的VolumeName會使用在外層宣告VolumeName，其存放位罝在Docker的volume目錄內。
```
 services:
 ...
     volumes:
       - VolumeName:/data
volumes:
	VolumeName:
````

## 2.啟用image
- 在yml下的位置執行命令
>docker-compose up -d
- 此指令會自動下載image，完成後會啟用。

- 確認是否有下載成功
> docker-compose images

- 確認容器是否正在執行
> docker-compose ps

- 停止容器
> docker-compose stop gitlab

- 刪除容器 -v 含volume都移除
> docker-compose down -v

## 3.測試GitLab
- 瀏覽 http://localhost:8088/
	- root
	- CK@kim28000543
## 4.其他
- Q: Volume無法刪除?
- A: 容器先停止，在Docker Destop UI，重新啟動Docker，再停止容器並刪除，再去刪除Volume。 ps:不行刪的話，就再重新作一次剛的動作。

# Question
-   其他環境設定，例如SMTP等設定。

# See Also
- [[C-GitLab Runner On Windows]]

# Reference
- [[R-2023-01-10 在 Ubuntu 上使用 Docker 架設 GitLab Server]]