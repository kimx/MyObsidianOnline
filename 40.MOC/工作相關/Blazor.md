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

- Blazor多國語系
	- E:\OneDrive\Tech\Blazor\BlazorLangLab
	- [Shared Resource架構](https://gemini.google.com/gem/a1cb0a1fc24a/a7c178a375376ec6)
	- [使用Claims切換](https://grok.com/c/224b5799-a9a6-42e3-abda-bc14c260a967)
# 其他
- [[@Robin]] [ChatGPT - Blazor 發展與建議](https://chatgpt.com/share/6864e234-311c-8002-ad62-a39fcf3e8e1d)