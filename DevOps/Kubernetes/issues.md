### 一次重大事故
kubectl get po 报错  
apiserver 无法连接  
容器基本都是exited状态
> crictl ps -a 

查看apiserver容器日志
> crictl logs 容器id

无法连接2379端口 (etcd数据库)  
查看etcd容器日志  
无法加载snap file  
应该是数据异常  
应该是异常断电导致数据库异常  
删除对应etcd文件
> rm -rf /var/lib/etcd/member/wal/*  
> rm -rf /var/lib/etcd/member/snap/*  
> systemctl restart kubelet.service 

虽然启动了
但是一些必须的组件、配置没了
到最后还是要重新安装k8s
但是这次没有连整个linux都重新安装，只是k8s彻底删除后重新安装k8s，有进步了

#### 彻底删除k8s

> systemctl stop kubelet  
> modprobe -r ipip

> lsmod

> rm -rf ~/.kube/

> rm -rf /etc/kubernetes/

> rm -rf /etc/systemd/system/kubelet.service.d

> rm -rf /etc/systemd/system/kubelet.service

> rm -rf /usr/bin/kube*

> rm -rf /etc/cni

> rm -rf /opt/cni

> rm -rf /var/lib/etcd

> rm -rf /var/etcd

重新安装k8s看[1.28.1版本安装](DevOps/Kubernetes/1.28.1版本安装.md)  

马上学习etcd备份/恢复