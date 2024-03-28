### issue 1: ingress配置了路由但没转发
##### 思路: 1. 文心一言 2. 百度  
##### 解决: https://blog.csdn.net/Hello_worId/article/details/123602379
创建ingress 添加 IngressClass属性
查看 ingressClass
> kubectl get ingressClass  

在ingress配置文件添加如下：
> spec.ingressClassName: nginx

### issue 2: xshell 按退格键出现^H
解决方案：https://blog.csdn.net/qq_33966519/article/details/108103722?spm=1001.2101.3001.6650.1&utm_medium=distribute.pc_relevant.none-task-blog-2%7Edefault%7ECTRLIST%7ERate-1-108103722-blog-52454939.235%5Ev38%5Epc_relevant_sort_base1&depth_1-utm_source=distribute.pc_relevant.none-task-blog-2%7Edefault%7ECTRLIST%7ERate-1-108103722-blog-52454939.235%5Ev38%5Epc_relevant_sort_base1&utm_relevant_index=2


### issue 3: JAVA21 record 类上使用 spring 的 @Transactional 无法被 cglib 代理
解决方案： 当场 我就，嘿嘿，把 record 换成 class 并且不在 spring 项目下不留 issue 让他们自己找bug，嘿嘿