# 禁止ubuntu 20.04自动休眠

https://zhuanlan.zhihu.com/p/415661679

## 1.检查休眠功能的状态以及历史记录，如下：
```bash
systemctl status sleep.target

```
## 2 执行关闭休眠功能的命令，如下
```bash
sudo systemctl mask sleep.target suspend.target hibernate.target hybrid-sleep.target
```

