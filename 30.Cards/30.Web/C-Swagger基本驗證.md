---
aliases : []
created: 2023-03-07
updated: 2023-03-07
type: card/blog
status: 🟩
publish: true
---
### Metadata
Tags:: #🗂️/🌱️
Topics:: [[WebAPI]] [[NetCore]] [[Github]] [[Swagger]]

# Foreword
- API文件加上基本驗證，避免其他人任意存取。

# Content
## 實作
1. 新增BasicAuthenticationHandler，繼承AuthenticationHandler
2. Controller 冠上驗證
3. Program.cs 加入設定
4. [完整程式碼](https://github.com/kimx/SwaggerBasicAuthenticationLab)

## .NET 10版本
- Bearer
```
builder.Services.AddOpenApi(options =>
{
    options.AddDocumentTransformer<BearerSecuritySchemeTransformer>();
});


internal sealed class BearerSecuritySchemeTransformer(IAuthenticationSchemeProvider authenticationSchemeProvider) : IOpenApiDocumentTransformer
{
    //public async Task TransformAsync(OpenApiDocument document, OpenApiDocumentTransformerContext context, CancellationToken cancellationToken)
    //{
    //    var authenticationSchemes = await authenticationSchemeProvider.GetAllSchemesAsync();
    //    if (authenticationSchemes.Any(authScheme => authScheme.Name == "Bearer"))
    //    {
    //        IDictionary<string, IOpenApiSecurityScheme> requirements = new Dictionary<string, IOpenApiSecurityScheme>
    //        {
    //            ["Bearer"] = new OpenApiSecurityScheme
    //            {
    //                Type = SecuritySchemeType.Http,
    //                Scheme = "bearer", // 不要大寫，OpenAPI 規範要求小寫
    //                In = ParameterLocation.Header,
    //                BearerFormat = "JWT"
    //            }
    //        };
    //        document.Components ??= new OpenApiComponents();
    //        document.Components.SecuritySchemes = requirements;
    //    }
    //}
    public async Task TransformAsync(OpenApiDocument document, OpenApiDocumentTransformerContext context, CancellationToken cancellationToken)
    {
        var authenticationSchemes = await authenticationSchemeProvider.GetAllSchemesAsync();
        if (authenticationSchemes.Any(authScheme => authScheme.Name == "Bearer"))
        {
            var securitySchemes = new Dictionary<string, IOpenApiSecurityScheme>
            {
                ["Bearer"] = new OpenApiSecurityScheme
                {
                    Type = SecuritySchemeType.Http,
                    Scheme = "bearer", // "bearer" refers to the header name here
                    In = ParameterLocation.Header,
                    BearerFormat = "Json Web Token"
                }
            };
            document.Components ??= new OpenApiComponents();
            document.Components.SecuritySchemes = securitySchemes;
            foreach (var operation in document.Paths.Values.SelectMany(path => path.Operations))
            {
                operation.Value.Security ??= [];
                operation.Value.Security.Add(new OpenApiSecurityRequirement
                {

                    [new OpenApiSecuritySchemeReference("Bearer", document)] = []
                });
            }

        }
    }
}
```
- API Key
	- 針對有套用API Key的才使用
```
                   builder.Services.AddOpenApi(options =>
            {
                options.AddDocumentTransformer<ApiKeySecuritySchemeTransformer>();
                options.AddOperationTransformer<ApiKeySecurityRequirementTransformer>();
            });
       
       internal static class ApiKeyOpenApiConfiguration
{
    internal const string HeaderName = "X-API-KEY";
    internal const string SecuritySchemeName = "ApiKey";

    internal static bool RequiresApiKey(ActionDescriptor? actionDescriptor)
    {
        if (actionDescriptor is not ControllerActionDescriptor controllerActionDescriptor)
        {
            return false;
        }

        return controllerActionDescriptor.MethodInfo.IsDefined(typeof(ApiKeyAttribute), inherit: true)
            || controllerActionDescriptor.ControllerTypeInfo.IsDefined(typeof(ApiKeyAttribute), inherit: true);
    }

    internal static OpenApiSecurityScheme CreateOpenApiSecurityScheme()
    {
        return new OpenApiSecurityScheme
        {
            Name = HeaderName,
            Type = SecuritySchemeType.ApiKey,
            In = ParameterLocation.Header,
            Description = "Provide the API key via the X-API-KEY header."
        };
    }
}

internal sealed class ApiKeySecuritySchemeTransformer : IOpenApiDocumentTransformer
{
    public Task TransformAsync(OpenApiDocument document, OpenApiDocumentTransformerContext context, CancellationToken cancellationToken)
    {
        document.Components ??= new OpenApiComponents();
        document.Components.SecuritySchemes ??= new Dictionary<string, IOpenApiSecurityScheme>();
        document.Components.SecuritySchemes[ApiKeyOpenApiConfiguration.SecuritySchemeName] =
            ApiKeyOpenApiConfiguration.CreateOpenApiSecurityScheme();

        return Task.CompletedTask;
    }
}

internal sealed class ApiKeySecurityRequirementTransformer : IOpenApiOperationTransformer
{
    public Task TransformAsync(OpenApiOperation operation, OpenApiOperationTransformerContext context, CancellationToken cancellationToken)
    {
        if (!ApiKeyOpenApiConfiguration.RequiresApiKey(context.Description.ActionDescriptor))
        {
            return Task.CompletedTask;
        }

        operation.Security ??= [];
        operation.Security.Add(new OpenApiSecurityRequirement
        {
            [new OpenApiSecuritySchemeReference(ApiKeyOpenApiConfiguration.SecuritySchemeName, context.Document!)] = []
        });

        return Task.CompletedTask;
    }
}
```
# See Also
- 永久卡片

# Reference
- 