# docker 部署 TDH quickstart
## 拉取镜像

    docker pull cloudera/quickstart

## 部署命令

    docker run \
    -idt \
    --hostname=quickstart.cloudera \
    --privileged=true \
    -p 8020:8020 -p 7180:7180 -p 21050:21050 -p 20070:50070 -p 20075:50075 \
    -p 20010:50010 -p 20020:50020 -p 28890:8890 -p 60010:60010 -p 10002:10002 \
    -p 25010:25010 -p 25020:25020 -p 18088:18088 -p 28088:8088 -p 19888:19888 \
    -p 7187:7187 -p 21000:11000 -p 28888:8888 \
    --name=mycdh \
    cloudera/quickstart /usr/bin/docker-quickstart 


## 部署网站

https://www.cnblogs.com/lijiong/p/15508134.html


### 部署问题1：端口占用

    netsh interface ipv4 show excludedportrange protocol=tcp

    协议 tcp 端口排除范围

    开始端口    结束端口
    ----------    --------
      1079        1178
      1179        1278
      1279        1378
      1379        1478
      1479        1578
      1617        1716
      1967        2066
      2067        2166
      2180        2279
      2280        2379
      2380        2479
      2480        2579
      3398        3497
      3498        3597
      5357        5357
     28385       28385
     28390       28390
     50000       50059     *

    * - 管理的端口排除。

替换端口即可

### 部署问题2：运行是 wsl 报错 139 

问题解释：wsl内存不够；

修改办法：在使用WSL2 跑 Docker 时，容器可能会因为内存不足显示Exited (139)。

这个是wsl2的锅，解决方案如下[1]。

在Windows 10 操作系统的系统盘- 用户 - <用户名>目录下，修改`.wslconfig`文件（如`C:\Users\zhu\.wslconfig`)，若没有这个文件，则需要先创建。

在其中修改/添加如下内容：

    [wsl2]
    kernelCommandLine = vsyscall=emulate
