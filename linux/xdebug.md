<h1 align="center">Xdebug</h1>

1.下载xdebug

```
通过phpinfo()查看php对应的版本和操作系统的位数，https://xdebug.org/download.php 下载对应的xdebug版本
```

2.配置php.ini

```
[xdebug]
zend_extension ="E:/cxd/wamp/wamp64/bin/php/php5.6.25/ext/php_xdebug-2.4.1-5.6-vc11-x86_64.dll"
xdebug.profiler_enable = off
xdebug.profiler_enable_trigger = off
xdebug.profiler_output_name = cachegrind.out.%t.%p
xdebug.profiler_output_dir ="E:/cxd/wamp/wamp64/tmp"
xdebug.show_local_vars=0

xdebug.auto_trace=On
;是否收集变量
xdebug.collect_vars= On
;是否收集返回值
xdebug.collect_return= On
;是否收集参数
xdebug.collect_params= On
;跟踪输出路径
xdebug.trace_output_dir="F:\xdebug"
;是否开启调试内容
xdebug.profiler_enable=On

xdebug.remote_enable = On
xdebug.remote_mode=req
xdebug.remote_handler=dbgp
xdebug.remote_host=localhost
xdebug.remote_port=9001
xdebug.idekey=netbeans-xdebug
xdebug.remote_log = "E:/cxd/wamp/wamp64/logs/xdebug.log"

output_buffering = Off
```

3.netbeans配置xdebug

```
xdebug.remote_port=9001
xdebug.idekey=netbeans-xdebug
xdebug.remote_log = "E:/cxd/wamp/wamp64/logs/xdebug.log"

output_buffering = Off
```

4.调试

```
窗口-调试-变量,断点,会话
```