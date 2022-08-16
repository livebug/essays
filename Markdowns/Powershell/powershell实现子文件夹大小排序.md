# powershell实现子文件夹大小排序

先上code：

```
# 输入根路径
param ($root = $(throw "必须输入一个目录才可以开始."))

$objs=@()
"开始遍历目录下所有一级子目录..."
foreach ($item in Get-ChildItem $root) {
    $size=0
    if($item.PSIsContainer)
    {
        # 如果时文件夹，就开始递归求和
        $size = (Get-ChildItem -Path $item.PSPath -Force -Recurse | 
                    Measure-Object -Property Length -Sum).Sum
    }
    elseif ($item.Length -ge 1MB){
        # 如果是文件，取属性 Length
        $size =$item.Length
    }
    
    # 文件夹或文件大于1M时才进行收录比较
    if ($size -ge 1MB) {
        # 创建一个新对象 路径，大小（MB为单位，保留两位小数）
        $obj = New-Object psobject -Property @{path=$item.FullName;size_MB=[Math]::Round($size/1MB,2)}
        # 加入到链表【其实是数组】
        $objs +=  $obj
    }

}

# 对链表进行处理
$objs | 
    Sort-Object size_MB -Descending |  # 根据大小排序，从大到小
        Select-Object -First ($objs.count/2) |  # 取前 50%
            Format-Table -Property size_MB, path -AutoSize # 以表格形式展示文件大小排序及路径
```

`Get-ChildItem` 同 dir

`Sort-Object` 排序

`Select-Object` 筛选

`Format-Table` 格式化对象打印

`New-Object` 新建对象 @{}

`$objs=@()` 新建数组

有计算数据记得括号加上，防止处理失败【一般是类型转换造成问题】
