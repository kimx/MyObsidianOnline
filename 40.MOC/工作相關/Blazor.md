---
aliases: 
created: 2023-08-04
updated: 2023-08-04
type: MOC
status: 🟩
publish: true
keywords:
  - 動態attribute
---
### Metadata
- Tags:: #🗺️
- Topics:: [[NetCore]]

# 技術備忘
-  [html 動態Blazor attributes](https://blazor-university.com/components/code-generated-html-attributes/)
- ValidationMessageStore 同一個FieldIdentifier 訊息出現多個，例如:Model.Name用在2個自訂元件，若元件訊息不一致，會出現2個，修正方式: 將訊息保持一致。
- RenderFragment builder參數用法
```
    private RenderFragment RenderDataGridFieldComponent(DynamicQueryField itemSetting) => builder =>
    {
        //    DynamicComponent dynamicComponent = new DynamicComponent();
 ..
        builder.OpenComponent(0, typeof(PropertyColumn<,>).MakeGenericType(dataType, propertyValueType));
..
        builder.AddAttribute(1, "Property", propExpression);
        builder.CloseComponent();
        // parameters.Add("ChildContent", RenderCodeId()); 自訂內容用

    };
```
# 其他
- 