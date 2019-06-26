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
