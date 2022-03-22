# snap 安装docker之后 
执行docker命令  

    Got permission denied while trying to connect to the Docker daemon socket at unix:///var/run/docker.sock: Get "http://%2Fvar%2Frun%2Fdocker.sock/v1.24/containers/json": dial unix /var/run/docker.sock: connect: permission denied

## 解决方案
添加用户组，赋高级权限

```bash
sudo groupadd docker     #添加docker用户组
sudo usermod -a -G docker $USER  #将登陆用户加入到docker用户组中
newgrp docker     #更新用户组
docker ps    #测试docker命令是否可以使用sudo正常使用
```

完成之后需要重启机器

一般 docker 用户组已经建立