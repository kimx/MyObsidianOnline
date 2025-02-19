---
aliases : []
created: 2023-03-06
updated: 2023-03-06
type: MOC
status: 🟩
publish: true
---
### Metadata
- Tags:: #🗺️
- Topics:: [[FrontEnd]]

# 網頁載入直線進度範例
- [參考](https://chatgpt.com/c/67513b31-d900-8003-98a5-7e21507ffea7) [[AI]] #GTD/🌀future 
``` Html
        /* 進度條容器 */
        #progress-bar-container {
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 3px; /* 進度條高度 */
            background: transparent; /* 容器背景透明 */
            z-index: 9999;
        }

        /* 進度條本體 */
        #progress-bar {
            height: 100%;
            width: 0; /* 初始進度為 0% */
            background: #29d; /* 進度條顏色 */
            transition: width 0.3s ease-out, opacity 0.5s ease-in; /* 寬度和淡出效果 */
            will-change: width, opacity; /* 提升動畫性能 */
        }


       <div id="progress-bar-container">
           <div id="progress-bar"></div>
       </div>

```

``` JavaScript
 const ProgressBar = (() => {
     const progressBar = document.getElementById('progress-bar');

     let progress = 0; // 當前進度

     return {
         // 開始進度條
         start() {
             progressBar.style.width = '0%';
             progressBar.style.opacity = '1';
             progress = 0;
         },

         // 更新進度條到指定百分比
         set(value) {
             progress = Math.min(value, 100); // 進度不得超過 100%
             progressBar.style.width = progress + '%';
         },

         // 完成進度條
         finish() {
             progress = 100;
             progressBar.style.width = '100%';
             setTimeout(() => {
                 progressBar.style.opacity = '0'; // 淡出進度條
             }, 500); // 延遲隱藏以確保用戶看到完成效果
         },

         // 重置進度條
         reset() {
             progressBar.style.width = '0%';
             progressBar.style.opacity = '0';
             progress = 0;
         },
     };
 })();
 document.addEventListener('DOMContentLoaded', () => {
     ProgressBar.start(); // 開始進度條
     let simulatedProgress = 0;

     // 模擬進度更新
     const interval = setInterval(() => {
         simulatedProgress += 10;
         ProgressBar.set(simulatedProgress);

         if (simulatedProgress >= 100) {
             //clearInterval(interval); // 停止模擬
             //ProgressBar.finish(); // 完成進度條
         }
     }, 100);
 });

 window.addEventListener('load', () => {
     setTimeout(function () {
         ProgressBar.set(100);
         ProgressBar.finish();
     }, 300);
 });
```
- 
# 其他
- 