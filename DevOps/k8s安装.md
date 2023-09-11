# 安装k8s 1.28.1

# 准备虚拟机 - 准备3台 centos7u9

工具：vmware 17 player(免费版)

iso：contos7u9(清华源下载)

### 设置主机名

主机名字分别为 k8s-master k8s-node1 k8s-node2

> 例如： hostnamectl set-hostname k8s-master


### 设置ip地址
编辑/etc/sysconfig/network-scripts/ifcfg-ens33文件

追加以下 

master 对应 192.168.198.160

node1 对应 192.168.198.161

node2 对应 192.168.198.162


> IPADDR="192.168.198.160"
> 
> PREFIX="24"
> 
> GATEWAY="192.168.198.2"
> 
> DNS1="119.29.29.29"

### 设置ip地址对应主机名
编辑/etc/hosts文件

> 192.168.198.160 k8s-master
> 
> 192.168.198.161 k8s-node1
> 
> 192.168.198.162 k8s-node2

### 关闭防火墙

查看防火墙状态
> firewall-cmd --state

关闭防火墙
> systemctl stop firewalld

设置关闭防火墙开机自启动
> systemctl disable firewalld

以上两条功能合并
> systemctl disable --now firewalld

### 关闭selinux
查看状态
> sestatus

设置selinux配置文件
> sed -ri 's/SELINUX=enforcing/SELINUX=disabled/' /etc/selinux/config

接重启虚拟机
> reboot

### 时间同步

查看定时任务

> crontab -l

编辑定时任务
> crontab -e

追加 每小时同步一次的定时任务
> 0 */1 * * * ntpdate time1.aliyun.com

### 升级内核
通过elrepo升级内核

导入elrepo的GPG key
> sudo rpm --import https://www.elrepo.org/RPM-GPG-KEY-elrepo.org

安装elrepo仓库
> sudo yum install -y https://www.elrepo.org/elrepo-release-7.0-4.el7.elrepo.noarch.rpm

安装内核 ml为长期稳定版 lt为长期维护版
> sudo yum --enablerepo=elrepo-kernel install -y kernel-lt.x86_64

设置grub2默认引导为0
> grub2-set-default 0

重新生成grub2引导文件
> sudo grub2-mkconfig -o /boot/grub2/grub.cfg

接重启
> reboot

### 配置内核转发及网桥过滤

添加配置
> cat>/etc/sysctl.d/k8s.conf<<EOF  
net.bridge.bridge-nf-call-ip6tables = 1  
net.bridge.bridge-nf-call-iptables = 1  
net.ipv4.ip_forward=1  
vm.swappiness = 0  
EOF

加载br_netfilter  
> modprobe br_netfilter

配置生效
> sudo sysctl -p

添加自启动脚本
> vi /etc/sysconfig/modules/br_netfilter.modules  

脚本内容
> #!/bin/bash  
> modprobe br_netfilter

添加脚本权限
> chmod 755 /etc/sysconfig/modules/br_netfilter.modules 

### 安装ipvs

> yum install ipset ipvsadm

添加配置文件
cat > /etc/sysconfig/modules/ipvs.modules <<EOF  
#!/bin/bash  
modprobe -- ip_vs
modprobe -- ip_vs_rr  
modprobe -- ip_vs_wrr  
modprobe -- ip_vs_sh  
modprobe -- nf_conntrack  
EOF

授权，运行，检查是否加载
> chmod 755 /etc/sysconfig/modules/ipvs.modules && bash /etc/sysconfig/modules/ipvs.modules && lsmod | grep -e ip_vs -e nf_conntrack

### 关闭swap分区

查看swap分区
> free -m

临时关闭swap分区
> swapoff -a

永久关闭swap分区
> vi /etc/fstab

注释掉 swap 配置
> #/dev/mapper/centos-swap swap                    swap    defaults        0 0

# 安装containerd 

从github上复制containerd下载链接 https://github.com/containerd/containerd/releases/tag/v1.7.5

安装wget
> yum install wget

下载tar.gz()
> wget https://github.com/containerd/containerd/releases/download/v1.7.5/cri-containerd-1.7.5-linux-amd64.tar.gz

注：巨慢无比国内，试了很多种方法，只有配置hosts文件稍微有点用
用windows CMD 命令 nslookup 查看
github.com github.global.ssl.fastly.net assets-cdn.github.com  
的ip地址，并添加到centos 的hosts文件中 目录为 /etc/hosts

如果有台机器下好了，可以通过xftp软件直接复制到其他机器上


![img.png](../resource/img.png)

> 20.205.243.166 github.com  
108.160.162.102 github.global.ssl.fastly.net  
185.199.111.153 assets-cdn.github.com  


下载完解压tar
> tar xf cri-containerd-1.7.5-linux-amd64.tar.gz -C /

