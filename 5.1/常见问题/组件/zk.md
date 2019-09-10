#  ZK FAQ

## zk 无法启动

**表象**

使用`./bkcec start zk`提示started，但很快EXIT退出

**原因**

1. java是否安装正常
2. 2181端口被占用
3. 上述1.2均正常，仍无法启动的异常

**解决方法**

原因1

```bash
# 使用java或者java -version命令来验证
$ java
$ java -version
```

原因2

```bash
# 检查端口
$ netstat -apn | grep 2181
tcp        0      0 :::2181                     :::*                        LISTEN      1403/java
$ kill -9 1403
$ netstat -apn | grep 2181
$
# 重新启动
```

原因3

```bash
# 进入到zk data目录，找到zoo.conf中配置的dataDir和dataLogDir路径。然后删除两个文件夹下的version -2文件夹
$ cd /data/bkce/public/zk/data

# 把有zookeeper_server.pid以及version-X开头的文件和文件夹删掉
$ rm -rf version-1 zookeeper_server.pid

# 重新启动zk，即可解决
$ ./bkcec start zk
```

上述3条确认后，仍无法启动的，可能zk.sh版本不对，请和蓝鲸运营人员联系