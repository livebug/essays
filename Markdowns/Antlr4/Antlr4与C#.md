# Antlr 与 C# 




## Q:发现生成的语句中对于 部分内嵌语法处理存在问题。

例如：
```
block_end :
       {!_input.LT(2).getText().equalsIgnoreCase("TRANSACTION")}? T_END 
     ;
```

其中 在C#的antlr实现中，`_input` 被私有化，此处替代的是 `TokenStream`，替换为如下：

```csharp
!this.TokenStream.LT(2).Text.Equals("TRANSACTION",StringComparison.OrdinalIgnoreCase)
```

---

源码文件 `Parser.cs`
```csharp
/// <summary>The input stream.</summary>
/// <remarks>The input stream.</remarks>
/// <seealso cref="InputStream()"/>
private ITokenStream _input;
...
public override IIntStream InputStream
{
    get
    {
        return _input;
    }
}
public ITokenStream TokenStream
{
    get
    {
        return _input;
    }
    set
    {
        this._input = null;
        Reset ();
        this._input = value;
    }
}
```

相应的java函数应该替换为C#的函数处理

+ `getText()` C# 使用`Text` 属性代替了
+ 字符串匹配函数 使用 `Equals()` 即可

### C# StringComparison 说明

| 枚举值                     | 值  | 说明                                                                                   |
| -------------------------- | --- | -------------------------------------------------------------------------------------- |
| CurrentCulture             | 0   | 使用区分区域性的排序规则和当前区域性比较字符串。                                       |
| CurrentCultureIgnoreCase   | 1   | 通过使用区分区域性的排序规则、当前区域性，并忽略所比较的字符串的大小写，来比较字符串。 |
| InvariantCulture           | 2   | 使用区分区域性的排序规则和固定区域性比较字符串。                                       |
| InvariantCultureIgnoreCase | 3   | 通过使用区分区域性的排序规则、固定区域性，并忽略所比较的字符串的大小写，来比较字符串。 |
| Ordinal                    | 4   | 使用序号（二进制）排序规则比较字符串。                                                 |
| OrdinalIgnoreCase          | 5   | 通过使用序号（二进制）区分区域性的排序规则并忽略所比较的字符串的大小写，来比较字符串。 |



