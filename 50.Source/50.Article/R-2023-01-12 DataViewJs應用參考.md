---
aliases: []
created: 2023-01-12
updated: 2023-01-12
type: article
status: 🟩
publish: true
card: true
---
### Metadata
- Title:: 
- Tags:: #📥️/📰️ 
- Topics::  [[Obsidian]]
- Links:: [[B-Obsidian DataviewJs應用]]

# Highlights & Notes
## Dataviewjs的奇技淫巧
- URL:: https://forum-zh.obsidian.md/t/topic/5954
- DataViewJs是DataView的進階應用，使用javascript做更進一步的應用。
	- 可以結合其他Plugin 例如:圖表
	- 區段宣告: dataviewjs
- Basic Sample
```
//取得所有筆記
dv.pages(``)
//使用Table
dv.Table(dv.pages(``))
//使用List
dv.List(dv.pages(``))
//所有工作
 dv.pages("").file.tasks
//過濾已完成的工作
dv.pages("").file.tasks.where(t=>!t.completed)
// Render 標題，數字2= ## 
dv.header(2,"🗓️本日待辦");
```
``` dataviewjs
```

## Plugin CustomJs
- URL:: https://github.com/saml-dev/obsidian-custom-js
- 載入自訂的 Js，範例中有結合將DataViewJs的方法放到自己的JS裡，讓其他筆記去引用。
## Joschua's Notes
- URL: https://notes.joschua.io/50+Slipbox/Dataview+Plugin
- 線上筆記，作者個人的DataviewJs卡片筆記。

# 自己的話
- 以上彙整了幾篇相關應用，可以使用javascript開發更彈性的應用，並將共用邏輯統一控管，再利用。
- DataviewJs Task Basic
```dataviewjs
const isDue =(t)=>{
	var result= moment(new Date(t.due)).isBefore(moment(),"day");
	return result;
}

const isToday =(t)=>{
	var result= moment(new Date(t.due)).isSame(moment(),"day");
	return result;
}

const isUpcoming =(t)=>{
	var result= moment(new Date(t.due)).isAfter(moment(),"day");
	return result;
}

const isUndated =(t)=>{
	return t.due == null;
}

let tasks = dv.pages().where(
	f=> f.file.path.indexOf("60.Extra")==-1
).file.tasks;
tasks=tasks.where(t=>!t.completed 
				  && t.section.subpath.indexOf("Routine")==-1
				  );
tasks.sort(t=>t.due);

dv.header(2,"🗓️本日待辦");
dv.taskList(tasks.filter(t=>isToday(t)),true)

dv.header(2,"🗓️過期待辦");
dv.taskList(tasks.filter(t=>isDue(t)),true)

dv.header(2,"🗓️未來待辨");
dv.taskList(tasks.filter(t=>isUpcoming(t)),true)

dv.header(2,"🗓️未排程");
dv.taskList(tasks.filter(t=>isUndated(t)),true)

```
- DataviewJs Task CommonJs
```dataviewjs
const isDue =(t)=>{
	var result= moment(new Date(t.due)).isBefore(moment(),"day");
	return result;
}

const isToday =(t)=>{
	var result= moment(new Date(t.due)).isSame(moment(),"day");
	return result;
}

const isUpcoming =(t)=>{
	var result= moment(new Date(t.due)).isAfter(moment(),"day");
	return result;
}

const isUndated =(t)=>{
	return t.due == null;
}

const {MyTask} = customJS;
let tasks=MyTask.getTasks(dv);
tasks.sort(t=>t.due);

dv.header(2,"🗓️本日待辦");
dv.taskList(tasks.filter(t=>isToday(t)),true)

dv.header(2,"🗓️過期待辦");
dv.taskList(tasks.filter(t=>isDue(t)),true)

dv.header(2,"🗓️未來待辨");
dv.taskList(tasks.filter(t=>isUpcoming(t)),true)

dv.header(2,"🗓️未排程");
dv.taskList(tasks.filter(t=>isUndated(t)),true)
```

# 其他
- [Dataview 官方欄位說明-Page](https://blacksmithgu.github.io/obsidian-dataview/annotation/metadata-pages/)
- [Dataview 官方欄位說明-Task](https://blacksmithgu.github.io/obsidian-dataview/annotation/metadata-tasks/#field-shorthands)
- [DataviewJs如何針對Header過濾](https://github.com/blacksmithgu/obsidian-dataview/discussions/547#discussioncomment-3214417)
- [dv.TaskList Snippet](https://gist.githubusercontent.com/TfTHacker/4e019abd25c58de57376add6e3aa4173/raw/7e2a5a1b66e2357421387575b49e6959c159013f/Tasks%2520by%2520Date%2520-%2520for%2520Obsidian%2520and%2520Dataview.js)