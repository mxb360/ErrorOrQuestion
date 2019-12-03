## 问题：
执行：`git push -u origin master`报错：
```shell
git clone server certificate verification failed. CAfile: /etc/ssl/certs/ca-certificates.crt CRLfile
```

## 原因：
系统并不信任你所要git的网站，所以通不过系统安全认证。

## 解决方案：
关闭系统的安全认证

全局配置：
```shell
git config --global http.sslverify false
```

当前项目配置
```shell
git config http.sslverify false
```
