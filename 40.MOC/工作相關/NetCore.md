---
aliases : []
created: 2023-01-03
updated: 2023-01-03
type: 
status: 🟩
publish: true
---
### Metadata
- Tags:: #🗺️
- Topics:: [[程式開發]]

# 重記記錄
## DI
- 自行注入Logger: 
``` C#
var logger = serviceProvider.GetRequiredService<ILogger<MyType>>();
```

- 關於Console LogLevel，在AppSetting是根據命名空間來看。
# 其他
- 