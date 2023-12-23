### 安装helm
加速地址
> https://mirrors.huaweicloud.com/helm/

解压
> tar -zxvf helm-v3.6.3-linux-amd64.tar.gz

移动位置
> sudo mv linux-amd64/helm /usr/local/bin/

查看版本
> helm version

添加仓库
> helm repo add ingress-nginx https://kubernetes.github.io/ingress-nginx

查看仓库
> helm repo list

搜索仓库
> helm search repo ingress-nginx

拉取
> helm pull ingress-nginx/ingress-nginx

解压 ingress tar
> tar -xf ingress-nginx-4.8.0.tgz

进入目录并修改values.yaml
修改 ingress-controller 内容如下：并注释掉digest*
> registry: registry.cn-hangzhou.aliyuncs.com  
> image: google_containers/nginx-ingress-controller

修改 kube-webhook-certgen，并注释掉digest* 
> registry: registry.cn-hangzhou.aliyuncs.com  
> image: google_containers/kube-webhook-certgen  
> tag: 1.5.2


修改 kind 类型为 DaemonSet

nodeSelector 添加标签: ingress: "true"，用于部署 ingress-controller 到指定节点

修改 dnsPolicy 的值为 ClusterFirstWithHostNet

修改 hostNetwork 的值为 true

修改type
> type: loadBalancer 改为 type: ClusterIP

搜索admission修改enabled
> enabled: true 改为 false

安装ingress-nginx
> helm install ingres-nginx ./ingress-nginx -n ingress-nginx

### helm 安装provisioner
> helm repo add nfs-subdir-external-provisioner https://kubernetes-sigs.github.io/nfs-subdir-external-provisioner/

> helm install nfs-provisioner nfs-subdir-external-provisioner/nfs-subdir-external-provisioner \
--set image.repository=dyrnq/nfs-subdir-external-provisioner \
--set nfs.server=192.168.198.161 \
--set nfs.path=/data/k8s-nfs/nfs-provisioner \
--set storageClass.name=nfs-sc \
--set storageClass.provisionerName=k8s-cluster.io/nfs-subdir-external-provisioner