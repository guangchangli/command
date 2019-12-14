### Linux软件安装

------

主要安装：

jdk			版本 1.8

tomcat		版本 8

mysql		版本 5.7



####第一节  JDK安装

#####1.1. 下载JDK,此处版本是1.8u131,实际操作以自己具体版本为准
 先查看Linux系统是多少位（32位/64位）：getconf LONG_BIT 然后去官网下载JDK

[jdk官方下载地址]: http://www.oracle.com/technetwork/java/javase/downloads/index.html

#####1.2. 解压安装

###### 1.2.1 卸载和下载jdk

	查看是否安装过java
	rpm -qa | grep java
	如果是centos 一般会自带两个openjdk
	rpm -e --nodeps 要卸载的包 (包通过上面的指令可以获取到)]
	先卸载7 再卸载6 最后卸载5
	命令：
	rpm -e --nodeps 要卸载的包
选择安装JDK的位置/opt/install，如果存在这个目录无需创建，一般新到的机器是没有这个目录的，这个我们创建这个目录。
指令  需要输入密码

	管理员：
	mkdir /opt/install
	非管理员：
	sudo mkdir /opt/install
###### 1.2.2上传和解压

将jdk-8u131-linux-x64.tar.gz上传到服务器的/opt/install。

可以使用SecureFXPortable(或者filelilla)将文件上传到服务器 



解压：进入/opt/install目录（cd /opt/install）解压

```
cd /opt/install   		切换到/opt/install
ls					显示当前目录下所有文件和目录
tar -zxvf jdk-8u131-linux-x64.tar.gz	解压到当前目录
rm -f jdk-8u131-linux-x64.tar.gz		删除jdk-8u131-linux-x64.tar.gz
```


#####1.3. jdk环境变量配置

打开/etc/profile

```
 vi  /etc/profile
```

在文档的最后面添加如下内容，记住不要带空格

```
export JAVA_HOME=/opt/install/jdk1.8.0_131
export JRE_HOME=$JAVA_HOME/jre
export CLASSPATH=.:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar:$JRE_HOME/lib
export PATH=$PATH:$JAVA_HOME/bin

注意：
	$JAVA_HOME 代表得到JAVA_HOME环境变量的值
	$PATH:$JAVA_HOME/bin： 冒号代表的是连接符号
```



让配置生效：

	source /etc/profile

#####1.4. 验证

	java –version
####第二节 tomcat安装

##### 2.1下载和安装

下载tomcat，从tomcat官网下载tomcat的压缩包。

[Tomcat官网下载](https://tomcat.apache.org/download-80.cgi)



```
tar -zxvf apache-tomcat-8.0.43.tar.gz		解压
mv apache-tomcat-8.0.43  tomcat8			重命名，非必须
```

##### 2.2 启动和访问

```
/opt/work/tomcat8/bin/startup.sh  启动Tomcat
/opt/work/tomcat8/bin/shutdown.sh  关闭Tomcat
```

```
如果启动不成功，修改tomcat下面的bin里面的 setclasspath，在顶部添加路径为自己的 jdk路径：
export JAVA_HOME=/opt/work/jdk1.8.0_131
export JRE_HOME=/opt/work/jdk1.8.0_131/jre
```



```
小技巧：
tomcat内存优化
Tomcat内存优化主要是对tomcat启动参数优化，我们可以在tomcat的启动脚本catalina.sh中设置 JAVA_OPTS 参数。比如服务器是6G内存，所以设置JVM启动参数大些，个人可以根据自己的实际情况进行设置：
JAVA_OPTS='-Xms2048m -Xmx4096m -Xmn1g-Xss1024k -XX:NewRatio=4 -XX:SurvivorRatio=4 -XX:PermSize=1024m-XX:MaxPermSize=1024m -XX:MaxTenuringThreshold=0 -XX:+UseParallelGC-XX:ParallelGCThreads=20 -XX:+UseParallelOldGC -XX:+UseAdaptiveSizePolicy'
```


以上文件所放的目录不是必须的,可以找个自己目录存放
####第三节 mysql安装
#####3.1下载和安装

###### 3.1.1 卸载

先卸载自带的mysql,因为版本较低,卸载方式参考上面卸载java 的方式

```
rpm -qa | grep mysql  查看是否安装过MySQL
rpm -e --nodeps mysql-server-5.1.73-7.el6.x86_64
rpm -e --nodeps mysql-libs-5.1.73-7.el6.x86_64
rpm -e --nodeps mysql-5.1.73-7.el6.x86_64
rpm -e --nodeps qt-mysql-4.6.2-28.el6_5.x86_64
```

###### 3.1.2 下载

```
一般2种方式：
第一种，在线安装使用yum
第二种，离线安装，自己去官网下载对应的rpm，上传服务器，解压，安装即可
```

###### 3.1.3 安装

在线安装

如果提示wget不是命令，则：安装一个插件

 yum -y install wget



```
1. yum install wget
2.wget http://repo.mysql.com/mysql-community-release-el7-5.noarch.rpm 
3. rpm -ivh mysql-community-release-el7-5.noarch.rpm    安装用来配置mysql的yum源的rpm包
		ls /etc/yum.repos.d		可以查看mysql的yum源的配置
4.yum install mysql-server   安装mysql
```



```
在安装rpm -ivh mysql-community-server的时候报错如下：
[root@linux_node_1 src]# rpm -ivh mysql-community-server-5.7.16-1.el7.x86_64.rpm 
  warning: mysql-community-server-5.7.16-1.el7.x86_64.rpm: Header V3 DSA/SHA1 Signature, key ID 5072e1f5: NOKEY
  error: Failed dependencies:
  libaio.so.1()(64bit) is needed by mysql-community-server-5.7.16-1.el7.x86_64
  libaio.so.1(LIBAIO_0.1)(64bit) is needed by mysql-community-server-5.7.16-1.el7.x86_64
  libaio.so.1(LIBAIO_0.4)(64bit) is needed by mysql-community-server-5.7.16-1.el7.x86_64
  net-tools is needed by mysql-community-server-5.7.16-1.el7.x86_64

  这个报错的意思是需要安装libaio包和net-tools包：可以yum安装一下，安装 libaio-0.3.107-10.el6.x86_64.rpm，下载地址：

wget http://mirror.centos.org/centos/6/os/x86_64/Packages/libaio-0.3.107-10.el6.x86_64.rpm
wget http://www.percona.com/redir/downloads/Percona-XtraDB-Cluster/5.5.37-25.10/RPM/rhel6/x86_64/Percona-XtraDB-Cluster-shared-55-5.5.37-25.10.756.el6.x86_64.rpm

  yum install net-tools  
  
```

#####3.2 数据库初始化
	为了保证数据库目录为与文件的所有者为mysql登陆用户，如果你是以root身份运行mysql服务，需要执行下面的命令初始化：
	mysqld --initialize --user=mysql
	如果是以mysql身份运行，则可以去掉 --user 选项。
	另外 --initialize 选项默认以“安全”模式来初始化，则会为 root 用户生成一个密码并将该密码标记为过期，登陆后你需要设置一个新的密码
	而使用 --initialize-insecure 命令则不使用安全模式，则不会为 root 用户生成一个密码。
	这里演示使用的 --initialize 初始化的，会生成一个 root 账户密码，密码在log文件里，位置为/var/log/mysqld.log 
#####3.3运行mysql
	service mysqld start   启动MySQL
	service mysqld stop	   停止MySQL
#####3.4使用mysql 

######3.4.2修改密码 

	先停止mysql:
	 service mysqld stop 
	再跳过mysql验证
	/usr/bin/mysqld_safe --skip-grant-tables &mysql -u root
	最后使用下面指令强制更改密码,注意自mysql5.7开始 密码字段不再是password而是authentication_string(或者password)：
	update mysql.user set password=password('admin') where user='root' and Host = 'localhost';


	记得刷新权限
	flush privileges;
```
重新启动mysql服务,使用新密码即可登录
service mysqld start
```

登录后需要输入密码：mysql -u root -padmin



#### 第四节 防火墙

##### 4.1 Tomcat无法访问

```
查看防火墙状态
firewall-cmd --state
systemctl status firewalld
# 开启
service firewalld start
# 重启
service firewalld restart
# 关闭
service firewalld stop
# 查看防火墙列表
firewall-cmd --list-all 
# 查询端口是否开放
firewall-cmd --query-port=8080/tcp
# 开放80端口
firewall-cmd --permanent --add-port=80/tcp
firewall-cmd --permanent --add-port=8080/tcp
firewall-cmd --permanent --add-port=3306/tcp
firewall-cmd --permanent --add-port=6379/tcp

# 移除端口
firewall-cmd --permanent --remove-port=8080/tcp

#重启防火墙(修改配置后要重启防火墙)
firewall-cmd --reload

# 参数解释
1、firwall-cmd：是Linux提供的操作firewall的一个工具；
2、--permanent：表示设置为持久；
3、--add-port：标识添加的端口；
```

##### 4.2 mysql远程连接

######4.2.1 远程连接的问题 
mysql默认只能本机访问，需要将localhost修改为%即可

	grant all privileges on *.* to 'root' @'%' identified by 'admin';
	以上指令代表允许root用户可以访问数据库下面的任意库(第一个)和任意表(第二个) admin代表root用户的密码
如果在开启远程的时候提示必须修改密码,执行以下操作

	flush privileges;
