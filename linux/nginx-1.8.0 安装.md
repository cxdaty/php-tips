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
