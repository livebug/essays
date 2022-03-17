# 编译运行
执行`mvn clean package`命令进行编译

然后右击war包，执行`run on tomcat server`

然后在tomcat服务器上，右键点击`restart`

此时完成了新包的部署

网页再次打开就是新修改的内容了

# 调试

a. 执行`mvn clean package`命令进行编译

b. 然后右击war包，执行`debug on tomcat server`

c. 此时就进入调试界面了

然后热替换只是适合用于修改java文件，也就是只能热替换class文件，对于其他文件的修改，执行a->b->c