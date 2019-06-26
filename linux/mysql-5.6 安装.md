1.下载mysql的repo源

```
wget http://repo.mysql.com/mysql-community-release-el7-5.noarch.rpm
```

2.安装rpm包

```
sudo rpm -ivh mysql-community-release-el7-5.noarch.rpm
```

3.安装mysql

```
sudo yum install -y mysql-server
```

4.启动

```
service mysqld restart
```

附:设置密码

```
//进入mysql控制台
mysql
mysql > use mysql;
//123456为你的密码，请修改
mysql > update user set password=password('123456') where user='root'; 
mysql > exit;
```
重启
```
service mysqld restart
```

