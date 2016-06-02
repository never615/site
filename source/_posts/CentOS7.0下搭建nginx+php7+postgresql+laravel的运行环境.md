---
title: CentOS7.0下搭建nginx+php7+postgresql+laravel的运行环境
date: 2016-04-20
update:
tags: 
- web环境搭建
- centos
category: web
---

只讲述如何配置一个laravel应用可以运行的基本环境，其他的如权限管理、禁止root远程登录、ssh密码登录、防火墙等不涉及。
这些东西配置下来给我最大的感悟就是,首先去查官网资料...
<!-- more -->

安装步骤大体分为以下几步：

1. 基本环境配置
2. 安装php-fpm（同时安装了php） 
3. 安装composer
4. 安装postgresql并配置
5. 安装nginx
6. 创建一个laravel应用并配置nginx

## CentOs基本环境配置
在CentOS上管理软件可以使用yum作为包管理工具，可以用命令查询、删除、下载、安装、删除系统上的软件。

yum的使用：[yum参考手册](https://access.redhat.com/sites/default/files/attachments/rh_yum_cheatsheet_1214_jcs_print-1.pdf)


系统官方的资源库提供的软件不能满足我们的需求，比如搜索php70u，会提示NO Matches found，所以我们要添加额外的资源库。

在这里可以找到ius的包，[https://dl.iuscommunity.org/pub/ius/stable/CentOS/7/x86_64/repoview/ius-release.html](https://dl.iuscommunity.org/pub/ius/stable/CentOS/7/x86_64/repoview/ius-release.html)。

复制包地址，使用wget下载，会下载到当前目录。
	
	wget https://dl.iuscommunity.org/pub/ius/stable/CentOS/7/x86_64/ius-release-1.0-14.ius.centos7.noarch.rpm
	
	
然后使用命令安装：

	rpm -ivh ius-release-1.0-10.ius.el6.noarch.rpm epel-release-6-5.noarch.rpm

如果安装失败，提示你安装epel,就用yum search epel，然后安装。
## 安装php-fpm和php,安装php常用扩展
搜索php-fpm：

	yum search php70u-fpm
安装，因为yum会自动解决软件之间的依赖，所以会自动安装php
	
	yum install php70u-fpm
查看php-fpm的状态：

	systemctl status php-fpm
启动php——fpm:

	systemctl start php-fpm
设置开机启动：

	systemctl enable php-fpm

安装php常用的扩展：
	
	yum install php70u-gd php70u-mysqlnd php70u-pdo php70u-mcrypt php70u-mbstring php70u-json php70u-cli -y
安装完成需要重新加载php-fpm:

	systemctl reload php-fpm
	
## 安装composer
composer是php中管理依赖的工具[官网](https://getcomposer.org/doc/00-intro.md)

	php -r "copy('https://getcomposer.org/installer', 'composer-setup.php');"
	php -r "if (hash_file('SHA384', 'composer-setup.php') === '92102166af5abdb03f49ce52a40591073a7b859a86e8ff13338cf7db58a19f7844fbc0bb79b2773bf30791e935dbd938') { echo 'Installer verified'; } else { echo 'Installer corrupt'; unlink('composer-setup.php'); } echo PHP_EOL;"
	php composer-setup.php
	php -r "unlink('composer-setup.php');"
这几条命令的意思就是：下载；校验；安装；删除安装包；

在国内使用composer如果没有翻墙的话，可以使用镜像。[镜像地址](http://pkg.phpcomposer.com/)

## 安装postgresql并配置
直接使用yum安装地方postgres不是最新的，一些新特性无法使用，建议按[官网](http://www.postgresql.org/download/linux/redhat/)教程安装最新版。

	yum install https://download.postgresql.org/pub/repos/yum/9.5/redhat/rhel-7-x86_64/pgdg-centos95-9.5-2.noarch.rpm
完成之后：

	yum install postgresql94-server postgresql94-contrib
	/usr/pgsql-9.4/bin/postgresql94-setup initdb
	systemctl enable postgresql-9.4.service
	systemctl start postgresql-9.4.service
	yum install php70u-pgsql
查看是否安装成功：

	rpm -aq|grep postgres
配置:
postgres安装完成之后会生成名为postgres的数据库、数据库用户和linux系统用户

* 切换到postgres用户：
	
		sudo su - postgres
* 使用psql命令登录PostgreSQL：

		psql
	
这时相当于系统用户postgres以同名数据库用户的身份，登录数据库，这是不用输入密码的。如果一切正常，系统提示符会变为"postgres=#"，表示这时已经进入了数据库控制台。以下的命令都在控制台内完成。

* 第一件事是使用\password命令，为postgres用户设置一个密码。

		\password postgres
* 创建数据库用户dbuser，并指定其为超级用户 

		sudo -u postgres createuser --superuser dbuser
* 登录数据库控制台，设置dbuser用户的密码，完成后退出控制台（postgres安装完成之后会生成名为postgres的数据库、数据库用户和linux系统用户）psql命令是登录PostgreSQL控制台

 		sudo -u postgres psql
		\password dbuser
		\q
* 创建数据库exampledb，并指定所有者为dbuser

 		sudo -u postgres createdb -O dbuser exampledb

我是使用Navicat Premium和Postico作为数据库管理软件的。Postico更轻，查看修改数据比较方便，Navicat功能比较强大。

### 数据库直接安装完成之后是不能远程访问的，如果需要远程访问的话，需要配置一下：
修改postgresql.conf和pg_hba.conf这两个文件。

可以使用locate命令定位这两个文件，updatedb命令可以更新locate文件，如果刚安装完没有找到这两个文件，可以调用这个命令刷新一下。

* postgresql.conf配置

		listen_addresses = '*'     //监听所有ip的连接，默认是本机  
		port = 5432             //这个不开也行，默认就是5432端口
* pg_hba.conf配置

		配置host    all         all         0.0.0.0/0             trust
* 如果配置防火墙，记得开放端口

修改完记得重启。


## 安装nginx并配置

[nginx官网安装教程](http://nginx.org/en/linux_packages.html)

想安装最新nginx，我们需要先添加nginx的库。

创建文件/etc/yum.repos.d/nginx.repo，并写入以下内容：

	[nginx]
	name=nginx repo
	baseurl=http://nginx.org/packages/mainline/centos/OSRELEASE/7/
	gpgcheck=0
	enabled=1	
	
或者使用rpm安装：

	rpm -Uvh http://nginx.org/packages/centos/7/noarch/RPMS/nginx-release-centos-7-0.el7.ngx.noarch.rpm

然后使用yum命令安装nginx即可。

## 创建一个laravel应用并配置nginx
[laravel官方文档](https://laravel.com/docs/5.2)

* 先通过composer下载laravel`composer global require "laravel/installer"`
* 创建一个laravel项目`composer create-project --prefer-dist laravel/laravel blog`
 

简单的nginx配置使其可以访问laravel应用：
配置文件在/etc/nginx/conf.d目录下。一个基本的配置如下：

``````
server {
   listen 81;
   server_name www.laravel.com;     
   root /data1/www/laravelapps/app/blog/public;
   index index.php index.html index.htm;

   location / {
        try_files $uri $uri/ /index.php?$query_string;
   }

   location ~ \.php$ {
    	fastcgi_pass   127.0.0.1:9000;
    	fastcgi_index  index.php;
      fastcgi_param  SCRIPT_FILENAME  $document_root		$fastcgi_script_name;
      include        fastcgi_params;
      fastcgi_param   SCRIPT_NAME  $fastcgi_script_name;     
   }
}

```````



