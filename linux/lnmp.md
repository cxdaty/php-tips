<h1 align="center">PHP</h1>

1.下载php-5.6.9
```
wget -O php.tar.gz http://cn2.php.net/get/php-5.6.9.tar.gz/from/this/mirror
```

2.解压php

```
tar -xvf php.tar.gz
```

3.进入php目录

```
cd php-5.6.9
```

4.安装依赖包

```
//扩展包更新包
yum  install epel-release
//更新yum源
yum  update
//安装依赖
yum install -y gcc libxml2 libxml2-devel openssl openssl-devel bzip2 bzip2-devel libcurl libcurl-devel libjpeg libjpeg-devel libpng libpng-devel freetype freetype-devel gmp gmp-devel libmcrypt libmcrypt-devel readline readline-devel libxslt libxslt-devel
```

5.编译配置

```
./configure  --prefix=/usr/local/php  --with-config-file-path=/usr/local/php/etc  --enable-fpm  --with-fpm-user=www  --with-fpm-group=www  --enable-inline-optimization  --disable-debug  --disable-rpath       --enable-soap  --with-libxml-dir  --with-xmlrpc  --with-openssl  --with-mcrypt  --with-mhash  --with-pcre-regex  --with-sqlite3  --with-zlib  --enable-bcmath  --with-iconv   --with-curl       --enable-dom  --enable-filter  --with-pcre-dir  --enable-ftp  --with-gd  --with-openssl-dir  --with-jpeg-dir  --with-png-dir  --with-zlib-dir --enable-gd-native-ttf  --enable-gd-jis-conv  --with-gettext       --enable-json  --enable-mbstring  --enable-mbregex  --enable-mbregex-backtrack    --enable-pdo  --with-mysql=mysqlnd  --with-mysqli=mysqlnd  --with-pdo-mysql=mysqlnd  --with-pdo-sqlite  --enable-session  --enable-shmop  --enable-simplexml --enable-sockets --enable-sysvsem --with-libxml-dir --enable-zip --with-pear --enable-opcache
```

6.正式安装
```
make && make install
```

7.配置环境变量
```
vi /etc/profile
//在末尾追加
export PATH=$PATH:/usr/local/php/bin
//执行命令使得改动立即生效
source /etc/profile
```

8.配置php-fpm

```
cp php.ini-production /usr/local/php/etc/php.ini
cp /usr/local/php/etc/php-fpm.conf.default /usr/local/php/etc/php-fpm.conf
cp /usr/local/php/etc/php-fpm.d/www.conf.default /usr/local/php/etc/php-fpm.d/www.conf
cp sapi/fpm/init.d.php-fpm /etc/init.d/php-fpm
chmod +x /etc/init.d/php-fpm
```

9.启动php-fpm
```
service php-fpm start
```



<h1 align="center">phpredis</h1>
1.下载

```
wget https://github.com/phpredis/phpredis/archive/2.2.4.tar.gz
```

2.解压

```
tar -zxvf 2.2.4.tar.gz
```

3.进入目录

```
cd phpredis-2.2.4
//安装依赖 
yum install -y m4 autoconf
```

4.侦测环境

```
/usr/local/php/bin/phpize
```

5.编译

```
./configure --with-php-config=/usr/local/php/bin/php-config
```

6.安装

```
make && make install
```

7.添加redis扩展

```
//修改php.ini
vi /usr/local/php/etc/php.ini
在末尾添加
extension = redis.so
```



<h1 align="center">nginx</h1>

1.下载
```
wget -c https://nginx.org/download/nginx-1.8.0.tar.gz
```

2.解压
```
tar -zxvf nginx-1.8.0.tar.gz
```

3.进入nginx目录

```
cd nginx-1.8.0
```

4.安装依赖包

```
yum install -y gcc-c++ pcre pcre-devel zlib zlib-devel openssl openssl-devel
```

5.编译配置

```
./configure
```

6.正式安装

```
make && make install
```

7.启动、停止

```
//启动
/usr/local/nginx/sbin/nginx
//停止
/usr/local/nginx/sbin/nginx -s stop
```


<h1 align="center">mysql</h1>

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


<h1 align="center">redis</h1>

1.下载

```
wget http://download.redis.io/releases/redis-4.0.6.tar.gz
```

2.解压

```
tar -zxvf redis-4.0.6.tar.gz
```

3.进入目录

```
cd redis-4.0.6
```

4.编译安装

```
make MALLOC=libc
```

5.正式安装

```
cd src
make install
```

6.配置以后台进程方式启动redis

修改redis.conf文件

```
//进入redis安装目录
cd /usr/local/redis-4.0.6
vi redis.conf
```

将
```
daemonize no
```
修改为

```
daemonize yes
```

7.启动设置

在/etc目录下新建redis目录
```
cd /etc
mkdir redis
```
将redis.conf文件复制一份到/etc/redis目录下，并命名为6379.conf
```
cp /usr/local/redis-4.0.6/redis.conf /etc/redis/6379.conf
```
将redis的启动脚本复制一份放到/etc/init.d目录下
```
cp /usr/local/redis-4.0.6/utils/redis_init_script /etc/init.d/redisd
```

8.启动

```
service redisd start
```


<h1 align="center">部署项目代码</h1>

1.创建根目录与日志目录

```
mkdir /home/wwwroot && mkdir /home/wwwlogs
```

2.复制代码到根目录

```
上传代码到目录/home/wwwroot/
创建www用户
useradd www
更改项目所有者为www
chown -R www:www /home/wwwroot/mowork
```

3.配置nginx

```
cp conf/nginx.conf  /usr/local/nginx/conf/nginx.conf
cp conf/enable-php.conf  /usr/local/nginx/conf/enable-php.conf
mkdir /usr/local/nginx/conf/vhost
cp conf/mowork.conf /usr/local/nginx/conf/vhost/mowork.conf

修改mowork.conf配置
vi /usr/local/nginx/conf/vhost/mowork.conf
配置文件说明
server_name 域名
root 项目根目录
```

4.启动所有服务

```
service php-fpm start
service nginx start
service mysql start
service redisd start 
```



