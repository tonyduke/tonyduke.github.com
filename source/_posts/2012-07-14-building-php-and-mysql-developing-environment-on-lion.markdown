---
layout: post
title: "在LION环境建立PHP和MySQL的开发环境"
date: 2012-07-14 17:36
comments: true
categories: 
---
## 打开系统默认的Apache

__方法1：__

打开System Prerences -> Sharing， 勾选Web Sharing即可
 
访问 [http://localhost/~anthony/](http://localhost/~anthony/ "个人网站")可以打开个人网站存放地址

该地址为 “/Users/anthony/Sites/”
 
访问 [http://localhost/](http://localhost/ "默认网站")可以打开默认的网站存放地址

该地址为 “/Library/WebServer/Documents”

__方法2：__

打开Terminal，输入命令

	apachectl start

## 启用root用户

使用root权限，默认的系统没有启用root帐号，选择System Preferences -> Users & Groups

![alt enable_root_user_step1.png](/images/img4blog/enable_root_user_step1.png "enable_root_user_step1.png")

图1－选择Open Directory Utility（图片在打开web sharing时才能查看）

![alt enable_root_user_step2.png](/images/img4blog/enable_root_user_step2.png "enable_root_user_step2.png")

图1－选择Edit，设定Root用户（图片在打开web sharing时才能查看）

## 打开apache的PHP支持

1. 打开apache配置文件

	* 进入apache目录
	
			cd /etc/apache2
	* 赋予配置文件可写权限
	
			chmod 644 httpd.conf
			vi httpd.conf

2. 打开其中的PHP设置，找到如下代码

		#LoadModule php5_module libexec/apache2/libphp5.so
	将其注释打开，保存。

3. 创建PHP的配置文件

		cp /etc/php.ini.default /etc/php.ini
	
	配置
	
		;通过下面两项来调整PHP提交文件的最大值，比如phpMyAdmin中导入数据的最大值
		upload_max_filesize = 2M
		post_max_size = 8M
		;比如通过display_errors来控制是否显示PHP程序的报错
		display_errors = Off

4. 设定时区，在php.ini中找到如下代码，设定时区

		date.timezone = Asia/Shanghai
	
5. 重启apache

		sudo apachectl restart
 
## 安装MySQL环境

1. 下载MySQL 5.1。选择合适的版本，比如这里选择的是mysql-5.5.21-osx10.6-x86_64.dmg。

2. 运行dmg，会发现里面有4个文件。首先点击安装mysql-5.5.21-osx10.6-x86_64.pkg，这是MySQL的主安装包。一般情况下，安装文件会自动把MySQL安装到/usr/local下的同名文件夹下。比如点击运行“mysql-5.5.21-osx10.6-x86_64.dmg”会把MySQ安装到“/usr/local/mysql-5.5.21-osx10.6-x86_64”中。一路默认安装完毕即可。

3. 点击安装第2个文件MySQLStartupItem.pkg，这样MySQL就会自动在开机时自动启动了。

4. 点击安装第3个文件MySQL.prefPane，这样就会在“系统设置偏好”中看到名为“MySQL”的ICON，通过它就可以设置MySQL开始还是停止，以及是否开机时自动运行。到这里MySQL就基本安装完毕了。

5. 设置my.conf

		sudo cp /usr/local/mysql/support-files/my-small.cnf /etc/my.cnf
