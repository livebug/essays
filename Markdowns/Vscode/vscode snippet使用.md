# vscode snippet使用

## 1. 打开方式

+ 左下角，点击设置

![Snipaste_2022-08-15_15-01-23.png](https://gitcode.net/archive/images/-/raw/master/Snipaste_2022-08-15_15-01-23.png)


## 2.选择语言然后书写模板

```json
{
    // Place your snippets for markdown here. Each snippet is defined under a snippet name and has a prefix, body and 
    // description. The prefix is what is used to trigger the snippet and the body will be expanded and inserted. Possible variables are:
    // $1, $2 for tab stops, $0 for the final cursor position, and ${1:label}, ${2:another} for placeholders. Placeholders with the 
    // same ids are connected.
    // Example:
    // "Print to console": {                  // 模板名称，一般是唯一的
    //  "prefix": "log",                      // 代码标志，需要唯一
    //  "body": [
    //       "console.log('$1');",
    //       "$2"
    //  ],                                     // 模板主体
    //  "description": "Log output to console" // 模板描述 
    // }
}
```
           
## :question: 问题

### 1. markdown不自动提示，需要修改配置
```json
"[markdown]": {
    "editor.formatOnSave": true,  // 保存时格式化
    "editor.renderWhitespace": "all", // 清理空格
    "editor.quickSuggestions": { // Controls whether suggestions should automatically show up while typing. 
        "other": true,
        "comments": true,
        "strings": true
    } 
}
```

<!-- 去露营了！ :tent: 很快回来。 -->

