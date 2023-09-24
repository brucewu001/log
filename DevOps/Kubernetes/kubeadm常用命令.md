# kubeadm

初始化
> kubeadm init

更多参数
> --kubenetes-version=指定版本  
> --apiserver=apiserverIP地址  
> ----image-repository registry.aliyuncs.com/google_containers 指定阿里云镜像

查看节点加入集群所需的节点
> kubeadm token list

重新创建token
> kubeadm token create

查看节点加入集群所需sha256
> openssl x509 -pubkey -in /etc/kubernetes/pki/ca.crt | openssl rsa -pubin -outform der 2>/dev/null | openssl dgst -sha256 -hex | sed 's/^.* //'

最后加入命令如下
> kubeadm join 192.168.198.160:6443 --token token值 --discovery-token-ca-cert-hash sha256:sha256的值