# centos7安装
要求：
centos 7

官网下载
https://gitlab.cn/install/
> curl -fsSL https://packages.gitlab.cn/repository/raw/scripts/setup.sh | /bin/bash

下载并暴露域名 http://gitlab.example.com
> sudo EXTERNAL_URL="http://gitlab.example.com" yum install -y gitlab-jh

修改密码已存在用户密码
> gitlab-rake "gitlab:password:reset"