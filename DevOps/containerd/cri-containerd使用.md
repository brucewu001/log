# 嗷嗷嗷

### 开局就是版本查看
> containerd --version

ctr：containerd自带的命令行工具，可以用来查看、操作、控制和管理容器。

crictl：Kubernetes的CRI客户端。由于containerd实现了对CRI（Container Runtime Interface 容器运行时接口）标准的支持，因此可以使用该工具对其进行操作。

查看所有容器
> crictl ps -a

查看容器日志
> crictl logs 容器id

修改tag (现在crictl还不支持修改，但是containerd自己的命令行工具ctr支持，但是k8s的镜像都是在命名空间为k8s.io里的所以需要拉取)
> ctr image tag xxx xxx