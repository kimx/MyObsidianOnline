---
aliases : []
created: 2023-01-18
updated: 2023-01-18
type: card
status: 🟩
publish: true
---
### Metadata
Tags:: #🗂️/🌞 
Topics:: [[Gitlab]] [[Docker]]
Links:: [[P-2023-01-專案-GitLab可行性測試]]
# Foreword
- 在Docker使用GitLab的備份/還原筆記，YAML設定接續 [[C-Docker架設GitLab Server]]

# Content
## 備份資料

```ad-note
title: 修改 docker-compose.yml ，以下為部份設定
~~~
...
        gitlab_rails['manage_backup_path'] = true
        gitlab_rails['backup_path'] = "/var/opt/gitlab/backups"
        gitlab_rails['backup_archive_permissions'] = 0644
        gitlab_rails['backup_pg_schema'] = 'public'          
        gitlab_rails['backup_keep_time'] = 604800    
...
~~~
```

```ad-note
title: 停止GitLab Container
~~~
docker-compose stop gitlab
~~~
```

```ad-note
title: 執行備份 
~~~
docker-compose exec -it gitlab gitlab-rake gitlab:backup:create
~~~
```

```ad-note
title: 備份組態及Sercret檔
~~~
docker-compose exec -it gitlab cp /etc/gitlab/gitlab-secrets.json /var/opt/gitlab/backups
~~~
```

```ad-note
title: 查看備份
~~~
docker-compose exec -it gitlab ls -lart var/opt/gitlab/backups
~~~
```

![upgit_20230118_1674025166.png](https://raw.githubusercontent.com/kimx/ObsidianAssets/master/2023/01/upgit_20230118_1674025166.png)

## 還原資料

```ad-note
title: 先停止服務
~~~
docker-compose exec -it gitlab gitlab-ctl stop puma
~~~
~~~
docker-compose exec -it gitlab gitlab-ctl stop sidekiq
~~~
```

- 還原設定: gitlab-secrets.json到gitlab_config目錄
	- 此動作適用在還原至另一個Container 例如:
		- Image重新指定另一個新的volume。
		- 全新的 Contianer。
		- 白話文: secrect.json就是備份檔的金鑰.
	- 若是本身Container還原可以不用做。
```ad-note
title: 執行還原
~~~
docker-compose exec -it gitlab gitlab-rake gitlab:backup:restore --trace
~~~
- 過程中會有一些確認yes/no，全都輸入yes
```

```ad-note
title: 重新啟動
~~~
docker-compose exec -it gitlab gitlab-ctl reconfigure
~~~
~~~
docker-compose exec -it gitlab gitlab-ctl restart
~~~
```

- 最後gitlab runner 要**重啟**才會正常執行工作。

## 其他

```ad-note
title: 進入Container Shell Command 互動模式
~~~
docker-compose exec gitlab sh
~~~
```

## Log
-  2023-01-18 : 測試備份後，刪除專案，再還原可以看見原本被刪除的檔案。

# Question
- 排程備份該如何作?
- 參考的連結有提到Remote upload backup，但未實作。
- 雖然資料可以備份還原,但之前原始碼放在AzureDevOps，不用擔心程式碼是否會遺失，而這種方式是自己管理，備份的檔案是GitLab的檔案格式，不是Repository，多少還是會考量到，若檔案毀損，程式碼無法還原時，該怎麼辨? 有沒有更萬一

# See Also
- [[C-Docker架設GitLab Server]]

# Reference
- [備份在Docker中的Gitlab資料](https://huskylin.github.io/2021/01/01/%E5%82%99%E4%BB%BD%E5%9C%A8Docker%E4%B8%AD%E7%9A%84Gitlab%E8%B3%87%E6%96%99-Backup-Gitlab-in-Docker/) 
- [還原參考此篇](https://blog.csdn.net/weixin_44208042/article/details/119138367)
- [Backup and restore Gitlab in docker](https://copdips.com/2018/09/backup-and-restore-gitlab-in-docker.html)