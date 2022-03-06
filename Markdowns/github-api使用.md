# github-api 使用

## 令牌
因为无令牌会造成出发访问数量限制，为简单页面创建只有查看权限的令牌

github文档 https://docs.github.com/cn/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token

选择权限时不选任何项，该token只用来查看

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

测试

curl -i -u livebug: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 https://api.github.com/users/livebug


## blazor 应用使用

在wwwroot目录下建立 appsettings.json 加入下列变量。更好的做法是每次都向后台API服务器申请token，鉴于该权限不涉及机密信息，暂且放在这里。!!不要保留机密信息再此!!

GithubLookApi_Token="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" 
