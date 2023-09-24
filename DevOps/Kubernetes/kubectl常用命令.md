# kubectl
### 偶直接就是上地址 https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands

### 在任意节点使用kubectl操作

master节点下admin.conf记录了最高权限的用户账号，复制到其他节点后即可访问所以资源

1. 复制master下的/etc/kubernetes/admin.conf 到节点机下
> scp /etc/kubernetes/admin.conf 节点IP:/etc/kubernetes/

2配置环境变量
> echo "export KUBECONFIG=/etc/kubernetes/admin.conf" >> ~/.bash_profile  
> source ~/.bash_profile

### 查看命名空间
> kubectl get ns

### 查看默认命名空间pods
> kubectl get pods 

### 查看kube-system命名空间pods
> kubectl get pods -n kube-system

### 查看配置节点
> kubectl get nodes

### 查看pod详情
> kubectl describe pods pods全名 -n 命名空间

### 查看deploy
> kubectl get deploy

### 查看deploy输出为yaml文件
> kubectl get deploy deploy全名 -o yaml

### 修改pod副本数量

### 修改pod副本数量(扩容/缩容)
> kubectl scale deploy --replicas=3 deploy全名

### 删除delopy
> kubectl delete deploy deploy全名

### 删除servers
> kubectl delete svc svc全名

### yaml资源pod标签详解 
> https://kubernetes.io/zh-cn/docs/reference/kubernetes-api/workload-resources/pod-v1/#PodStatus

### 编辑coredns的配置文件（用编辑，实际上只是想复制里面的配置信息）
> kubectl edit deploy -n kube-system coredns

### 在pod里的容器里执行命令 cat /inited
> kubectl exec -it nginx-demo -c nginx -- cat /inited

### 实时查看pod变化
> kubectl get po -w

### 查看pod的label
> kubectl get po pod名 --show-labels -n 命名空间

### 修改pod的label（临时修改，一刷新就没）
> kubectl label po pod名 原有label键=修改值 --overwrite  -n 命名空间

### 新增pod的label（临时修改，一刷新就没）
> kubectl label po pod名 新label键=值

### 搜索pod by labels
并集
> kubectl get po -l 键=值,键=值,键=值 

一个键多个值的匹配  
> kubectl get po -l 键=值,键=值,键 in (值, 值, 值) 

### 获取ReplicaSet(RS)
> kubectl get rs

### 命令创建deployment
> kubectl create deployment nginx-deploy --image=nginx:1.7.9

### 查看deploy滚动更新状态
> kubectl rollout status deploy全名

### 修改deploy镜像
> kubectl set image deployment/资源名 nginx=nginx:1.7.9

### 查看deploy修改历史版本（可选：查看版本详情）
> kubectl rollout history deployment/资源名 [--revision=版本号]

### 暂停/恢复 

暂停
> kubectl rollout pause deployment/资源名 

恢复
> kubectl rollout resume deployment/资源名 

替换
> kubectl replace -f xxx.yaml

### 查看所有资源
> kubectl get all

### 启动busybox并进入sh
> kubectl -it run --image busybox busybox /bin/sh

### 进入busybox sh
> kubectl -it exec  busybox /bin/sh

### 使用patch修改镜像
> （无法使用，scale命令替换）kubectl patch sts web --type='json' -p='[{"op": "replace","path": "/spec/containers/0/image","value": "nginx:1.9.1"}]'

### 删除statefulset默认级联删除，即sts和pod一起删除，若想非级联删除添加选项 --cascade=false
> kubectl delete web sts --cascade=orphan