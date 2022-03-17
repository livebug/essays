*该文档保留所有的链接地址*

参考教程：
* https://www.yiibai.com/maven/maven_environment_setup.html 易百教程
* https://www.runoob.com/maven/maven-tutorial.html 菜鸟教程

maven 官方网站：
* https://maven.apache.org/download.cgi


# Windows 安装步骤：
1. 下载ZIP 文件  
    点击直接下载  
    https://mirror.bit.edu.cn/apache/maven/maven-3/3.6.3/binaries/apache-maven-3.6.3-bin.zip
2. 解压到 自己的目录（因为我C盘富裕，所以解压到C:\Java） 文件夹下
3. 该步骤推荐一下解压缩工具 bindzip   
    (官网 https://www.bandisoft.com/bandizip/)  
    (点击下载 https://www.bandisoft.com/bandizip/dl.php?online)
4. 配置环境变量  
    手动：(图像来自 菜鸟教程)

    ![MAVEN_HOME](https://www.runoob.com/wp-content/uploads/2018/09/1536057115-1481-20151218175411912-170761788.png)
    ![PATH](https://www.runoob.com/wp-content/uploads/2018/09/1536057115-7470-20151218175417006-1644078150.png)

    ```
        MAVEN_HOME  
        C:\Java\apache-maven-3.6.3  
        PATH  
        %MAVEN_HOME%\bin  
        setx MAVEN_HOME "C:\Java\apache-maven-3.6.3" -M
    ```
    PowerShell:
    ```powershell
    ## 设置系统环境变量 使用管理员打开powershell 
    [environment]::SetEnvironmentvariable("MAVEN_HOME","C:\Java\apache-maven-3.6.3","Machine")
    $path=[environment]::GetEnvironmentvariable("PATH", "Machine")
    [environment]::SetEnvironmentvariable("Path",$path+";%MAVEN_HOME%\bin","Machine")
    ## 查看环境变量
    [environment]::GetEnvironmentvariable("MAVEN_HOME", "Machine")
    [environment]::GetEnvironmentvariable("Path", "Machine")
    ## 重启计算机
    Restart-Computer
    ```
<!-- 
    [environment]::GetEnvironmentvariable("MAVEN_HOME", "User")
    [environment]::GetEnvironmentvariable("Path", "User")
-->
5. 执行`mvn -v `查看安装结果
    ```
    PS F:\Java> mvn -v
    Apache Maven 3.6.3 (cecedd343002696d0abb50b32b541b8a6ba2883f)
    Maven home: C:\Java\apache-maven-3.6.3\bin\..
    Java version: 1.8.0_231, vendor: Oracle Corporation, runtime: C:\Java\jdk1.8.0_231\jre
    Default locale: zh_CN, platform encoding: GBK
    OS name: "windows 10", version: "10.0", arch: "amd64", family: "windows"
    ```
6. 配置vscode
    ```json
    "java.home": "C:\\Java\\jdk1.8.0_231",
    "java.configuration.maven.userSettings": "C:\\Java\\apache-maven-3.6.3\\conf\\settings.xml",
    "maven.executable.path": "C:\\Java\\apache-maven-3.6.3\\bin\\mvn.cmd",
    "maven.terminal.useJavaHome": true,
    "maven.terminal.customEnv": [
        {
            "environmentVariable": "JAVA_HOME",
            "value": "C:\\Java\\jdk1.8.0_231"
        }
    ],
    ```
7. 修改 maven 镜像仓库
```xml
    <mirror>
      <id>alimaven</id>
      <name>aliyun maven</name>
      <url>http://maven.aliyun.com/nexus/content/groups/public/</url>
      <mirrorOf>central</mirrorOf>        
    </mirror>
```
8. 备注
    * 本地仓库  
        Maven 的本地仓库，在安装 Maven 后并不会创建，它是在第一次执行 maven 命令的时候才被创建。

        运行 Maven 的时候，Maven 所需要的任何构件都是直接从本地仓库获取的。如果本地仓库没有，它会首先尝试从远程仓库下载构件至本地仓库，然后再使用本地仓库的构件。

        默认情况下，不管Linux还是 Windows，每个用户在自己的用户目录下都有一个路径名为 .m2/respository/ 的仓库目录。

        Maven 本地仓库默认被创建在 %USER_HOME% 目录下。要修改默认位置，在 %M2_HOME%\conf 目录中的 Maven 的 settings.xml 文件中定义另一个路径。


# 第一次创建Webapp 日志记录

PS F:\Java\helloworld\helloWebapp> & "C:\Java\apache-maven-3.6.3\bin\mvn.cmd" org.apache.maven.plugins:maven-archetype-plugin:3.1.2:generate -DarchetypeArtifactId="maven-archetype-webapp" -DarchetypeGroupId="org.apache.maven.archetypes" -DarchetypeVersion="1.4"
[INFO] Scanning for projects...
Downloading from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/apache/maven/plugins/maven-archetype-plugin/3.1.2/maven-archetype-plugin-3.1.2.pom
Downloaded from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/apache/maven/plugins/maven-archetype-plugin/3.1.2/maven-archetype-plugin-3.1.2.pom (11 kB at 15 kB/s)
Downloading from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/apache/maven/archetype/maven-archetype/3.1.2/maven-archetype-3.1.2.pom
Downloaded from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/apache/maven/archetype/maven-archetype/3.1.2/maven-archetype-3.1.2.pom (12 kB at 27 kB/s)
Downloading from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/apache/maven/maven-parent/33/maven-parent-33.pom
Downloaded from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/apache/maven/maven-parent/33/maven-parent-33.pom (44 kB at 154 kB/s)
Downloading from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/apache/apache/21/apache-21.pom
Downloaded from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/apache/apache/21/apache-21.pom (17 kB at 38 kB/s)
Downloading from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/apache/maven/plugins/maven-archetype-plugin/3.1.2/maven-archetype-plugin-3.1.2.jar
Downloaded from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/apache/maven/plugins/maven-archetype-plugin/3.1.2/maven-archetype-plugin-3.1.2.jar (97 kB at 186 kB/s)
[INFO]
[INFO] ------------------< org.apache.maven:standalone-pom >-------------------
[INFO] Building Maven Stub Project (No POM) 1
[INFO] --------------------------------[ pom ]---------------------------------
[INFO]
[INFO] >>> maven-archetype-plugin:3.1.2:generate (default-cli) > generate-sources @ standalone-pom >>>
[INFO]
[INFO] <<< maven-archetype-plugin:3.1.2:generate (default-cli) < generate-sources @ standalone-pom <<<
[INFO]
[INFO]
[INFO] --- maven-archetype-plugin:3.1.2:generate (default-cli) @ standalone-pom ---
Downloading from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/apache/maven/archetype/archetype-catalog/3.1.2/archetype-catalog-3.1.2.pom
Downloaded from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/apache/maven/archetype/archetype-catalog/3.1.2/archetype-catalog-3.1.2.pom (2.0 kB at 7.9 kB/s)
Downloading from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/apache/maven/archetype/archetype-models/3.1.2/archetype-models-3.1.2.pom
Downloaded from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/apache/maven/archetype/archetype-models/3.1.2/archetype-models-3.1.2.pom (2.8 kB at 7.9 kB/s)
Downloading from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/codehaus/plexus/plexus-utils/3.2.0/plexus-utils-3.2.0.pom
Downloaded from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/codehaus/plexus/plexus-utils/3.2.0/plexus-utils-3.2.0.pom (4.8 kB at 19 kB/s)
Downloading from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/codehaus/plexus/plexus/5.1/plexus-5.1.pom
Downloaded from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/codehaus/plexus/plexus/5.1/plexus-5.1.pom (23 kB at 82 kB/s)
Downloading from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/apache/maven/archetype/archetype-descriptor/3.1.2/archetype-descriptor-3.1.2.pom
Downloaded from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/apache/maven/archetype/archetype-descriptor/3.1.2/archetype-descriptor-3.1.2.pom (2.0 kB at 8.5 kB/s)
Downloading from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/apache/maven/archetype/archetype-common/3.1.2/archetype-common-3.1.2.pom
Downloaded from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/apache/maven/archetype/archetype-common/3.1.2/archetype-common-3.1.2.pom (18 kB at 66 kB/s)
Downloading from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/codehaus/groovy/groovy/2.4.16/groovy-2.4.16.pom
Downloaded from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/codehaus/groovy/groovy/2.4.16/groovy-2.4.16.pom (19 kB at 77 kB/s)
Downloading from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/apache/ivy/ivy/2.4.0/ivy-2.4.0.pom
Downloaded from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/apache/ivy/ivy/2.4.0/ivy-2.4.0.pom (6.3 kB at 27 kB/s)
Downloading from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/apache/apache/7/apache-7.pom
Downloaded from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/apache/apache/7/apache-7.pom (14 kB at 31 kB/s)
Downloading from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/net/sourceforge/jchardet/jchardet/1.0/jchardet-1.0.pom
Downloaded from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/net/sourceforge/jchardet/jchardet/1.0/jchardet-1.0.pom (1.3 kB at 3.1 kB/s)
Downloading from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/codehaus/plexus/plexus-component-annotations/1.7.1/plexus-component-annotations-1.7.1.pom
Downloaded from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/codehaus/plexus/plexus-component-annotations/1.7.1/plexus-component-annotations-1.7.1.pom (770 B at 2.2 kB/s)
Downloading from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/codehaus/plexus/plexus-containers/1.7.1/plexus-containers-1.7.1.pom
Downloaded from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/codehaus/plexus/plexus-containers/1.7.1/plexus-containers-1.7.1.pom (5.0 kB at 15 kB/s)
Downloading from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/codehaus/plexus/plexus/4.0/plexus-4.0.pom
Downloaded from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/codehaus/plexus/plexus/4.0/plexus-4.0.pom (22 kB at 77 kB/s)
Downloading from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/sonatype/forge/forge-parent/10/forge-parent-10.pom
Downloaded from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/sonatype/forge/forge-parent/10/forge-parent-10.pom (14 kB at 37 kB/s)
Downloading from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/jdom/jdom/1.0/jdom-1.0.pom
Downloaded from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/jdom/jdom/1.0/jdom-1.0.pom (1.2 kB at 4.9 kB/s)
Downloading from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/apache/maven/maven-model/3.0/maven-model-3.0.pom
Downloaded from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/apache/maven/maven-model/3.0/maven-model-3.0.pom (3.9 kB at 12 kB/s)
Downloading from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/apache/maven/maven/3.0/maven-3.0.pom
Downloaded from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/apache/maven/maven/3.0/maven-3.0.pom (22 kB at 89 kB/s)
Downloading from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/apache/maven/maven-parent/15/maven-parent-15.pom
Downloaded from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/apache/maven/maven-parent/15/maven-parent-15.pom (24 kB at 70 kB/s)
Downloading from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/apache/apache/6/apache-6.pom
Downloaded from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/apache/apache/6/apache-6.pom (13 kB at 52 kB/s)
Downloading from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/apache/maven/maven-core/3.0/maven-core-3.0.pom
Downloaded from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/apache/maven/maven-core/3.0/maven-core-3.0.pom (6.6 kB at 20 kB/s)
Downloading from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/apache/maven/maven-settings/3.0/maven-settings-3.0.pom
Downloaded from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/apache/maven/maven-settings/3.0/maven-settings-3.0.pom (1.9 kB at 5.6 kB/s)
Downloading from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/apache/maven/maven-settings-builder/3.0/maven-settings-builder-3.0.pom
Downloaded from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/apache/maven/maven-settings-builder/3.0/maven-settings-builder-3.0.pom (2.2 kB at 6.7 kB/s)
Downloading from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/codehaus/plexus/plexus-interpolation/1.14/plexus-interpolation-1.14.pom
Downloaded from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/codehaus/plexus/plexus-interpolation/1.14/plexus-interpolation-1.14.pom (910 B at 2.4 kB/s)
Downloading from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/codehaus/plexus/plexus-components/1.1.18/plexus-components-1.1.18.pom
Downloaded from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/codehaus/plexus/plexus-components/1.1.18/plexus-components-1.1.18.pom (5.4 kB at 16 kB/s)
Downloading from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/codehaus/plexus/plexus/2.0.7/plexus-2.0.7.pom
Downloaded from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/codehaus/plexus/plexus/2.0.7/plexus-2.0.7.pom (17 kB at 47 kB/s)
Downloading from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/sonatype/plexus/plexus-sec-dispatcher/1.3/plexus-sec-dispatcher-1.3.pom
Downloaded from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/sonatype/plexus/plexus-sec-dispatcher/1.3/plexus-sec-dispatcher-1.3.pom (3.0 kB at 12 kB/s)
Downloading from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/sonatype/spice/spice-parent/12/spice-parent-12.pom
Downloaded from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/sonatype/spice/spice-parent/12/spice-parent-12.pom (6.8 kB at 29 kB/s)
Downloading from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/sonatype/forge/forge-parent/4/forge-parent-4.pom
Downloaded from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/sonatype/forge/forge-parent/4/forge-parent-4.pom (8.4 kB at 36 kB/s)
Downloading from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/sonatype/plexus/plexus-cipher/1.4/plexus-cipher-1.4.pom
Downloaded from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/sonatype/plexus/plexus-cipher/1.4/plexus-cipher-1.4.pom (2.1 kB at 8.6 kB/s)
Downloading from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/apache/maven/maven-repository-metadata/3.0/maven-repository-metadata-3.0.pom
Downloaded from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/apache/maven/maven-repository-metadata/3.0/maven-repository-metadata-3.0.pom (1.9 kB at 8.2 kB/s)
Downloading from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/apache/maven/maven-artifact/3.0/maven-artifact-3.0.pom
Downloaded from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/apache/maven/maven-artifact/3.0/maven-artifact-3.0.pom (1.9 kB at 5.5 kB/s)
Downloading from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/apache/maven/maven-plugin-api/3.0/maven-plugin-api-3.0.pom
Downloaded from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/apache/maven/maven-plugin-api/3.0/maven-plugin-api-3.0.pom (2.3 kB at 9.7 kB/s)
Downloading from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/sonatype/sisu/sisu-inject-plexus/1.4.2/sisu-inject-plexus-1.4.2.pom
Downloaded from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/sonatype/sisu/sisu-inject-plexus/1.4.2/sisu-inject-plexus-1.4.2.pom (5.4 kB at 22 kB/s)
Downloading from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/sonatype/sisu/inject/guice-plexus/1.4.2/guice-plexus-1.4.2.pom
Downloaded from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/sonatype/sisu/inject/guice-plexus/1.4.2/guice-plexus-1.4.2.pom (3.1 kB at 8.3 kB/s)
Downloading from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/sonatype/sisu/inject/guice-bean/1.4.2/guice-bean-1.4.2.pom
Downloaded from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/sonatype/sisu/inject/guice-bean/1.4.2/guice-bean-1.4.2.pom (2.6 kB at 7.7 kB/s)
Downloading from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/sonatype/sisu/sisu-inject/1.4.2/sisu-inject-1.4.2.pom
Downloaded from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/sonatype/sisu/sisu-inject/1.4.2/sisu-inject-1.4.2.pom (1.2 kB at 3.5 kB/s)
Downloading from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/sonatype/sisu/sisu-parent/1.4.2/sisu-parent-1.4.2.pom
Downloaded from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/sonatype/sisu/sisu-parent/1.4.2/sisu-parent-1.4.2.pom (7.8 kB at 33 kB/s)
Downloading from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/sonatype/forge/forge-parent/6/forge-parent-6.pom
Downloaded from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/sonatype/forge/forge-parent/6/forge-parent-6.pom (11 kB at 32 kB/s)
Downloading from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/codehaus/plexus/plexus-classworlds/2.2.3/plexus-classworlds-2.2.3.pom
Downloaded from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/codehaus/plexus/plexus-classworlds/2.2.3/plexus-classworlds-2.2.3.pom (4.0 kB at 12 kB/s)
Downloading from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/codehaus/plexus/plexus/2.0.6/plexus-2.0.6.pom
Downloaded from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/codehaus/plexus/plexus/2.0.6/plexus-2.0.6.pom (17 kB at 69 kB/s)
Downloading from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/sonatype/sisu/sisu-inject-bean/1.4.2/sisu-inject-bean-1.4.2.pom
Downloaded from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/sonatype/sisu/sisu-inject-bean/1.4.2/sisu-inject-bean-1.4.2.pom (5.5 kB at 22 kB/s)
Downloading from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/sonatype/sisu/sisu-guice/2.1.7/sisu-guice-2.1.7.pom
Downloaded from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/sonatype/sisu/sisu-guice/2.1.7/sisu-guice-2.1.7.pom (11 kB at 44 kB/s)
Downloading from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/apache/maven/maven-model-builder/3.0/maven-model-builder-3.0.pom
Downloaded from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/apache/maven/maven-model-builder/3.0/maven-model-builder-3.0.pom (2.2 kB at 6.6 kB/s)
Downloading from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/apache/maven/maven-aether-provider/3.0/maven-aether-provider-3.0.pom
Downloaded from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/apache/maven/maven-aether-provider/3.0/maven-aether-provider-3.0.pom (2.5 kB at 10.0 kB/s)
Downloading from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/sonatype/aether/aether-api/1.7/aether-api-1.7.pom
Downloaded from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/sonatype/aether/aether-api/1.7/aether-api-1.7.pom (1.7 kB at 5.4 kB/s)
Downloading from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/sonatype/aether/aether-parent/1.7/aether-parent-1.7.pom
Downloaded from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/sonatype/aether/aether-parent/1.7/aether-parent-1.7.pom (7.7 kB at 25 kB/s)
Downloading from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/sonatype/aether/aether-util/1.7/aether-util-1.7.pom
Downloaded from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/sonatype/aether/aether-util/1.7/aether-util-1.7.pom (2.1 kB at 6.0 kB/s)
Downloading from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/sonatype/aether/aether-impl/1.7/aether-impl-1.7.pom
Downloaded from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/sonatype/aether/aether-impl/1.7/aether-impl-1.7.pom (3.7 kB at 11 kB/s)
Downloading from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/sonatype/aether/aether-spi/1.7/aether-spi-1.7.pom
Downloaded from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/sonatype/aether/aether-spi/1.7/aether-spi-1.7.pom (1.7 kB at 6.7 kB/s)
Downloading from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/apache/maven/shared/maven-invoker/3.0.1/maven-invoker-3.0.1.pom
Downloaded from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/apache/maven/shared/maven-invoker/3.0.1/maven-invoker-3.0.1.pom (4.9 kB at 19 kB/s)
Downloading from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/apache/maven/shared/maven-shared-components/31/maven-shared-components-31.pom
Downloaded from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/apache/maven/shared/maven-shared-components/31/maven-shared-components-31.pom (5.1 kB at 16 kB/s)
Downloading from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/apache/maven/maven-parent/31/maven-parent-31.pom
Downloaded from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/apache/maven/maven-parent/31/maven-parent-31.pom (43 kB at 148 kB/s)
Downloading from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/apache/apache/19/apache-19.pom
Downloaded from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/apache/apache/19/apache-19.pom (15 kB at 44 kB/s)
Downloading from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/apache/maven/shared/maven-shared-utils/3.2.1/maven-shared-utils-3.2.1.pom
Downloaded from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/apache/maven/shared/maven-shared-utils/3.2.1/maven-shared-utils-3.2.1.pom (5.6 kB at 16 kB/s)
Downloading from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/apache/maven/shared/maven-shared-components/30/maven-shared-components-30.pom
Downloaded from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/apache/maven/shared/maven-shared-components/30/maven-shared-components-30.pom (4.6 kB at 13 kB/s)
Downloading from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/apache/maven/maven-parent/30/maven-parent-30.pom
Downloaded from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/apache/maven/maven-parent/30/maven-parent-30.pom (41 kB at 122 kB/s)
Downloading from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/apache/apache/18/apache-18.pom
Downloaded from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/apache/apache/18/apache-18.pom (16 kB at 42 kB/s)
Downloading from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/commons-io/commons-io/2.2/commons-io-2.2.pom
Downloaded from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/commons-io/commons-io/2.2/commons-io-2.2.pom (11 kB at 32 kB/s)
Downloading from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/apache/commons/commons-parent/24/commons-parent-24.pom
Downloaded from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/apache/commons/commons-parent/24/commons-parent-24.pom (47 kB at 131 kB/s)
Downloading from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/apache/apache/9/apache-9.pom
Downloaded from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/apache/apache/9/apache-9.pom (15 kB at 43 kB/s)
Downloading from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/apache/maven/shared/maven-artifact-transfer/0.11.0/maven-artifact-transfer-0.11.0.pom
Downloaded from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/apache/maven/shared/maven-artifact-transfer/0.11.0/maven-artifact-transfer-0.11.0.pom (11 kB at 33 kB/s)
Downloading from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/apache/maven/shared/maven-shared-components/33/maven-shared-components-33.pom
Downloaded from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/apache/maven/shared/maven-shared-components/33/maven-shared-components-33.pom (5.1 kB at 15 kB/s)
Downloading from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/apache/maven/shared/maven-common-artifact-filters/3.0.1/maven-common-artifact-filters-3.0.1.pom
Downloaded from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/apache/maven/shared/maven-common-artifact-filters/3.0.1/maven-common-artifact-filters-3.0.1.pom (4.8 kB at 14 kB/s)
Downloading from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/apache/maven/shared/maven-shared-utils/3.1.0/maven-shared-utils-3.1.0.pom
Downloaded from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/apache/maven/shared/maven-shared-utils/3.1.0/maven-shared-utils-3.1.0.pom (5.0 kB at 22 kB/s)
Downloading from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/commons-codec/commons-codec/1.11/commons-codec-1.11.pom
Downloaded from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/commons-codec/commons-codec/1.11/commons-codec-1.11.pom (14 kB at 57 kB/s)
Downloading from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/apache/commons/commons-parent/42/commons-parent-42.pom
Downloaded from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/apache/commons/commons-parent/42/commons-parent-42.pom (68 kB at 189 kB/s)
Downloading from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/slf4j/slf4j-api/1.7.5/slf4j-api-1.7.5.pom
Downloaded from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/slf4j/slf4j-api/1.7.5/slf4j-api-1.7.5.pom (2.7 kB at 7.7 kB/s)
Downloading from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/slf4j/slf4j-parent/1.7.5/slf4j-parent-1.7.5.pom
Downloaded from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/slf4j/slf4j-parent/1.7.5/slf4j-parent-1.7.5.pom (12 kB at 32 kB/s)
Downloading from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/codehaus/plexus/plexus-velocity/1.1.8/plexus-velocity-1.1.8.pom
Downloaded from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/codehaus/plexus/plexus-velocity/1.1.8/plexus-velocity-1.1.8.pom (1.9 kB at 4.2 kB/s)
Downloading from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/codehaus/plexus/plexus-components/1.1.15/plexus-components-1.1.15.pom
Downloaded from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/codehaus/plexus/plexus-components/1.1.15/plexus-components-1.1.15.pom (2.8 kB at 7.8 kB/s)
Downloading from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/codehaus/plexus/plexus/2.0.3/plexus-2.0.3.pom
Downloaded from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/codehaus/plexus/plexus/2.0.3/plexus-2.0.3.pom (15 kB at 38 kB/s)
Downloading from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/commons-collections/commons-collections/3.2.1/commons-collections-3.2.1.pom
Downloaded from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/commons-collections/commons-collections/3.2.1/commons-collections-3.2.1.pom (13 kB at 37 kB/s)
Downloading from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/apache/commons/commons-parent/9/commons-parent-9.pom
Downloaded from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/apache/commons/commons-parent/9/commons-parent-9.pom (22 kB at 62 kB/s)
Downloading from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/apache/apache/4/apache-4.pom
Downloaded from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/apache/apache/4/apache-4.pom (4.5 kB at 13 kB/s)
Downloading from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/apache/velocity/velocity/1.7/velocity-1.7.pom
Downloaded from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/apache/velocity/velocity/1.7/velocity-1.7.pom (11 kB at 31 kB/s)
Downloading from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/commons-lang/commons-lang/2.4/commons-lang-2.4.pom
Downloaded from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/commons-lang/commons-lang/2.4/commons-lang-2.4.pom (14 kB at 60 kB/s)
Downloading from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/apache/maven/wagon/wagon-provider-api/3.3.3/wagon-provider-api-3.3.3.pom
Downloaded from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/apache/maven/wagon/wagon-provider-api/3.3.3/wagon-provider-api-3.3.3.pom (1.9 kB at 5.5 kB/s)
Downloading from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/apache/maven/wagon/wagon/3.3.3/wagon-3.3.3.pom
Downloaded from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/apache/maven/wagon/wagon/3.3.3/wagon-3.3.3.pom (21 kB at 93 kB/s)
Downloading from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/codehaus/plexus/plexus-interactivity-api/1.0-alpha-6/plexus-interactivity-api-1.0-alpha-6.pom
Downloaded from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/codehaus/plexus/plexus-interactivity-api/1.0-alpha-6/plexus-interactivity-api-1.0-alpha-6.pom (726 B at 2.2 kB/s)
Downloading from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/codehaus/plexus/plexus-interactivity/1.0-alpha-6/plexus-interactivity-1.0-alpha-6.pom
Downloaded from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/codehaus/plexus/plexus-interactivity/1.0-alpha-6/plexus-interactivity-1.0-alpha-6.pom (1.1 kB at 4.6 kB/s)
Downloading from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/codehaus/plexus/plexus-components/1.1.9/plexus-components-1.1.9.pom
Downloaded from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/codehaus/plexus/plexus-components/1.1.9/plexus-components-1.1.9.pom (2.4 kB at 7.1 kB/s)
Downloading from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/codehaus/plexus/plexus/1.0.10/plexus-1.0.10.pom
Downloaded from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/codehaus/plexus/plexus/1.0.10/plexus-1.0.10.pom (8.2 kB at 36 kB/s)
Downloading from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/apache/maven/shared/maven-script-interpreter/1.0/maven-script-interpreter-1.0.pom
Downloaded from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/apache/maven/shared/maven-script-interpreter/1.0/maven-script-interpreter-1.0.pom (3.8 kB at 12 kB/s)
Downloading from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/apache/maven/shared/maven-shared-components/17/maven-shared-components-17.pom
Downloaded from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/apache/maven/shared/maven-shared-components/17/maven-shared-components-17.pom (8.7 kB at 24 kB/s)
Downloading from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/apache/maven/maven-parent/21/maven-parent-21.pom
Downloaded from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/apache/maven/maven-parent/21/maven-parent-21.pom (26 kB at 106 kB/s)
Downloading from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/apache/apache/10/apache-10.pom
Downloaded from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/apache/apache/10/apache-10.pom (15 kB at 46 kB/s)
Downloading from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/codehaus/groovy/groovy/1.8.3/groovy-1.8.3.pom
Downloaded from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/codehaus/groovy/groovy/1.8.3/groovy-1.8.3.pom (32 kB at 127 kB/s)
Downloading from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/antlr/antlr/2.7.7/antlr-2.7.7.pom
Downloaded from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/antlr/antlr/2.7.7/antlr-2.7.7.pom (632 B at 2.0 kB/s)
Downloading from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/asm/asm/3.2/asm-3.2.pom
Downloaded from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/asm/asm/3.2/asm-3.2.pom (264 B at 1.2 kB/s)
Downloading from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/asm/asm-parent/3.2/asm-parent-3.2.pom
Downloaded from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/asm/asm-parent/3.2/asm-parent-3.2.pom (4.4 kB at 13 kB/s)
Downloading from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/asm/asm-commons/3.2/asm-commons-3.2.pom
Downloaded from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/asm/asm-commons/3.2/asm-commons-3.2.pom (415 B at 1.5 kB/s)
Downloading from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/asm/asm-tree/3.2/asm-tree-3.2.pom
Downloaded from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/asm/asm-tree/3.2/asm-tree-3.2.pom (404 B at 1.2 kB/s)
Downloading from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/asm/asm-util/3.2/asm-util-3.2.pom
Downloaded from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/asm/asm-util/3.2/asm-util-3.2.pom (409 B at 1.7 kB/s)
Downloading from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/asm/asm-analysis/3.2/asm-analysis-3.2.pom
Downloaded from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/asm/asm-analysis/3.2/asm-analysis-3.2.pom (417 B at 1.2 kB/s)
Downloading from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/beanshell/bsh/2.0b4/bsh-2.0b4.pom
Downloaded from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/beanshell/bsh/2.0b4/bsh-2.0b4.pom (1.2 kB at 3.7 kB/s)
Downloading from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/beanshell/beanshell/2.0b4/beanshell-2.0b4.pom
Downloaded from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/beanshell/beanshell/2.0b4/beanshell-2.0b4.pom (1.4 kB at 3.5 kB/s)
Downloading from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/apache/ant/ant/1.8.1/ant-1.8.1.pom
Downloaded from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/apache/ant/ant/1.8.1/ant-1.8.1.pom (8.8 kB at 38 kB/s)
Downloading from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/apache/ant/ant-parent/1.8.1/ant-parent-1.8.1.pom
Downloaded from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/apache/ant/ant-parent/1.8.1/ant-parent-1.8.1.pom (4.3 kB at 13 kB/s)
Downloading from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/apache/maven/archetype/archetype-catalog/3.1.2/archetype-catalog-3.1.2.jar
Downloading from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/apache/ivy/ivy/2.4.0/ivy-2.4.0.jar
Downloading from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/codehaus/groovy/groovy/2.4.16/groovy-2.4.16.jar
Downloading from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/apache/maven/archetype/archetype-common/3.1.2/archetype-common-3.1.2.jar
Downloading from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/apache/maven/archetype/archetype-descriptor/3.1.2/archetype-descriptor-3.1.2.jar
Downloaded from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/apache/maven/archetype/archetype-descriptor/3.1.2/archetype-descriptor-3.1.2.jar (24 kB at 51 kB/s)
Downloading from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/net/sourceforge/jchardet/jchardet/1.0/jchardet-1.0.jar
Downloaded from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/apache/maven/archetype/archetype-catalog/3.1.2/archetype-catalog-3.1.2.jar (19 kB at 28 kB/s)
Downloading from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/codehaus/plexus/plexus-component-annotations/1.7.1/plexus-component-annotations-1.7.1.jar
Downloaded from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/net/sourceforge/jchardet/jchardet/1.0/jchardet-1.0.jar (27 kB at 28 kB/s)
Downloading from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/jdom/jdom/1.0/jdom-1.0.jar
Downloaded from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/apache/maven/archetype/archetype-common/3.1.2/archetype-common-3.1.2.jar (185 kB at 167 kB/s)
Downloading from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/apache/maven/maven-artifact/3.0/maven-artifact-3.0.jar
Downloaded from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/codehaus/plexus/plexus-component-annotations/1.7.1/plexus-component-annotations-1.7.1.jar (4.3 kB at 3.6 kB/s)
Downloading from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/apache/maven/maven-settings-builder/3.0/maven-settings-builder-3.0.jar
Downloaded from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/apache/maven/maven-artifact/3.0/maven-artifact-3.0.jar (52 kB at 34 kB/s)
Downloading from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/commons-io/commons-io/2.2/commons-io-2.2.jar
Downloaded from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/apache/maven/maven-settings-builder/3.0/maven-settings-builder-3.0.jar (38 kB at 23 kB/s)
Downloading from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/codehaus/plexus/plexus-velocity/1.1.8/plexus-velocity-1.1.8.jar
Downloaded from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/jdom/jdom/1.0/jdom-1.0.jar (153 kB at 89 kB/s)
Downloaded from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/apache/ivy/ivy/2.4.0/ivy-2.4.0.jar (1.3 MB at 743 kB/s)
Downloading from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/apache/velocity/velocity/1.7/velocity-1.7.jar
Downloading from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/commons-lang/commons-lang/2.4/commons-lang-2.4.jar
Downloaded from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/codehaus/groovy/groovy/2.4.16/groovy-2.4.16.jar (4.7 MB at 2.7 MB/s)
Downloading from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/apache/maven/wagon/wagon-provider-api/3.3.3/wagon-provider-api-3.3.3.jar
Downloaded from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/codehaus/plexus/plexus-velocity/1.1.8/plexus-velocity-1.1.8.jar (7.9 kB at 4.1 kB/s)
Downloading from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/codehaus/plexus/plexus-utils/3.2.0/plexus-utils-3.2.0.jar
Downloaded from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/commons-io/commons-io/2.2/commons-io-2.2.jar (174 kB at 89 kB/s)
Downloading from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/codehaus/plexus/plexus-interactivity-api/1.0-alpha-6/plexus-interactivity-api-1.0-alpha-6.jar
Downloaded from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/apache/maven/wagon/wagon-provider-api/3.3.3/wagon-provider-api-3.3.3.jar (56 kB at 25 kB/s)
Downloading from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/apache/maven/maven-plugin-api/3.0/maven-plugin-api-3.0.jar
Downloaded from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/codehaus/plexus/plexus-interactivity-api/1.0-alpha-6/plexus-interactivity-api-1.0-alpha-6.jar (12 kB at 5.2 kB/s)
Downloading from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/sonatype/sisu/sisu-inject-plexus/1.4.2/sisu-inject-plexus-1.4.2.jar
Downloaded from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/codehaus/plexus/plexus-utils/3.2.0/plexus-utils-3.2.0.jar (263 kB at 99 kB/s)
Downloading from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/sonatype/sisu/sisu-inject-bean/1.4.2/sisu-inject-bean-1.4.2.jar
Downloaded from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/apache/maven/maven-plugin-api/3.0/maven-plugin-api-3.0.jar (49 kB at 18 kB/s)
Downloaded from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/commons-lang/commons-lang/2.4/commons-lang-2.4.jar (262 kB at 95 kB/s)
Downloading from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/apache/maven/maven-core/3.0/maven-core-3.0.jar
Downloading from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/sonatype/sisu/sisu-guice/2.1.7/sisu-guice-2.1.7-noaop.jar
Downloaded from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/sonatype/sisu/sisu-inject-plexus/1.4.2/sisu-inject-plexus-1.4.2.jar (202 kB at 67 kB/s)
Downloading from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/apache/maven/maven-repository-metadata/3.0/maven-repository-metadata-3.0.jar
Downloaded from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/apache/velocity/velocity/1.7/velocity-1.7.jar (450 kB at 146 kB/s)
Downloading from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/apache/maven/maven-model-builder/3.0/maven-model-builder-3.0.jar
Downloaded from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/sonatype/sisu/sisu-inject-bean/1.4.2/sisu-inject-bean-1.4.2.jar (153 kB at 48 kB/s)
Downloading from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/apache/maven/maven-aether-provider/3.0/maven-aether-provider-3.0.jar
Downloaded from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/apache/maven/maven-repository-metadata/3.0/maven-repository-metadata-3.0.jar (30 kB at 8.8 kB/s)
Downloading from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/sonatype/aether/aether-impl/1.7/aether-impl-1.7.jar
Downloaded from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/apache/maven/maven-aether-provider/3.0/maven-aether-provider-3.0.jar (51 kB at 14 kB/s)
Downloading from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/sonatype/aether/aether-spi/1.7/aether-spi-1.7.jar
Downloaded from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/apache/maven/maven-model-builder/3.0/maven-model-builder-3.0.jar (148 kB at 41 kB/s)
Downloading from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/sonatype/aether/aether-api/1.7/aether-api-1.7.jar
Downloaded from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/sonatype/aether/aether-impl/1.7/aether-impl-1.7.jar (106 kB at 28 kB/s)
Downloading from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/sonatype/aether/aether-util/1.7/aether-util-1.7.jar
Downloaded from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/sonatype/aether/aether-spi/1.7/aether-spi-1.7.jar (14 kB at 3.4 kB/s)
Downloading from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/codehaus/plexus/plexus-interpolation/1.14/plexus-interpolation-1.14.jar
Downloaded from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/sonatype/aether/aether-api/1.7/aether-api-1.7.jar (74 kB at 18 kB/s)
Downloading from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/codehaus/plexus/plexus-classworlds/2.2.3/plexus-classworlds-2.2.3.jar
Downloaded from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/apache/maven/maven-core/3.0/maven-core-3.0.jar (527 kB at 125 kB/s)
Downloading from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/sonatype/plexus/plexus-sec-dispatcher/1.3/plexus-sec-dispatcher-1.3.jar
Downloaded from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/sonatype/sisu/sisu-guice/2.1.7/sisu-guice-2.1.7-noaop.jar (472 kB at 111 kB/s)
Downloading from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/sonatype/plexus/plexus-cipher/1.4/plexus-cipher-1.4.jar
Downloaded from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/sonatype/aether/aether-util/1.7/aether-util-1.7.jar (108 kB at 25 kB/s)
Downloading from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/apache/maven/maven-model/3.0/maven-model-3.0.jar
Downloaded from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/codehaus/plexus/plexus-interpolation/1.14/plexus-interpolation-1.14.jar (61 kB at 14 kB/s)
Downloading from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/apache/maven/maven-settings/3.0/maven-settings-3.0.jar
Downloaded from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/codehaus/plexus/plexus-classworlds/2.2.3/plexus-classworlds-2.2.3.jar (46 kB at 10 kB/s)
Downloading from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/apache/maven/shared/maven-invoker/3.0.1/maven-invoker-3.0.1.jar
Downloaded from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/sonatype/plexus/plexus-cipher/1.4/plexus-cipher-1.4.jar (13 kB at 3.0 kB/s)
Downloading from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/apache/maven/shared/maven-shared-utils/3.2.1/maven-shared-utils-3.2.1.jar
Downloaded from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/sonatype/plexus/plexus-sec-dispatcher/1.3/plexus-sec-dispatcher-1.3.jar (29 kB at 6.2 kB/s)
Downloading from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/apache/maven/shared/maven-artifact-transfer/0.11.0/maven-artifact-transfer-0.11.0.jar
Downloaded from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/apache/maven/maven-model/3.0/maven-model-3.0.jar (165 kB at 35 kB/s)
Downloading from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/apache/maven/shared/maven-common-artifact-filters/3.0.1/maven-common-artifact-filters-3.0.1.jar
Downloaded from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/apache/maven/shared/maven-invoker/3.0.1/maven-invoker-3.0.1.jar (33 kB at 6.9 kB/s)
Downloading from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/commons-codec/commons-codec/1.11/commons-codec-1.11.jar
Downloaded from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/apache/maven/maven-settings/3.0/maven-settings-3.0.jar (47 kB at 9.7 kB/s)
Downloading from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/slf4j/slf4j-api/1.7.5/slf4j-api-1.7.5.jar
Downloaded from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/apache/maven/shared/maven-artifact-transfer/0.11.0/maven-artifact-transfer-0.11.0.jar (128 kB at 26 kB/s)
Downloading from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/commons-collections/commons-collections/3.2.1/commons-collections-3.2.1.jar
Downloaded from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/apache/maven/shared/maven-shared-utils/3.2.1/maven-shared-utils-3.2.1.jar (167 kB at 33 kB/s)
Downloading from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/apache/maven/shared/maven-script-interpreter/1.0/maven-script-interpreter-1.0.jar
Downloaded from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/apache/maven/shared/maven-common-artifact-filters/3.0.1/maven-common-artifact-filters-3.0.1.jar (61 kB at 12 kB/s)
Downloading from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/beanshell/bsh/2.0b4/bsh-2.0b4.jar
Downloaded from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/slf4j/slf4j-api/1.7.5/slf4j-api-1.7.5.jar (26 kB at 5.1 kB/s)
Downloading from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/apache/ant/ant/1.8.1/ant-1.8.1.jar
Downloaded from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/apache/maven/shared/maven-script-interpreter/1.0/maven-script-interpreter-1.0.jar (21 kB at 3.8 kB/s)
Downloaded from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/commons-codec/commons-codec/1.11/commons-codec-1.11.jar (335 kB at 60 kB/s)
Downloaded from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/beanshell/bsh/2.0b4/bsh-2.0b4.jar (282 kB at 48 kB/s)
Downloaded from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/commons-collections/commons-collections/3.2.1/commons-collections-3.2.1.jar (575 kB at 94 kB/s)
Downloaded from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/apache/ant/ant/1.8.1/ant-1.8.1.jar (1.5 MB at 241 kB/s)
[INFO] Generating project in Interactive mode
[WARNING] No archetype found in remote catalog. Defaulting to internal catalog
[INFO] Archetype repository not defined. Using the one from [org.apache.maven.archetypes:maven-archetype-webapp:1.0] found in catalog internal
Downloading from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/apache/maven/archetypes/maven-archetype-webapp/1.4/maven-archetype-webapp-1.4.pom
Downloaded from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/apache/maven/archetypes/maven-archetype-webapp/1.4/maven-archetype-webapp-1.4.pom (1.4 kB at 4.1 kB/s)
Downloading from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/apache/maven/archetypes/maven-archetype-bundles/1.4/maven-archetype-bundles-1.4.pom
Downloaded from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/apache/maven/archetypes/maven-archetype-bundles/1.4/maven-archetype-bundles-1.4.pom (4.5 kB at 17 kB/s)
Downloading from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/apache/maven/archetypes/maven-archetype-webapp/1.4/maven-archetype-webapp-1.4.jar
Downloaded from alimaven: http://maven.aliyun.com/nexus/content/repositories/central/org/apache/maven/archetypes/maven-archetype-webapp/1.4/maven-archetype-webapp-1.4.jar (6.8 kB at 28 kB/s)
Define value for property 'groupId': com.hello
Define value for property 'artifactId': main
Define value for property 'version' 1.0-SNAPSHOT: :
Define value for property 'package' com.hello: :
Confirm properties configuration:
groupId: com.hello
artifactId: main
version: 1.0-SNAPSHOT
package: com.hello
 Y: : y
[INFO] ----------------------------------------------------------------------------
[INFO] Using following parameters for creating project from Archetype: maven-archetype-webapp:1.4
[INFO] ----------------------------------------------------------------------------
[INFO] Parameter: groupId, Value: com.hello
[INFO] Parameter: artifactId, Value: main
[INFO] Parameter: version, Value: 1.0-SNAPSHOT
[INFO] Parameter: package, Value: com.hello
[INFO] Parameter: packageInPathFormat, Value: com/hello
[INFO] Parameter: package, Value: com.hello
[INFO] Parameter: version, Value: 1.0-SNAPSHOT
[INFO] Parameter: groupId, Value: com.hello
[INFO] Parameter: artifactId, Value: main
[INFO] Project created from Archetype in dir: F:\Java\helloworld\helloWebapp\main
[INFO] ------------------------------------------------------------------------
[INFO] BUILD SUCCESS
[INFO] ------------------------------------------------------------------------
[INFO] Total time:  01:45 min
[INFO] Finished at: 2020-04-09T22:47:32+08:00
[INFO] ------------------------------------------------------------------------

<!-- 20200409 -->