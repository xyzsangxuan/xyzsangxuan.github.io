---
title: 在CeontOS中安装Docker
date: 2020-07-03 15:14:24
tags: 
    - 运维
categories: 
    - Docker
cover: /img/cover9.png
top_img: /img/cover9.png
mathjax: false
description: 如题
---
&ensp;&ensp;&ensp;&ensp;前提条件：首先我们安装的不是企业版。企业版提供了有一些收费的高级特性，社区版没有这些特性，但是不影响我们目前的使用。

## centos7修改yum源为阿里源

### 安装base reop源

```
# cd /etc/yum.repos.d/
```

&ensp;&ensp;&ensp;&ensp;接着备份旧的配置文件

```
# sudo mv CentOS-Base.repo CentOS-Base.repo.bak
```

&ensp;&ensp;&ensp;&ensp;下载阿里源的文件

```
# sudo wget -O CentOS-Base.repo http://mirrors.aliyun.com/repo/Centos-7.repo
```



### 安装epel repo源

&ensp;&ensp;&ensp;&ensp;epel（RHEL7）

```
# wget -O /etc/yum.repos.d/epel.repo http://mirrors.aliyun.com/repo/epel-7.repo
```



&ensp;&ensp;&ensp;&ensp;epel（RHEL6）

```
# wget -O /etc/yum.repos.d/epel.repo http://mirrors.aliyun.com/repo/epel-6.repo
```

&ensp;&ensp;&ensp;&ensp;epel（RHEL5）

```
# wget -O /etc/yum.repos.d/epel.repo http://mirrors.aliyun.com/repo/epel-5.repo
```

### 清理缓存

```
# yum clean all
```

### 重新生成缓存

```
# yum makecache
```

## CentOS7安装dockerCE

### 卸载旧版本

&ensp;&ensp;&ensp;&ensp;如果是新机器可以忽略这一步，因为centos还没有自带docker服务。

```
# yum remove docker docker-client docker-client-latest docker-common docker-latest docker-latest-logrotate docker-logrotatedocker-selinux docker-engine-selinux docker-engine
```

### 安装dockerCE

* 安装依赖包

```
# yum install -y yum-utils device-mapper-persistent-data lvm2
```

* 添加Docker软件包源

```
# yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
```

&ensp;&ensp;&ensp;&ensp;但是鉴于国内网络问题，建议使用国内阿里的源

```
# yum-config-manager --add-repo https://mirrors.aliyun.com/docker-ce/linux/centos/docker-ce.repo
```

### 打开测试版本list

&ensp;&ensp;&ensp;&ensp;如果你希望安装测试版本和edge版本，但默认情况下处于禁用状态。可以将它们与稳定存储库一起启用

```
# yum-config-manager --enable docker-ce-edge

# yum-config-manager --enable docker-ce-test
```

### 安装（安装最新版本）

```
# yum install docker-ce
```

### 安装（制定版本）

```
# yum list docker-ce --showduplicates|sort –r

# yum install docker-ce-17.06.0.ce
```

### 启动

启动        systemctl start docker

守护进程重启   sudo systemctl daemon-reload

重启docker服务   systemctl restart  docker

重启docker服务  sudo service docker restart

关闭docker   service docker stop

关闭docker  systemctl stop docker





### 更换docker源

```
sudo mkdir -p /etc/docker
sudo tee /etc/docker/daemon.json <<-'EOF'
{
  "registry-mirrors": ["https://172ih0ly.mirror.aliyuncs.com"]
}
EOF
sudo systemctl daemon-reload
sudo systemctl restart docker
```

