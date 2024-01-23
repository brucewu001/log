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

### 请求死循环
> while true; do curl <ip>; done

### 添加执行权限
> sudo chmod +x /etc/sysconfig/startup.sh

### base64编码/解码
1. 编码
> echo 'supersecret' | base64

2. 解码
> echo 'c3VwZXJzZWNyZXQK' | base64 --decode

### 简单输出到文件
1. 覆盖写人文件
> echo 'dsgzsdga' > index.html

2. 追加写人文件
> echo 'sadgaeasdg' >> index.html

### 查看硬盘方式
> df -h   
> fdisk -l：这个命令会显示文件系统的类型，但不直接以m来显示大小。  
> sfdisk -uM -l：这个命令类似于fdisk，但能输出更详细的信息，且能够以m来显示大小。  
> cfdisk：这是一个交互式查看分区的命令，并且可以创建和编辑分区。  
> parted：这个命令可以查看并编辑分区。  
> pydf：这个命令是df的升级版，更易读的输出硬盘分区。  
> lsblk：这个命令可以显示所有的存储块，包括所有的磁盘分区，包括分区大小和分区点。  


