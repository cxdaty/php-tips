
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
