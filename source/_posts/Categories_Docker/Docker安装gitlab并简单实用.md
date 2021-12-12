---
title: Docker安装gitlab并简单实用
date: 2020-07-03 15:19:41
tags: 
    - gitlab
    - 运维
categories: 
    - Docker
cover: /img/cover7.png
top_img: /img/cover7.png
mathjax: false
description: 如题
---
## 前言

* 系统 centos7.*
* 通过docker 安装gitlab 并 持久化

## 下载镜像

&ensp;&ensp;&ensp;&ensp;执行下面的命令，从 docker 的镜像仓库中下载 gitlab 社区版的镜像

```
docker pull gitlab/gitlab-ce:latest
```

## 编写docker-compose文件

```
version: '2'
services:
    gitlab:
      image: 'gitlab/gitlab-ce:latest'
      restart: unless-stopped
      hostname: '192.168.124.72'
      environment:
        TZ: 'Asia/Shanghai'
        GITLAB_OMNIBUS_CONFIG: |
          external_url 'http://192.168.124.72'
          gitlab_rails['time_zone'] = 'Asia/Shanghai'
          # 需要配置到 gitlab.rb 中的配置可以在这里配置，每个配置一行，注意缩进。
          # 比如下面的电子邮件的配置：
          # gitlab_rails['smtp_enable'] = true
          # gitlab_rails['smtp_address'] = "smtp.exmail.qq.com"
          # gitlab_rails['smtp_port'] = 465
          # gitlab_rails['smtp_user_name'] = "xxxx@xx.com"
          # gitlab_rails['smtp_password'] = "password"
          # gitlab_rails['smtp_authentication'] = "login"
          # gitlab_rails['smtp_enable_starttls_auto'] = true
          # gitlab_rails['smtp_tls'] = true
          # gitlab_rails['gitlab_email_from'] = 'xxxx@xx.com'
      ports:
        - '80:80'
        - '443:443'
        - '222:22'
      volumes:
        - ./gitlab/config:/etc/gitlab
        - ./gitlab/data:/var/opt/gitlab
        - ./gitlab/logs:/var/log/gitlab
volumes:
    config:
    data:
    logs:
```

&ensp;&ensp;&ensp;&ensp;启动

```
docker-compose up -d
```



&ensp;&ensp;&ensp;&ensp;修改配置文件

```
# 配置http协议所使用的访问地址
external_url 'http://192.168.124.72'

# 配置ssh协议所使用的访问地址和端口
gitlab_rails['gitlab_ssh_host'] = '192.168.124.72'
gitlab_rails['gitlab_shell_ssh_port'] = 222
```

&ensp;&ensp;&ensp;&ensp;**注意**，每次修改gitlab.rb配置文件之后，或者在容器里执行gitlab-ctl reconfigure命令，或者重启容器以让新配置生效。