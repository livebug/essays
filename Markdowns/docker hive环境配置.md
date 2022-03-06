# hive 环境搭建

## 1. 准备一个 mysql 容器 （因为镜像中不带mysql） 非常简单
### 1.1 准备musql容器
```bash
# docker 中下载 mysql
docker pull mysql:latest
#启动
docker run -itd --name hive-server \
--net=hadoop --hostname hive-server \
-p 23306:3306 -e MYSQL_ROOT_PASSWORD=123456 mysql
#进入容器
docker exec -it mysql bash
```
### 1.2 配置mysql
```bash
#登录mysql
mysql -u root -p
#[可选]修改root密码 改不改都行，后面配置使用的都是用户hive
ALTER USER 'root'@'localhost' IDENTIFIED BY 'Lzslov123!';
#添加远程登录用户
CREATE USER 'hive'@'%' IDENTIFIED WITH mysql_native_password BY 'hive!';
GRANT ALL PRIVILEGES ON *.* TO 'hive'@'%';
#刷新权限
flush privileges
```

## 2. hive 集群
### 2.1 hive集群镜像拉取
```bash
docker push livebug/hive:tagname
```
### 2.2 执行容器启动脚本`./start-container.sh `
```bash
#!/bin/bash
# ./start-container.sh 
# the default node number is  默认是4个可以自动调整
N=${1:-4}
# start hadoop master container
sudo docker rm -f hadoop-master &> /dev/null
echo "start hadoop-master &hive container..."
sudo docker run -itd \
                --net=hadoop \
                -p 9870:9870 \
                -p 8088:8088 \
                -p 19888:19888 \
                -p 10000:10000 \
                -p 10002:10002 \
                -p 9999:9999 \
                -p 8042:8042 \
                --name hadoop-master \
                --hostname hadoop-master \
                -v /opt/hadoop:/opt \
                livebug/hive:3.1.2 &> /dev/null


# start hadoop slave container
i=1
while [ $i -lt $N ]
do
	sudo docker rm -f hadoop-slave$i &> /dev/null
	echo "start hadoop-slave$i container..."
	sudo docker run -itd \
	                --net=hadoop \
	                --name hadoop-slave$i \
                    -p ${i}8042:8042 \
	                --hostname hadoop-slave$i \
	                livebug/hive:3.1.2 &> /dev/null
	i=$(( $i + 1 ))
done 

# get into hadoop master container
sudo docker exec -it hadoop-master bash

```
### 2.3 进入 `hadoop-master` 容器，执行集群启动脚本 `./start-hadoop.sh`
启动之后尝试以下连接
+ http://localhost:8088/cluster
+ http://localhost:8042/node
+ http://localhost:18042/node
+ http://localhost:28042/node
+ http://localhost:38042/node
### 2.4 启动historyserver[可忽略]
```bash
root@hadoop-master:/usr/local/hadoop/sbin# mr-jobhistory-daemon.sh start historyserver 
WARNING: Use of this script to start the MR JobHistory daemon is deprecated.
WARNING: Attempting to execute replacement "mapred --daemon start" instead.
# mapred --daemon start historyserver
```
访问 http://localhost:19888/jobhistory

### 2.5 阶段测试 
1. 执行单词计数统计测试脚本 
2. 并且history如果打开的话，还可以看到作业历史

## 3.hive
### 3.1 初始换hive
```bash
root@hadoop-master:~# schematool -dbType mysql -initSchema
Metastore connection URL:        jdbc:mysql://hive-server:3306/hive?createDatabaseIfNotExist=true
Metastore Connection Driver :    com.mysql.cj.jdbc.Driver
Metastore connection User:       hive
Starting metastore schema initialization to 3.1.0
Initialization script hive-schema-3.1.0.mysql.sql 
Initialization script completed
schemaTool completed
```
此时mysql库中已经新建`hive`库，如果需要重新来，记得在mysql中把`hive`库删掉
### 3.1.1 为hadoop操作赋权
```bash
    hadoop fs -chmod -R 777 /
```
### 3.2 尝试hive
```bash
root@hadoop-master:~# hive
Hive Session ID = 55b39bc4-cc46-42da-b18c-45964286684a

Logging initialized using configuration in jar:file:/usr/local/hive/lib/hive-common-3.1.2.jar!/hive-log4j2.properties Async: true
Hive-on-MR is deprecated in Hive 2 and may not be available in the future versions. Consider using a different execution engine (i.e. spark, tez) or using Hive 1.X releases.
Hive Session ID = ca58270e-7a99-4f90-9efc-a421415dc29c
hive> show databases;
OK
default
Time taken: 0.478 seconds, Fetched: 1 row(s)
```
### 3.3 启动 hiveserver2
```bash
root@hadoop-master:~# nohup hiveserver2 > hiveserver2.log &
2022-03-06 14:46:29: Starting HiveServer2
Hive Session ID = ae2065a5-e1d3-4d6f-809d-68b3078afea1
```
可访问 http://localhost:10002/ 查看hive连接

### 3.4 连接 hiveserver2
```bash
beeline -u jdbc:hive2://hadoop-master:10000 -n hive

beeline -u jdbc:hive2://hadoop-master:10000 -n root
Connecting to jdbc:hive2://hadoop-master:10000
Connected to: Apache Hive (version 3.1.2)
Driver: Hive JDBC (version 3.1.2)
Transaction isolation: TRANSACTION_REPEATABLE_READ
Beeline version 3.1.2 by Apache Hive
0: jdbc:hive2://hadoop-master:10000> 
```

### 3.5 使用第三方软件尝试连接