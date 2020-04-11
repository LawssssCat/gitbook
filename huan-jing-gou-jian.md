# linux 环境构建

## VirtualBox

VM环境

## Vagrant

成品镜像

```bash
$ vagrant box add centos-7 ./centos-7.0-x86_64.box
$ vagrant init centos-7
$ vagrant up
$ vagrant ssh
```

管理员

```bash
$ su root
# 密码 vagrant
$ whoami
```

> 入门案例：[https://www.cnblogs.com/lawsssscat/p/12676477.html](https://www.cnblogs.com/lawsssscat/p/12676477.html)

## docker

虚拟容器

安装：[https://docs.docker.com/engine/install/centos/](https://docs.docker.com/engine/install/centos/)

```bash
$ sudo yum remove docker \
                  docker-client \
                  docker-client-latest \
                  docker-common \
                  docker-latest \
                  docker-latest-logrotate \
                  docker-logrotate \
                  docker-engine
$ sudo yum install -y yum-utils
$ sudo yum-config-manager \
    --add-repo \
    https://download.docker.com/linux/centos/docker-ce.repo
$ sudo yum install docker-ce docker-ce-cli containerd.io
```

开启

```bash
$ sudo systemctl start docker
$ sudo systemctl enable docker
```

阿里云容器镜像服务：[https://cr.console.aliyun.com/cn-hangzhou/instances/mirrors](https://cr.console.aliyun.com/cn-hangzhou/instances/mirrors)

```bash
$ sudo mkdir -p /etc/docker
$ sudo tee /etc/docker/daemon.json <<-'EOF'
{
  "registry-mirrors": ["https://eslh5xx9.mirror.aliyuncs.com"]
}
EOF
$ sudo systemctl daemon-reload
$ sudo systemctl restart docker
```

## MySQL

```bash
$ sudo docker pull mysql:5.7
$ sudo docker images 

$ sudo docker run --name mysql -p 3306:3306 \
-v /dev/mydata/mysql/log:/var/log/mysql \
-v /dev/mydata/mysql/data:/var/lib/mysql \
-v /dev/mydata/mysql/conf:/etc/mysql \
-e MYSQL_ROOT_PASSWORD=root \
-d mysql:5.7
# 日志映射到本地 -v /dev/mydata/mysql/log:/var/log/mysql
# 容器中的Store Data映射到本地 -v 
# 使用自定义MySQL配置文件 -v /dev/mydata/mysql/conf:/etc/mysql
# （必须）指定数据库登录密码 MYSQL_ROOT_PASSWORD=root
```

{% hint style="info" %}
* `/dev/mydata/mysql/log:/var/log/mysql` 日志映射到本地
* `/dev/mydata/mysql/data:/var/lib/mysql` 数据库数据映射到本地

/dev/mydata/mysql/data:/var/lib/mysql/dev/mydata/mysql/data:/var/lib/mysql
{% endhint %}

> Docker官网关于MySQL:5.7：[https://hub.docker.com/\_/mysql](https://hub.docker.com/_/mysql)
>
> Docker官网关于MySQL:5.7的Dockerfile：[https://github.com/docker-library/mysql/blob/d284e15821ac64b6eda1b146775bf4b6f4844077/5.7/Dockerfile](https://github.com/docker-library/mysql/blob/d284e15821ac64b6eda1b146775bf4b6f4844077/5.7/Dockerfile)





