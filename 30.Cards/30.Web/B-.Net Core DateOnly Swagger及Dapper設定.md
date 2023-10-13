---
aliases : []
created: 2023-03-10
updated: 2023-03-10
type: blog
status: 🟩
publish: true
---
### Metadata
Tags:: #🗂️/🌲
Topics:: [[NetCore]] [[WebAPI]] [[Dapper]]

# 前言
之前在寫前端時，針對日期在處理前後端序列化時，需要因時區特性作一些處理，例如:在台灣主機，取得後端的Json都會+08:00，前端則需要作顯示或調整的處理(Long Story不多述訴。

.Net Core 6 時代，就沒這煩惱了，直接使用DateOnly，前端得到的Json視為字串格式yyyy-MM-dd，送到後端也可以序列化成DateOnly型別。

# 使用方式
以下針對目前正在開發的一個專案，所使用到的技術，針對DateOnly的設定調整。
1. Swagger:加入MapType，告知DateOnly對應Json為string
```
builder.Services.AddSwaggerGen(c =>
{...
    c.MapType<DateOnly>(() => new OpenApiSchema { Format = "date", Type = "string" });
});
```

此設定為測試API時，對應正確的欄位，如下圖修改前/後
![upgit_20230310_1678429711.png](https://raw.githubusercontent.com/kimx/ObsidianAssets/master/2023/03/upgit_20230310_1678429711.png)

2.Dapper: 加入TypeHandler，處理從資料庫取值及設定參數值
```
public class DapperSqlDateOnlyTypeHandler : SqlMapper.TypeHandler<DateOnly>
{
    public override void SetValue(IDbDataParameter parameter, DateOnly date)
    {
        parameter.DbType = DbType.Date;
        parameter.Value = date.ToDateTime(new TimeOnly(0, 0));
    }

    public override DateOnly Parse(object value)
    {
        var result = DateOnly.FromDateTime((DateTime)value);
        return result;
    }
}

//Program.cs
   Dapper.SqlMapper.AddTypeHandler(new DapperSqlDateOnlyTypeHandler());
```

以上設定，在Blazor InputDate繫結及叫用API，測試OK。

# 總結
- 這樣在日期(不包含時間)的操作上，可以省下不少功夫以及避免一些時區序列/反序化問題。

# 相關參考
- [DapperSqlDateOnlyTypeHandler](https://github.com/DapperLib/Dapper/issues/1715#issuecomment-1149665776)

# 您可能也會有興趣的其他文章
- [Web API文件產生器-Swagger](https://note.kimx.info/2017/05/web-api-swagger.html)