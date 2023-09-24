### 重启
> reboot 
> 或
> shutdown -r now

### 查看服务状态
> systemctl status 应用名

### 查看ip地址
> ip addr

### 重启网络
> systemctl restart network

### 查看当前系统时间
> date


### 删除文件
> rm [选项] 文件名

以下是一些常用的选项：

-i：在删除文件之前提示确认。  
-r 或 --recursive：递归地删除目录及其内容。  
-f 或 --force：强制删除文件，不会提示确认。  

### 查看文件大小
> ls -lh 文件名

### 文件重命名
> mv 老文件全名 新文件全名

### 主机文件同步
> scp 文件绝对路径 主机名\ip地址

### 通过端口查看进程（需要安装lsof）
> lsof -i :端口号

域名解析(安装dig)
> yum -y install bind-utils  
> dig

### 命令耗时
> time 命令  
> 例如： time kubectl delete po nginx-demo