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

