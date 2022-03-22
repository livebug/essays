## docker 安装 hadoop镜像 

https://caidao.gitbooks.io/reading-notes/content/you-yi-si-de-jing-li/ji-yu-docker-kuai-su-da-jian-hive-huan-jing.html


下载Docker镜像

    sudo docker pull kiwenlau/hadoop:1.0

下载GitHub仓库

    git clone https://github.com/kiwenlau/hadoop-cluster-docker

## docker 安装 mysql 8 版本

    # docker 中下载 mysql
    docker pull mysql:latest

    #启动
    docker run -itd --name hive-server \
    --net=hadoop --hostname hive-server \
    -p 23306:3306 -e MYSQL_ROOT_PASSWORD=123456 mysql

    #进入容器
    docker exec -it mysql bash

    #登录mysql
    mysql -u root -p
    ALTER USER 'root'@'localhost' IDENTIFIED BY 'Lzslov123!';

    #添加远程登录用户
    CREATE USER 'hive'@'%' IDENTIFIED WITH mysql_native_password BY 'hive!';
    GRANT ALL PRIVILEGES ON *.* TO 'hive'@'%';

    CREATE USER 'hive'@'%' IDENTIFIED WITH mysql_native_password BY 'hive!';
    GRANT ALL PRIVILEGES ON *.* TO 'hive'@'%';
    #刷新权限
    flush privileges;


下载hive https://downloads.apache.org/hive/hive-2.3.9/

    wget https://downloads.apache.org/hive/hive-2.3.9/apache-hive-2.3.9-bin.tar.gz

mysql驱动器jar包 https://repo1.maven.org/maven2/mysql/mysql-connector-java/5.1.38/
 

 https://cloud.tencent.com/developer/article/1183174


## hive 配置

### `hive-env.sh`
```bash
# Hive Configuration Directory can be controlled by:
# hive的放置目录
export HIVE_CONF_DIR=/usr/local/hive
# Folder containing extra libraries required for hive compilation/execution can be controlled by:
export HIVE_AUX_JARS_PATH=/usr/local/hive/lib
```

### `hive-site.xml` 模板是  `hive-default.xml.template`
需要关注以下几个：
```xml
<!-- java8 + mysql8 + mysql-connector-java-8.0.17.jar -->
  <property>
   <name>system:java.io.tmpdir</name>
   <value>/root/hive/tmp</value>
 </property>
 <property>
    <name>system:user.name</name>
    <value>hive</value>
</property>
<property>
    <name>javax.jdo.option.ConnectionURL</name>
    <value>jdbc:mysql://172.18.111.104:3306/hive?createDatabaseIfNotExist=true</value>
    <description>JDBC connect string for a JDBC metastore</description>
</property>
<property>
    <name>javax.jdo.option.ConnectionDriverName</name>
    <value>com.mysql.cj.jdbc.Driver</value>
    <description>Driver class name for a JDBC metastore</description>
</property>
<property>
    <name>javax.jdo.option.ConnectionUserName</name>
    <value>root</value>
    <description>username to use against metastore database</description>
</property>
<property>
    <name>javax.jdo.option.ConnectionPassword</name>
    <value>password</value>
    <description>password to use against metastore database</description>
</property>
<property>
    <name>datanucleus.schema.autoCreateAll</name>
    <value>true</value>
</property>
<property>
    <name>hive.metastore.schema.verification</name>
    <value>false</value>
</property>
```

## hive 初始化
```bash
export PATH=$PATH:$HIVE_CONF_DIR/bin

schematool -dbType mysql -initSchema
```
成功如下：
```
# schematool -dbType mysql -initSchema
Metastore connection URL:        jdbc:mysql://hive-server:3306/hive?createDatabaseIfNotExist=true
Metastore Connection Driver :    com.mysql.cj.jdbc.Driver
Metastore connection User:       hive
Starting metastore schema initialization to 3.1.0
Initialization script hive-schema-3.1.0.mysql.sql 
Initialization script completed
schemaTool completed
```
### 报错问题
1. Class path contains multiple SLF4J bindings.

    重复jar包，去掉老版本即可

2. hive 命令启动时报错：expansion character (code 0x8 at [row,col,system-id]

    删掉相应字符即可 \

3. Required field 'serverProtocolVersion' is unset! 

    修改 hadoop core-site.xml
    ```xml
    <!-- 配置hive远程访问 hive 替换相应连接用户名 -->
    <property>
	    <name>hadoop.proxyuser.hive.hosts</name>
	    <value>*</value>
    </property>
    <property>
        <name>hadoop.proxyuser.hive.groups</name>
        <value>*</value>
    </property> 
    ```

4. `Error: Error while processing statement: FAILED: Execution Error, return code 1 from org.apache.hadoop.hive.ql.exec.DDLTask. MetaException(message:Got exception: org.apache.hadoop.security.AccessControlException Permission denied: user=hive, access=WRITE, inode="/":root:supergroup:drwxr-xr-x`
    ```bash
    hadoop fs -chmod -R 777 /
    ```