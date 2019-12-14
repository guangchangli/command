# linux

```
ln –s 源文件 目标文件 软链接 生成映像创建快捷方式
ln 源文件 目标文件 硬链接 创建一个文件大小相同的文件 
软链接和硬链接文件同步变化
```



### 1.安装vim

```
yum -y install vim*
```

### 2.jdk

```
export JAVA_HOME=/usr/local/java/jdk        
export PATH=$JAVA_HOME/bin:$PATH
export CLASSPATH=.:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar
```

### 3.关闭防火墙

```
service iptables stop 
chkconfig  iptables off 
开启
service iptables start
chkconfig iptables on
重启
service iptables restart
配置文件
/etc/sysconfig/iptables
```

### 4.桥接静态ip

```
BOOTPROTO=static        #开机协议
ONBOOT=yes              #设置为开机启动；
DNS1=114.114.114.114    #DNS地址
IPADDR=192.168.2.2      #设置的固定IP
NETMASK=255.255.255.0   #子网掩码
GATEWAY=192.168.2.1     #网关
复制的虚拟机 
修改网卡
```

### 5.zookeeper

#### 1.安装zookeeper

```

将conf文件夹下zoo_sample.cfg复制一份，改名为zoo.cfg
修改配置dataDir属性，指定一个真实目录
启动zookeeper：bin/zkServer.sh start
关闭zookeeper：bin/zkServer.sh stop
查看zookeeper状态：bin/zkServer.sh status
```

#### 2.安装Dubbo-admin 

```
Dubbo部署监控中心
webapps/dubbo-admin.war
启动tomcat，访问 8080/dubbo-admin/
用户名：root
密码：root

如果监控中心和注册中心在同一台服务器上，可以不需要任何配置。
如果不在同一台服务器，需要修改配置文件：
/webapps/dubbo-admin/WEB-INF/dubbo.properties
修改注册中心地址
```

### 6.vsftpd

```
yum install -y vsftpd
启动vsftpd:  service vsftpd start
停止vsftpd:  service vsftpd stop
重启vsftpd:  service vsftpd restart
状态vsftpd:  service vsftpd status
开机启动：chkconfig vsftpd on
```

```
/etc/vsftpd/vsftpd.conf   主配置文件，核心配置文件
 /etc/vsftpd/ftpusers      黑名单，这里面的用户不允许访问FTP服务器
 /etc/vsftpd/user_list      白名单，允许访问FTP服务器的用户列表
```

```
vim /etc/vsftpd/vsftpd.conf
将配置文件中，“ /etc/vsftpd/vsftpd.conf ”中的“anonymous_enable=YES” 改为“anonymous_enable=NO”
```

```
添加用户
useradd ftpuser -s /sbin/nologin -d /home/ftp
home/ftp文件路径u	
passwd ftpuser  #输入两次密码，匹配成功

setsebool -P ftp_home_dir 1   #允许用户访问自己的根目录
编辑 /etc/vsftpd/  vsftpd.conf 
userlist_deny=NO 参数这个参数=NO 代表 这个配置信息的用户可以访问FTP
```

### 7.nginx

#### 1.环境

```
环境要求 c语言编写的
	gcc
	安装nginx需要先将官网下载的源码进行编译，编译依赖gcc环境，如果没有gcc环境，需要安装gcc。
yum install gcc-c++ 
	PCRE
	PCRE(Perl Compatible Regular Expressions)是一个Perl库，包括 perl 兼容的正则表达式库。nginx的http模块使用pcre来解析正则表达式，所以需要在linux上安装pcre库。
yum install -y pcre pcre-devel
注：pcre-devel是使用pcre开发的一个二次开发库。nginx也需要此库。
	zlib
	zlib库提供了很多种压缩和解压缩的方式，nginx使用zlib对http包的内容进行gzip，所以需要在linux上安装zlib库。
yum install -y zlib zlib-devel

	openssl
	OpenSSL 是一个强大的安全套接字层密码库，囊括主要的密码算法、常用的密钥和证书封装管理功能及SSL协议，并提供丰富的应用程序供测试或其它目的使用。
	nginx不仅支持http协议，还支持https（即在ssl协议上传输http），所以需要在linux安装openssl库。
yum install -y openssl openssl-devel

```

#### 2.安装

```
进入nginx文件夹，使用./configure执行编译：
		## 安装到/usr/local/java/nginx的nginx目录下
       ./configure --prefix=/usr/local/java/nginx
安装nginx，执行：
			make
			make install

```

```
启动
/sbin ./nginx 
停止
/sbin ./nginx -s stop
重启
/sbin ./nginx -s reload
退出
/sbin ./nginx -s quit
```

#### 3.配置代理

```
编辑 /conf nginx.conf

upstream server_list{
  server ip:8080;
  server ip:8080;
  ip_hash;
  
}
location / {
  proxy_pass server_list;
  proxy_set_header HOST $host;
}
location ~* \.(jpg|jpeg|gif|js|css)$ {
  root //;
  proxy_set-header HOST $host;
}

```



### 8.redis

```
c语言开发的需要c语言环境
yum install gcc-c++
安装
/redis 
make 
make install PREFIX=/安装到指定目录
```

```
修改链接方式
源码目录 redis.conf
修改 daemonize yes 后段启动
```

```
启动
./redis-server redis.conf
连接
./redis-cli -h -p 6379
关闭
shutdown
./redis-cli shutdown
```

##### 四种数据类型方法

| string | set set     | get get                   | Del       | 常用主键自增 incr 存的是 k v |
| :----- | ----------- | ------------------------- | --------- | ---------------------------- |
| hash   | hset hmset  | get hmget                 | hdel      | 存的是 k map                 |
| List   | lpush rpush | lrange k 0 -1             | lpop rpop | 链表                         |
| set    | sadd        | smemebers                 | srem      | 无序不允许重复               |
| zset   | zadd k i v  | zrevrange 0 -1 withscores | Orem k    | 有序不允许重复               |

##### 集群搭建

```
redis集群通过
```

```
安装ruby
yum install ruby
yum install rubygems

```

### 9.solr-cloud

```
上传会报错
想执行 solrhome 配置文件上传命令：
./zkcli.sh -zkhost 192.168.0.1:218 -cmd upconfig -confdir /usr/local/solr-cloud/solrhome01/collection1/conf/ -confname myconf

要安装 unzip zip
安装完之后，还需要在 /solr-4.10.3/example 目录下执行：
java -jar start.jar

```

