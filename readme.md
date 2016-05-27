# showdoc_docker

## showdoc介绍

> 写api文档不错的工具

[作者的教程](http://blog.star7th.com/2016/05/2007.html)
[demo](http://doc.star7th.com/index.php?s=/2&page_id=9)

## docker化
由于本人不是php开发 也不想装php环境，所以就用docker搭建了运行showdoc的环境。


首先去[https://dashboard.daocloud.io/packages/8ae9639b-9fce-491a-890f-ffac6404dc70](https://dashboard.daocloud.io/packages/8ae9639b-9fce-491a-890f-ffac6404dc70)
这个地址查看php的docker的用法，然后做自己的Dockfile文件。

```
FROM php:5.6-apache
COPY showdoc/ /var/www/html/

RUN apt-get update && apt-get install -y \
        libfreetype6-dev \
        libjpeg62-turbo-dev \
        libmcrypt-dev \
        libpng12-dev \
    && docker-php-ext-install -j$(nproc) gd

RUN chmod 777 Application/Runtime \
  && chmod 777 Public/Uploads \
  && chmod 777 Sqlite \
  && chmod 777 Sqlite/showdoc.db.php
CMD ["apache2-foreground"]
```

## 创建和运行镜像
创建镜像  
```
docker build -t showdoc .
```
然后运行
```
docker run -d --name showdoc -p 83:80 showdoc
```
然后浏览器访问(这里是mac版本的演示，所以地址是192.168.99.100)
```
http://192.168.99.100:83
```
