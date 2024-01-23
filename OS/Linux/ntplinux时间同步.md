### ntp时间同步服务器

安装
> yum install -y ntp

配置/etc/ntp.conf(服务器节点)
```shell
### 在 server 部分添加如下内容，并注释掉 server 0 ~ n
server 210.72.145.44 prefer
server 127.127.1.0 iburst
```

配置/etc/ntp.conf(从节点)
```shell
### 在 server 部分添加如下内容，并注释掉 server 0 ~ n
server 服务器节点ip或域名
```

启动ntp
> systemctl start ntpd.service

开机自启动
> systemctl enable ntpd.service

查看ntp状态
> service ntpd status

查看ntp是否同步
> ntpstat