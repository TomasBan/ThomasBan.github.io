---
layout: post
title:  OSX Supervisor报错
date: 2019-06-06 16:23:51.000000000 +09:00
---

## 问题描述
一开始用`brew`安装的supervisor，一开始没有使用。在安装php5.6之后，先让`supervisor`来管理`php-fpm`，进入`superviosrctl`，在命令后下报了以下的错误

```bash
error: <class 'xmlrpclib.ProtocolError'>, <ProtocolError for 127.0.0.1/RPC2: 404 Not Found>: file: /usr/local/Cellar/supervisor/3.3.5/libexec/lib/python2.7/site-packages/supervisor/xmlrpc.py line: 519
```

## 问题解决

1.一开始以为是`supervisord`出了问题，去修改`supervisord`的配置问题，后面发现不是`supversiord`的问题；
2.然后怀疑是`supervisord`与原本的`docker`监听端口`9001`发生冲突，于是修改`supervisord.ini`里面的端口，修改之后发现没有任何的改善；
3.最后发现是`supervisorctl`在没代`-c`参数的时候，会调用其他目录的`supervisord.ini`的配置文件，在进入`supervisorctl` 加上`-c`参数引入`supervisord.ini`的配置文件即可

## 参考博客

- [supervisor进程管理中的常用命令](http://www.04007.cn/article/245.html)
