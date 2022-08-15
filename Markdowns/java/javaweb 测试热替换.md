# Java Web app Debug Hot Replace
刚开始使用Vscode 来搞java，虽然之前因为net core与angular的缘故，对vscode 还是有所熟悉的，但是对java我还是新手，跟不用提那么多的配置了。

## 创建一个java web 项目，使用maven

然后就是在本文的重点了，vacode 的调试功能以及热替换

## Debug
首先使用mvn命令进行编译打包

mvn clean package

这样在target目录下就会有project_name.war包了，右键该文件，点击`Debug on Tomcat Server`，这样就会启动调试，你打一个断点或者新增一个断点都会触发，基本的调试就不再赘述了。

点击调试会出现调试工具面板  
![./debug.png](https://gitcode.net/archive/images/-/raw/master/20220815/debug.PNG)

从左到右依次为 `暂停/启动` `单步跳过` `单步调试` `单步跳出` `重启` `断开连接` `热替换`

## Hot Replace
修改代码之后的操作是

1. 首先，保持连接不断，也就是`断开连接`不要点击；

3. 再然后，点击`热替换`，此时特替换会构建项目之后把新的 classes 包放置于服务器上，
目前测试的结果是对页面的修改不会实现热替换，只对java文件发生改变管用；


对应步骤的截图：

0. 未修改是的显示

![](https://gitcode.net/archive/images/-/raw/master/20220815/test1.PNG)

1. 修改的内容

![](https://gitcode.net/archive/images/-/raw/master/20220815/updatejavacode.PNG)

2. 点击一下热替换

![](https://gitcode.net/archive/images/-/raw/master/20220815/test2.PNG)

<!-- 20200413 -->