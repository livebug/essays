# wsl-ubuntu20使用与antlr安装

## wsl Ubuntu20.04 初始化

### 新增 sha 用户
```bash
$ adduser sha
```
### 指定进入根目录
```bash
$ vi /etc/passwd

找到类似的（应该是最后一个）
sha:x:1000:1001:sharif,sharif,,:/sha:/bin/bash
```
### 指定目录权限
```bash
# 为 sha 用户赋 /sha 目录权限
$  chown -R sha:sha /sha
# 赋权
$ chmod 700 /sha
```

### 将用户加入到sudo组
```bash
sudo usermod -G sudo username 
或
sudo vim /etc/sudoers
```
## antlr4 安装

不多说先放地址 https://github.com/antlr/antlr4/blob/master/doc/getting-started.md

```bash
$ cd /usr/local/lib
$ curl -O https://www.antlr.org/download/antlr-4.9-complete.jar
# 后面的写到 .bashrc 中
$ export CLASSPATH=".:/usr/local/lib/antlr-4.9-complete.jar:$CLASSPATH"
$ alias antlr4='java -Xmx500M -cp "/usr/local/lib/antlr-4.9-complete.jar:$CLASSPATH" org.antlr.v4.Tool'
$ alias grun='java -Xmx500M -cp "/usr/local/lib/antlr-4.9-complete.jar:$CLASSPATH" org.antlr.v4.gui.TestRig'
```