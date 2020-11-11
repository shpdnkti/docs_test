# 社区版 6.0 基础包快速部署

## 一、安装环境准备

###  1.1 准备机器

1. 建议操作系统： CentOS 7.6
2. 建议机器配置
   - 体验功能：建议 4 核 16 G，硬盘 50G 以上
   - 生产环境：建议 8 核 32 G，硬盘 100G 以上（可根据实际情况适当调整配置）
3. 机器数量：3 台（假设 ip 分别为：10.0.0.1，10.0.0.2，10.0.0.3）
4. 选择一台为中控机（假设为 10.0.0.1）进行安装部署操作，使用 root 账号登录。

### 1.2 获取证书

- 通过 `ifconfig` 或者 `ip addr` 命令分别获取三台机器第一个内网网卡 MAC 地址
- 前往蓝鲸官网证书生成页面（[https://bk.tencent.com/download_ssl/](https://bk.tencent.com/download_ssl/)），根据提示在输入框中填入英文分号分隔的三个 MAC 地址，生成并下载证书
- 上传证书包至中控机 `/data`
   - 证书包包名：ssl_certificates.tar.gz

### 1.3 下载安装包

- 下载安装包，选择 6.0.0 版本：[https://bk.tencent.com/download/](https://bk.tencent.com/download/)
- 上传安装包至中控机 `/data `
    - 完整包包名：bkce_src-6.0.0.tgz


### 1.4 解压相关资源包

1. 解压完整包（包含蓝鲸相关产品，如 PaaS、CMDB、JOB 等；蓝鲸依赖的 rpm 包，SaaS 镜像，定制 Python 解释器；部署脚本）

   ```bash
   cd /data
   tar xf bkce_src-6.0.0.tgz
   ```

2. 解压各个产品软件包

   ```bash
   cd /data/src/; for f in *gz;do tar xf $f; done
   ```

3. 解压证书包

    ```bash
    install -d -m 755 /data/src/cert
    tar xf ssl_certificates.tar.gz -C /data/src/cert/
    chmod 644 /data/src/cert/*
    ```
    
6.  拷贝 rpm 包文件夹到/opt/目录

    ```bash
    cp -a /data/src/yum /opt
    ```

### 1.5 自定义安装配置

1. 生成 install.config

   ```bash
   # 请根据实际机器的 IP 进行替换第一列的示例 IP 地址，确保三个 IP 之间能互相通信
   cat << EOF >/data/install/install.config
   10.0.0.1 iam,ssm,usermgr,gse,license,redis,consul,es7,monitorv3(influxdb-proxy),monitorv3(monitor),monitorv3(grafana)
   10.0.0.2 nginx,consul,mongodb,rabbitmq,appo,influxdb(bkmonitorv3),monitorv3(transfer),fta,beanstalk
   10.0.0.3 paas,cmdb,job,mysql,zk(config),kafka(config),appt,consul,log(api),nodeman(nodeman)
   EOF
   ```

2. 对  install.config  中的主机配置中控机ssh登录免密。根据提示，依次输入每台机器的root密码

   ```bash
   bash /data/install/configure_ssh_without_pass
   ```

## 二、开始部署

### 2.1 初始化操作

1. 执行初始化操作

```bash
# 快速部署暂不支持自定义安装目录
cd /data/install/
./bk_install common
```

2. 检查相关配置

```bash
./health_check/check_bk_controller.sh
```

### 2.2 部署 PaaS 

```bash
./bk_install paas
```

### 2.3 部署 app_mgr（SaaS 运行环境）

```bash
./bk_install app_mgr
```

### 2.4 部署 CMDB（配置平台）

```bash
./bk_install cmdb
```

### 2.5 部署 JOB（作业平台）

```bash
./bk_install job
```

### 2.6 部署 bknodeman（节点管理）

```bash
./bk_install bknodeman
```

### 2.7 部署 bkmonitorv3 （监控平台）

```bash
./bk_install bkmonitorv3
```

### 2.8 部署 bklog（日志平台)

```bash
./bk_install bklog
```

### 2.9 部署 fta（故障自愈后台）

```bash
./bk_install fta
```

### 2.10 部署 SaaS

请按顺序执行：
```bash
# 权限中心
./bk_install saas-o bk_iam
# 用户管理
./bk_install saas-o bk_user_manage
# 标准运维
./bk_install saas-o bk_sops
# 服务流程管理
./bk_install saas-o bk_itsm
# 故障自愈SaaS
./bk_install saas-o bk_fta_solutions
```

### 2.11 检测相关服务状态

```bash
cd /data/install/
echo bkssm bkiam usermgr paas cmdb gse job consul bklog | xargs -n 1 ./bkcli check
```

示例：

![](../images/paas_status.png)

## 三、访问蓝鲸

### 3.1 配置本地 hosts

> 下面介绍的操作均可能覆盖现有 hosts ，进行操作前请先确认是否需要备份。

1. Windows 配置
用文本编辑器（如`Notepad++`）打开文件：
`C:\Windows\System32\drivers\etc\hosts`
将以下内容内容复制到上述文件内并保存，以下 IP 须更换为本机浏览器可以访问的 IP。
```bash
10.0.0.2 paas.bktencent.com cmdb.bktencent.com job.bktencent.com jobapi.bktencent.com
10.0.0.3 nodeman.bktencent.com
```
> 注意：如果遇到无法保存，请右键文件 hosts 并找到“属性” -> “安全”，然后选择你登陆的用户名，最后点击编辑，勾选“写入”即可。
2. Linux / Mac OS 配置
将以下内容全部内容复制到 `/etc/hosts`中并保存，以下 IP 须更换为本机浏览器可以访问的 IP。
```bash
10.0.0.2 paas.bktencent.com cmdb.bktencent.com job.bktencent.com jobapi.bktencent.com
10.0.0.3 nodeman.bktencent.com
```

### 3.2 获取管理员账户名密码

在任意一台机器上，执行以下命令，获取管理员账号和密码

```bash
grep -E "BK_PAAS_ADMIN_USERNAME|BK_PAAS_ADMIN_PASSWORD" /data/install/bin/04-final/usermgr.env
```

### 3.3 访问蓝鲸开始使用

> 默认蓝鲸工作台入口：[http://paas.bktencent.com](http://paas.bktencent.com)

![](../images/login.png)