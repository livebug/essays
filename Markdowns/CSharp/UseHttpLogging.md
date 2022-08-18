# UseHttpLogging

https://docs.microsoft.com/zh-cn/aspnet/core/fundamentals/http-logging/?view=aspnetcore-6.0

>ASP.NET Core 中的 HTTP 日志记录



### 启用 HTTP 日志记录
1. `Program.cs` 添加中间件
2. 日志中配置日志级别
   ```json
    {
        "DetailedErrors": true,
        "Logging": {
            "LogLevel": {
            "Default": "Information",
            "Microsoft.AspNetCore": "Warning",
            "Microsoft.AspNetCore.HttpLogging.HttpLoggingMiddleware": "Information"
            }
        }
    }
    ```