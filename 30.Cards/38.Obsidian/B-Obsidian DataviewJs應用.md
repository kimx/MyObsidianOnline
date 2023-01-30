---
aliases : []
created: 2023-01-12
updated: 2023-01-12
type: blog
status: 🟩
---
### Metadata
Tags:: #🗂️/🌲 
Topics:: [[Obsidian]]

# Foreword
- DataviewJs為Dataview的更進一步應用，使用javascript撰寫。
- 筆記示範，如何使用DataviewJs並結合CustomJs讓取得Tasks的方式可以在多個筆記引用。
# Content
## 安裝PlugIn CustomJs
- 指定js的資料夾![upgit_20230112_1673508473.png](https://raw.githubusercontent.com/kimx/ObsidianAssets/master/2023/01/upgit_20230112_1673508473.png)
## 撰寫 MyTask.js
 - 取得所有**未完成的工作**，並濾掉不需要的**資料夾**及**header**
``` javascript
class MyTask {
  getTasks(dv) {
    let tasks = dv.pages().where((f) => f.file.path.indexOf("60.Extra") == -1).file.tasks;
    tasks = tasks.where(
				(t) => !t.completed 
					 && t.section.subpath.indexOf("Routine") == -1
    );
    tasks.sort((t) => t.due);
    return tasks;
  }
}

```
- 完成後放到資料夾 60.Extra/67.Assets/js

## DataviewJs顯示Tasks
- 透過customJs 使用MyTask，並呼叫getTasks取得待處理工作。
- 針對**各狀態**過濾，顯示**標題及Tasks**。
- 若要顯示結果，將dataviewjs**-marked**，的marked移除。
```dataviewjs-marked
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

# Question
- 

# See Also
- [[C-我的Obsidian筆記使用方式|My Note know how]]

# Reference
- [[R-2023-01-12 DataViewJs應用參考]]