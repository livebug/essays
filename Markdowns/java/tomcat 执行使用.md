# maven TOMCAT7 配置
*建议:tomcat7只支持jdk1.7及以下，若是jdk1.8则需要用tomcat8及以上*
```xml
    <pluginManagement>
     <plugins>
        <plugin>
            <groupId>org.apache.tomcat.maven</groupId>
            <artifactId>tomcat7-maven-plugin</artifactId>
            <version>2.2</version>
            <configuration>
              <path>/mozi</path>
              <port>8080</port>
              <uriEncoding>UTF-8</uriEncoding>
            </configuration>
         </plugin>
      </plugins>
    </pluginManagement>

    tomcat7:run         --启动嵌入式tomcat ，并运行当前项目
    tomcat7:deploy      --部署一个web war包
    tomcat7:reload      --重新加载web war包
    tomcat7:start       --启动tomcat
    tomcat7:stop        --停止tomcat
    tomcat7:undeploy    --停止一个war包

    tomcat7 是直接将tomcat7嵌入到java项目当中，就不需要本地重新配置服务器了
    当然这种是不太合适vscode的
```
# maven TOMCAT8 配置 
https://www.jianshu.com/p/65aaf1f06408

## 第一步：配置 Tomcat 访问权限
`conf/tomcat-users.xml`文件中的 `<tomcat-users>`标签
```xml
<role rolename="manager-gui"/> 
<role rolename="manager-script"/>
<role rolename="manager-jmx"/>
<role rolename="manager-status"/>
<user password="1234" username="admin"
roles="manager-gui,manager-script,manager-jmx,manager-status" />
```
## 第二步：配置maven的settings.xml
在 `conf/settings.xml` 文件中的标签 `<servers>` 添加子标签。
```xml
<server> 
    <id>tomcat8</id>
    <username>admin</username>
    <password>1234</password>
</server>
```

## 第三步 
```xml
<build>
   <plugins>
     <plugin>
        <groupId>org.apache.maven.plugins</groupId>
        <artifactId>maven-compiler-plugin</artifactId>
        <configuration>
          <source>1.8</source>
          <target>1.8</target>
        </configuration>
     </plugin>

     <plugin>
        <groupId>org.apache.tomcat.maven</groupId>
        <artifactId>tomcat7-maven-plugin</artifactId>
        <version>2.2</version>
        <configuration>
            <!-- 直接访问 Tomcat 服务器的 manager -->
            <url>http://localhost:8080/manager/text</url>
            <server>tomcat8</server>
        </configuration>
    </plugin>
  </plugins>
</build>
```

*以上的两个配置都不合适与vscode 进行javaweb的调试*
# vscode 使用tomcat
需要安装tomcat插件
1. 先将项目打包 war 包
2. 右键 run/debug on tomcat server
3. 然后项目就启动起来了

vscode 官方使用教程链接地址：https://code.visualstudio.com/docs/java/java-tomcat-jetty#_tomcat

其中包括对tomcat以及jetty的指导视频。

简单分析一下tomcat与jetty其实对于neter来说就是IIS与net core中的Kestrel，这样说只是为了简单区分实则大不一样。

tomcat 是最重量级企业级服务器，包含高级功能；而jetty就是一个轻量的服务器，就是主要应用于分布式，对高级功能要求不到

IIS 作为net的老牌服务器，到现在也一直保持优势，图形化管理界面等等；而Kestrel是随着net core一起而生的，就包含在net core中，作为net core跨平台的服务器方案，轻重兼备的边缘服务器。

世界都是成对出现的

<!-- 20200410 -->