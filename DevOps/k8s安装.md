# 准备虚拟机 - 准备3台 centos7u9

工具：vmware 17 player

iso：contos7u9(清华源下载)

### 第一步 设置主机名

主机名字分别为 k8s-master k8s-node1 k8s-node2

> 例如： hostnamectl set-hostname k8s-master


### 设置ip地址
编辑/etc/sysconfig/network-scripts/ifcfg-ens33文件

偶选择跳过

### 设置ip地址对应主机名
编辑/etc/hosts文件

> 192.168.198.129 k8s-master
> 192.168.198.130 k8s-node0
> 192.168.198.131 k8s-node1







