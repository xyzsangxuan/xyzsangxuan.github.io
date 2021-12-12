---
title: Docker安装MySQL5.6
date: 2020-07-03 15:22:06
tags: 
    - Linux
    - 运维
categories: 
    - Docker
cover: /img/cover6.png
top_img: /img/cover6.png
mathjax: false
description: 如题
---
1,docker hub上查找mysql镜像

```
docker search mysql
```



2,在dockerhub上（阿里云加速器）拉取MySQL镜像到本地标签为5.6

```
docker pull mysql:5.6
```

3,使用mysql5.6创建容器（也叫运行镜像）

```
docker run -p 12345:3306 --name mysql -v /zycmysql/conf:/etc/mysql/conf.d -v /zymysql/mysql/logs -v /zycmsql/mysql/data:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=123456 -d mysql:5.6
```

基本启动（缺点：容器关闭在启动我们的数据就没有了）

```
# docker run --name mysql -p 3306:3306 -e MYSQL_ROOT_PASSWORD=123456 -d mysql:5.6

```

高级启动（容器关闭在启动我么你的数据不会消失）

```
# docker run --name mysql -p 3306:3306 -v /mysql/data:/var/lib/mysql -e MYSQL_ROOT_PASSWORD=123456 -d mysql:5.6

```



4,交互运行，进入mysql

```
#  docker exec -it adca2afca208 /bin/bash
mysql -uroot -p


show databases;
```

5,查看服务器地址

```
ifconfig
```

