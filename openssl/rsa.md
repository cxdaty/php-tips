<h1 align="center">windows：RSA:生成私钥对</h1>

下载openssl.zip

```
下载openssl.zip
```

1. 生成原始 RSA私钥文件 private_key.pem

```
genrsa -out private_key.pem 1024
```


2. 将原始 RSA私钥转换为 pkcs8格式

```
pkcs8 -topk8 -inform PEM -in private_key.pem -outform PEM -nocrypt -out rsa_private_key.pem
```


3. 生成 RSA公钥 rsa_public_key.pem

```
rsa -in private_key.pem -pubout -out rsa_public_key.crt
```

3. 获取文件

```
rsa_private_key.pem

rsa_public_key.crt
```







