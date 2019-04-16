# centos 7 安装 MySQL 8.0

## 先检查系统中是否已经安装mysql
```text
rpm -qa|grep -i mysql
```
## 如果需要卸载，则使用如下命令
```text
sudo yum remove (包名)
```
## 使用如下命令安装MySQL
```text
wget http://repo.mysql.com/mysql80-community-release-el7-2.noarch.rpm  # 下载mysql安装包
sudo rpm -ivh mysql80-community-release-el7-2.noarch.rpm
sudo yum install -y mysql mysql-server
```

## 启动mysql服务
```text
service mysqld restart
```

## 修改默认root 密码

### 1、更改加密方式
```text
sudo vim /etc/my.cnf

# 将此行的注释打开
default-authentication-plugin=mysql_native_password
```
### 2、找到默认密码
```text
grep 'temporary password' /var/log/mysqld.log
会出现这样的结果
A temporary password is generated for root@localhost: 1>Sw7?Ag9vdp
其中 1>Sw7?Ag9vdp 就是默认密码，记录下来
```
### 3、使用默认密码登录
```text
mysql -uroot -p(默认密码)
```
### 4、设置密码强度级别，三个数字分别对应低，中，高三个级别，我这里为了方便记忆，设置成"低"也就是0
```text
set global validate_password.policy=0;
```
### 5、这个是设置密码长度的，不能低于4位，根据需要自己设置长度
```text
set global validate_password.length=4;
```
### 6、给root用户本地登录设置密码,"password"是我设置的密码
```text
ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'password';
```
### 7、退出当前账户，使用修改后的密码登录即可

