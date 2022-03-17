# JavaWeb 学习路线
前言：

因为自己对 Java 和 net core 有一定的掌握，不是小白起步，并且对 javaweb 的学习目前的目标是看得懂项目结构，了解 javaweb 基本运作即可，
所以我的 javaweb 学习路程不是冲着成为一个高级 javaer 去的，更像是一个复习，所以小白慎重选择。

## java语言的学习
此处直接略过。java语言基础请转 [菜鸟教程-java教程](https://www.runoob.com/java/java-tutorial.html)

## 开发环境搭建
* 使用工具为`vscode`,之所以选择vscode当然是因为轻量简单（插件安装[Java Extension Pack](https://marketplace.visualstudio.com/items?itemName=vscjava.vscode-java-pack)
这是一个插件包会带有java需要的环境）

  额外插件：
    + Chinese (Simplified) Language Pack for Visual Studio Code（中文包）
    + tomcat for java （tomcat插件）
    + 应该推荐一点html+css+js的插件的，但是新版的vscode的功能已经不错了，涉及到前端之后的再仔细写吧

* jdk 1.8 (众所周知)

* maven，见下文介绍

* tomcat8 选择8，是因为更好的配合jdk8

<hr />

## javaweb 第一步 了解项目结构
直接maven起步，因为javaweb主要是maven来构建项目的，
学习maven，可以直接了解web项目结构

配置maven，过程见[maven 安装配置 - vscode for java](https://blog.csdn.net/qq_34332733/article/details/105461978)

创建项目，因为懒，点鼠标的不会使用代码

在 vscode 中 `ctrl+shift+p` 输入 `maven Create Maven Project`

选择模板 `maven-archetype-webapp`

其他地方很多介绍这个项目的结构的了，这里不过多解释了

```
Maven 提倡使用一个共同的标准目录结构，Maven 使用约定优于配置的原则，大家尽可能的遵守这样的目录结构。如下所示：

目录	                            目的
${basedir}	                        存放pom.xml和所有的子目录
${basedir}/src/main/java	        项目的java源代码
${basedir}/src/main/resources	    项目的资源，比如说property文件，springmvc.xml
${basedir}/src/main/webapp          web应用文件跟目录，该文件存放网站内容页面、css、js、本地图片、jsp视图页面
${basedir}/src/main/webapp/WEB-INF	web项目的信息，比如存放web.xml
${basedir}/src/test/java	        项目的测试类，比如说Junit代码
${basedir}/src/test/resources	    测试用的资源
${basedir}/target	                打包输出目录
${basedir}/target/classes	        编译输出目录
${basedir}/target/test-classes	    测试编译输出目录

```

编译打包 默认是打成`war`包的，目录在`${basedir}/target`下
    
    maven clean package 

## vscode 测试
见[vscode 测试+热替换功能介绍](https://blog.csdn.net/qq_34332733/article/details/105497776)

对打好的war包右键，选择debug on tomcat server 此时打开了调试模式

注意的一点：我提倡使用debug on tomcat Server 因为省事，但是当你修改页面的时候是需要重新打包启动的(maven clean package)。

## Servlet 学习
视频地址： [尚硅谷JAVAWEB之Servlet入门](https://www.bilibili.com/video/BV1JJ411q7ik)

因为学习 Servlet 为主，所以不是全看视频，视频的 1-14 节是主要讲 Servlet

菜鸟教程地址 [servlet-tutorial](https://www.runoob.com/servlet/servlet-tutorial.html)

主要内容包括 Servlet接口 实现Servlet接口 web.xml中Servlet配置 继承实现HttpServlet类 ServletContext web.xml中配置上下文（ServletContext）

*Context 在 web 工程中翻译为上下文，还有基本意思是环境，这是长期运行在web程序中为控制器/servlet提供基础服务，他可以提供许多的配置信息，暂时这么理解*

<!-- 20200417 -->

## 测试案例是个图书处理小系统吧
只有一张表 就是 图书表；

使用 sqlite 数据库；简单使用方法：见[]()

第一步使用Servlet ，只不过用 `html` 来替换 `jsp`，确实`jsp`对于我一个neter来说`jsp`难用之极，页面采用`html` + `bootstrap` 来实现就行了，这样一来数据传输使用`json`。

基本功能：（1）增删改查（CRUD），（2）然后就是有个身份认证和授权，（3）还有就是日志 log4j

## JavaWeb项目前后端分离
https://www.cnblogs.com/gxz-sw/p/9754975.html


## 2020425 
时隔这么多天重新收拾出来继续写，这段时间弄了一个nuc搞了一下黑苹果，没有4k显示器的我很难受，所以安装上黑苹果调试两天无果之后又回到win10,在这里做个忠告，没有充足的时间，以及富裕的财富，别搞乱七八糟的东西。

## 下面开始实现 图书管理小系统

### 第一个小问题maven生成xml版本。默认的是2.3，修改为3
其实改不改无所谓的。放一个链接：[（亲测解决）Idea创建Maven Web工程的web.xml版本问题解决](https://blog.csdn.net/sinat_34104446/article/details/82895337)

### 写界面
使用html

## SpringMVC

## SSH 和 SSM 

## SpringBoot （公司暂时没用，可以后放）