---
title: 安装mysql
date: 2019-09-11 20:09:18
tags: [mysql]
---

# Mysql Installation

1. 下载zip，解压到某文件夹，用管理员权限进入命令行，进入mySql解压路径bin文件夹，如：D:\Program Files\mysql-8.0.13-winx64\bin

2. 输入`mysqld -install`安装（一般需要创建一个data文件，可以提前创建，然后在ini文件中写入）也可以在提示错误的时候手动创建）

   <!-- more -->

3. `net start mysql`启动mysql服务器

4. `mysql -h localhost -u root -p`或者`mysql -u root -p`登陆，登陆成功后，要更改密码才能进行其他操作，参考[登陆](https://dev.mysql.com/doc/refman/8.0/en/connecting-disconnecting.html)

   > -h: 指定客户端所要登录的Mysql，登陆本机(localhost or 127.0.0.1)该参数可忽略
   >
   > -u: 登陆的用户名
   >
   > -p: 告诉服务器将会使用一个密码来登陆，如果密码为空可忽略
   >
   > 密码: Speical4mysql

5. `ALTER USER ‘root'@'localhost' IDENTIFIED BY 'NewPassword';`

6. 创建用户与8.0前版本也有所不同，

   `create user 'guest'@'localhost' identified by 'guest123'`

7. 同样的，授权命令也发生了变化

   `grant all on *.* to 'guest'@'localhost' with grant option;`

8. 就算是root用户，默认也是没有grant权限的，要用`grant grant option on *.* to 'root'@'localhost';`来给root用户grant权限，之后即可正常操作。有关权限的操作，可以参考[官方文档](https://dev.mysql.com/doc/refman/8.0/en/privileges-provided.html)

9. 彻底关闭mysql，`mysqladmin -u root -p shutdown`

10. 关闭后不能直连，要打开`net start mysql`,打开后就可以重复上面的登陆步骤来操作。

11. 在系统环境变量的Path（下方那个）中添加`D:\Program Files\mysql-8.0.13-winx64\bin`路径后，不用每次都cd到对应的bin文件夹，直接用`mysql -u root -p`即可。