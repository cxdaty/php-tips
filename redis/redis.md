### Redis

- Win+R快捷键，输入CMD，进入CMD窗口，进入解压后文件所在路径，并输入以下指令：
```
redis-server.exe redis.windows.conf
```

- 启动客户端
```
redis-cli.exe
```

- 密码登录：如果设置了登录密码，则需要再输入密码才能登陆成功
```
auth yourPasspord
```

- 设置密码
```
CONFIG SET requirepass myPassword
```

- 退出客户端
```
quit
```

- php安装redis扩展
```
 1.phpinfo()函数查看PHP的版本信息，下载对应的扩展版本
 2.php_redis-2.2.5-5.6-ts-vc11-x64.zip和php_igbinary-1.2.1-5.5-ts-vc11-x64.zip(对应的版本信息)
 3.copy到ext目录
 4.修改php.ini，在该文件中加入：
   ; php_redis
   extension=php_igbinary.dll
   extension=php_redis.dll
```

- 常用
```
 1.$redis = new \Redis();
   $redis->connect('127.0.0.1',6379);
   $redis->auth('password');
 2.$redis->exists($key);
   $redis->hSet();
   $redis->set('key',$value);
   $redis->hGet();
   $redis->hdel();
   $redis->expire($key,86400);
3.事务
   $redis->multi();
   $res = $redis->exec();
```