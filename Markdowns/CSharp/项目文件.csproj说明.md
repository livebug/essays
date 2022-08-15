# C# project file  `.csproj`

## Project 元素
Project元素是每个项目文件的根元素。 除了标识项目文件的 XML 架构之外，Project元素还可以包含属性来指定生成过程的入口点。 例如，在 Contact Manager 示例解决方案中， Publish.proj 文件指定生成应首先调用名为 FullPublish 的目标。
```
<Project ToolsVersion="4.0" DefaultTargets="FullPublish" 
         xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
  
</Project>
```
## 属性和条件
```
<PropertyGroup>    
   <ServerName>FABRIKAM\TEST1</ServerName>
   <ConnectionString>
     Data Source=FABRIKAM\TESTDB;InitialCatalog=ContactManager,...
   </ConnectionString>
</PropertyGroup>
```
## 项和项组
```
<ItemGroup>
   <ProjectsToBuild Include="$(SourceRoot)ContactManager-WCF.sln"/>
</ItemGroup>
```
项目文件将指示MSBuild构造需要以相同方式处理的文件列表
- 引用列表包括必须就地用于成功生成的程序集，
- 编译列表包括必须编译的代码文件，
- 内容列表包含必须不更改复制的资源。  
我们将介绍生成过程引用和使用本主题后面的项的方式。

复制资源文件到输出目录

```
  <ItemGroup>
    <None Update="SqlTestFiles\1.sql">
      <CopyToOutputDirectory>Always</CopyToOutputDirectory>
    </None>
  </ItemGroup>
```
