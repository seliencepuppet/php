## linux下安装amqp扩展模块

<br/>

以下错误是php解释器没有安装连接rabbitmq的连接包

```shell
configure: error: Please reinstall the librabbitmq distribution itself or (re)install librabbitmq development package if it available in your system
```

#### 安装rabbitmq-c-0.7.1

没有安装就会提示上面的错误

我选择的是最新版本0.7.1

```shell
[root@zhangyz ~]# wget https://github.com/alanxz/rabbitmq-c/releases/download/v0.7.1/rabbitmq-c-0.7.1.tar.gz
[root@zhangyz ~]# tar zxf rabbitmq-c-0.7.1.tar.gz
[root@zhangyz ~]# cd rabbitmq-c-0.7.1
[root@zhangyz rabbitmq-c-0.7.1]# ./configure --prefix=/usr/local/rabbitmq-c-0.7.1
[root@zhangyz rabbitmq-c-0.7.1]# make && make install

[root@zhangyz ~]# yum install autoconf gcc gcc-c++ cmake librabbitmq-devel librabbitmq
[root@zhangyz ~]# wget https://pecl.php.net/get/amqp-1.6.1.tgz
[root@zhangyz ~]# tar zxf amqp-1.6.1.tgz
[root@zhangyz ~]# cd amqp-1.6.1
[root@zhangyz ~]# /usr/local/php5/bin/phpize
[root@zhangyz amqp-1.6.1]# ./configure --with-php-config=/usr/local/php5/bin/php-config --with-amqp --with-librabbitmq-dir=/usr/local/rabbitmq-c-0.7.1
[root@zhangyz amqp-1.6.1]# make 
[root@zhangyz amqp-1.6.1]# make install
```

在php.ini文件当中添加所需要的扩展模块

```shell
[root@zhangyz ~]# vim /usr/local/php5/etc/php.ini
```

最后添加一行

```shell
extension = /usr/local/php5/lib/php/extensions/no-debug-non-zts-20100525/amqp.so
```

添加完成之后重启apache或nginx
