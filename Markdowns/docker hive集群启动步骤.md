

## 启动集群容器
```bash
root@hadoop-master:~#  ./start-container.sh 
start hadoop-master &hive container...
start hadoop-slave1 container...
start hadoop-slave2 container...
start hadoop-slave3 container...
```

## 启动hadoop集群
```bash
root@hadoop-master:~#./start-hadoop.sh 
Starting namenodes on [hadoop-master]
hadoop-master: Warning: Permanently added 'hadoop-master,172.18.0.3' (ECDSA) to the list of known hosts.
hadoop-master: WARNING: HADOOP_NAMENODE_OPTS has been replaced by HDFS_NAMENODE_OPTS. Using value of HADOOP_NAMENODE_OPTS.
Starting datanodes
WARNING: HADOOP_SECURE_DN_LOG_DIR has been replaced by HADOOP_SECURE_LOG_DIR. Using value of HADOOP_SECURE_DN_LOG_DIR.
hadoop-slave2: Warning: Permanently added 'hadoop-slave2,172.18.0.5' (ECDSA) to the list of known hosts.
hadoop-slave3: Warning: Permanently added 'hadoop-slave3,172.18.0.6' (ECDSA) to the list of known hosts.
hadoop-slave1: Warning: Permanently added 'hadoop-slave1,172.18.0.4' (ECDSA) to the list of known hosts.
hadoop-master: Warning: Permanently added 'hadoop-master,172.18.0.3' (ECDSA) to the list of known hosts.
hadoop-slave2: WARNING: HADOOP_SECURE_DN_LOG_DIR has been replaced by HADOOP_SECURE_LOG_DIR. Using value of HADOOP_SECURE_DN_LOG_DIR.
hadoop-slave3: WARNING: HADOOP_SECURE_DN_LOG_DIR has been replaced by HADOOP_SECURE_LOG_DIR. Using value of HADOOP_SECURE_DN_LOG_DIR.
hadoop-slave2: WARNING: HADOOP_DATANODE_OPTS has been replaced by HDFS_DATANODE_OPTS. Using value of HADOOP_DATANODE_OPTS.
hadoop-slave3: WARNING: HADOOP_DATANODE_OPTS has been replaced by HDFS_DATANODE_OPTS. Using value of HADOOP_DATANODE_OPTS.
hadoop-slave1: WARNING: HADOOP_SECURE_DN_LOG_DIR has been replaced by HADOOP_SECURE_LOG_DIR. Using value of HADOOP_SECURE_DN_LOG_DIR.
hadoop-slave1: WARNING: HADOOP_DATANODE_OPTS has been replaced by HDFS_DATANODE_OPTS. Using value of HADOOP_DATANODE_OPTS.
hadoop-master: WARNING: HADOOP_SECURE_DN_LOG_DIR has been replaced by HADOOP_SECURE_LOG_DIR. Using value of HADOOP_SECURE_DN_LOG_DIR.
hadoop-master: WARNING: HADOOP_DATANODE_OPTS has been replaced by HDFS_DATANODE_OPTS. Using value of HADOOP_DATANODE_OPTS.
Starting secondary namenodes [hadoop-master]
hadoop-master: Warning: Permanently added 'hadoop-master,172.18.0.3' (ECDSA) to the list of known hosts.
hadoop-master: WARNING: HADOOP_SECONDARYNAMENODE_OPTS has been replaced by HDFS_SECONDARYNAMENODE_OPTS. Using value of HADOOP_SECONDARYNAMENODE_OPTS.
Starting resourcemanager
Starting nodemanagers
hadoop-master: Warning: Permanently added 'hadoop-master,172.18.0.3' (ECDSA) to the list of known hosts.
hadoop-slave2: Warning: Permanently added 'hadoop-slave2,172.18.0.5' (ECDSA) to the list of known hosts.
hadoop-slave1: Warning: Permanently added 'hadoop-slave1,172.18.0.4' (ECDSA) to the list of known hosts.
hadoop-slave3: Warning: Permanently added 'hadoop-slave3,172.18.0.6' (ECDSA) to the list of known hosts.
```
+ http://localhost:8088/cluster
+ http://localhost:8042/node
+ http://localhost:18042/node
+ http://localhost:28042/node
+ http://localhost:38042/node

## 启动historyserver[可忽略]
```bash
root@hadoop-master:/usr/local/hadoop/sbin# mr-jobhistory-daemon.sh start historyserver 
WARNING: Use of this script to start the MR JobHistory daemon is deprecated.
WARNING: Attempting to execute replacement "mapred --daemon start" instead.
# mapred --daemon start historyserver
```
访问 http://localhost:19888/jobhistory

### 阶段测试 
1. 执行单词计数统计测试脚本 
2. 并且history如果打开的话，还可以看到作业历史
```bash
root@hadoop-master:~# ./run-wordcount.sh 
2022-03-06 14:38:01,070 INFO client.DefaultNoHARMFailoverProxyProvider: Connecting to ResourceManager at hadoop-master/172.18.0.3:8032
2022-03-06 14:38:01,297 INFO mapreduce.JobResourceUploader: Disabling Erasure Coding for path: /tmp/hadoop-yarn/staging/root/.staging/job_1646548619494_0001
2022-03-06 14:38:01,472 INFO input.FileInputFormat: Total input files to process : 2
2022-03-06 14:38:01,659 INFO mapreduce.JobSubmitter: number of splits:2
2022-03-06 14:38:01,738 INFO mapreduce.JobSubmitter: Submitting tokens for job: job_1646548619494_0001
2022-03-06 14:38:01,738 INFO mapreduce.JobSubmitter: Executing with tokens: []
2022-03-06 14:38:01,863 INFO conf.Configuration: resource-types.xml not found
2022-03-06 14:38:01,863 INFO resource.ResourceUtils: Unable to find 'resource-types.xml'.
2022-03-06 14:38:02,016 INFO impl.YarnClientImpl: Submitted application application_1646548619494_0001
2022-03-06 14:38:02,043 INFO mapreduce.Job: The url to track the job: http://hadoop-master:8088/proxy/application_1646548619494_0001/
2022-03-06 14:38:02,043 INFO mapreduce.Job: Running job: job_1646548619494_0001
2022-03-06 14:38:07,095 INFO mapreduce.Job: Job job_1646548619494_0001 running in uber mode : false
2022-03-06 14:38:07,096 INFO mapreduce.Job:  map 0% reduce 0%
2022-03-06 14:38:12,133 INFO mapreduce.Job:  map 100% reduce 0%
2022-03-06 14:38:16,149 INFO mapreduce.Job:  map 100% reduce 100%
2022-03-06 14:38:16,156 INFO mapreduce.Job: Job job_1646548619494_0001 completed successfully
2022-03-06 14:38:16,212 INFO mapreduce.Job: Counters: 54
        File System Counters
                FILE: Number of bytes read=56
                FILE: Number of bytes written=820914
                FILE: Number of read operations=0
                FILE: Number of large read operations=0
                FILE: Number of write operations=0
                HDFS: Number of bytes read=258
                HDFS: Number of bytes written=26
                HDFS: Number of read operations=11
                HDFS: Number of large read operations=0
                HDFS: Number of write operations=2
                HDFS: Number of bytes read erasure-coded=0
        Job Counters 
                Launched map tasks=2
                Launched reduce tasks=1
                Data-local map tasks=2
                Total time spent by all maps in occupied slots (ms)=5300
                Total time spent by all reduces in occupied slots (ms)=1559
                Total time spent by all map tasks (ms)=5300
                Total time spent by all reduce tasks (ms)=1559
                Total vcore-milliseconds taken by all map tasks=5300
                Total vcore-milliseconds taken by all reduce tasks=1559
                Total megabyte-milliseconds taken by all map tasks=5427200
                Total megabyte-milliseconds taken by all reduce tasks=1596416
        Map-Reduce Framework
                Map input records=2
                Map output records=4
                Map output bytes=42
                Map output materialized bytes=62
                Input split bytes=232
                Combine input records=4
                Combine output records=4
                Reduce input groups=3
                Reduce shuffle bytes=62
                Reduce input records=4
                Reduce output records=3
                Spilled Records=8
                Shuffled Maps =2
                Failed Shuffles=0
                Merged Map outputs=2
                GC time elapsed (ms)=103
                CPU time spent (ms)=1670
                Physical memory (bytes) snapshot=904417280
                Virtual memory (bytes) snapshot=7767515136
                Total committed heap usage (bytes)=886046720
                Peak Map Physical memory (bytes)=346542080
                Peak Map Virtual memory (bytes)=2587172864
                Peak Reduce Physical memory (bytes)=212193280
                Peak Reduce Virtual memory (bytes)=2593439744
        Shuffle Errors
                BAD_ID=0
                CONNECTION=0
                IO_ERROR=0
                WRONG_LENGTH=0
                WRONG_MAP=0
                WRONG_REDUCE=0
        File Input Format Counters 
                Bytes Read=26
        File Output Format Counters 
                Bytes Written=26

input file1.txt:
Hello Hadoop

input file2.txt:
Hello Docker

wordcount output:
Docker  1
Hadoop  1
Hello   2
```

---

到此 hadoop集群启动成功，下面启动hive

--- 
## 初始换hive

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
此时mysql库中已经新建`hive`库
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
## 启动 hiveserver2
```bash
root@hadoop-master:~# nohup hiveserver2 > hiveserver2.log &
2022-03-06 14:46:29: Starting HiveServer2
Hive Session ID = ae2065a5-e1d3-4d6f-809d-68b3078afea1
```

http://localhost:10002/

### 连接 hiveserver2
```bash
beeline -u jdbc:hive2://hadoop-master:10000 -n root
Connecting to jdbc:hive2://hadoop-master:10000
Connected to: Apache Hive (version 3.1.2)
Driver: Hive JDBC (version 3.1.2)
Transaction isolation: TRANSACTION_REPEATABLE_READ
Beeline version 3.1.2 by Apache Hive
0: jdbc:hive2://hadoop-master:10000> 
```