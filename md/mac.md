# mac	

- 刷新dns

  ```
  sudo killall -HUP mDNSResponder
  sudo dscacheutil -flushcache
  ```

- Svn 日志

  ```
  svn log -l num
  ```

- 端口

  ```
  lsof -i tcp:8080 
  sudo lsof -i -P | grep -i "listen"
  ```

  ```
  sudo lsof -i -P | grep -i "listen"
  ```

- 当前环境

  ```
  env
  ```

- 文件

  ```
  df [-g] 文件系统使用
  du  当前文件
  df -h
  ```

- Vim 跳转

  ```
  ngg  跳转
  gg   文件首行
  G    文件最后一行
  H 	 屏幕首行
  M 	 屏幕中间
  L		 屏幕最后
  $    行尾
  ^ 	 行首
  :n enter
  :nu 行号  
  永久行号
  修改 ～/.vimrc set number
  ```

- vim 移动

  ```
  k 上移
  j 下移
  h 左移
  l 右移
  ctrl f 上一页
  ctrl b 下一页
  * 当前下一个
  # 当前下一个
  gg 
  ```

- 搜索

  ```
  /str 正向搜索
  n 	 跳转到下次
  ?str 反向搜索
  N    跳转到上次
  ```

- 文件查找

  ```
  find  path -iname  file ["str*"]
  mdfind -name str
  mdfind -onlyin path str 路径下所有
  ```

- Bash_profile

  ```
  # jdk相关配置
  export JAVA_8_HOME="$(/usr/libexec/java_home -v 1.8)"
  export JAVA_13_HOME="$(/usr/libexec/java_home -v 13)"
  alias jdk8='export JAVA_HOME=$JAVA_8_HOME'
  alias jdk13='export JAVA_HOME=$JAVA_13_HOME'
  export JAVA_HOME=$JAVA_8_HOME
  
  # maven
  export M2_HOME=/usr/local/apache-maven-3.6.3
  export PATH=${PATH}:${M2_HOME}/bin
  export JAVA_HOME=$JAVA_8_HOME
  
  # mysql
  PATH=$PATH:/usr/local/mysql/bin
  
  PATH=/bin:/usr/bin:/usr/local/bin:${PATH} 
  export PATH
  ```

- Mvn settings

  ```
  <?xml version="1.0" encoding="UTF-8"?>
  <settings xmlns="http://maven.apache.org/SETTINGS/1.0.0"
            xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
            xsi:schemaLocation="http://maven.apache.org/SETTINGS/1.0.0 http://maven.apache.org/xsd/settings-1.0.0.xsd">
      <localRepository>/usr/local/repo</localRepository>
    <pluginGroups>
    </pluginGroups>
    <proxies>
    </proxies>
    <servers>
      <server>
        <id>nexus-server</id>
        <username>admin</username>
        <password>admin123</password>
      </server>
    </servers>
    <mirrors>
      <mirror>  
    		<id>alimaven</id>  
    		<name>aliyun maven</name>  
    		<mirrorOf>central</mirrorOf>          
  	</mirror>
    </mirrors>
    <profiles>
    </profiles>
  </settings>
  ```
  
- iterm2

  ```
  跳转
  ctrl a 行首
  ctrl e 行尾
  command k/r 清屏 ctrl l
  ctrl u 清楚当前行
  从光标处删到行首/尾 ctrl w/k
  command alt / 最近打开记录
  command option 矩形选中
  command shift h 打开最近记录
  command shift B 时间
  ```

- 权限

  ```
  文件类型 主权限（user） 组权限(gtroup) 其他权限(other)
  ```

  ###### 文件类型

  ```
  d 目录
  - 文件
  l 链接
  b 表示为装置文件里面的可供存储的接口设备 可随机存取装置
  c 表示为装置文件里面的串行端口设备
  ```

  修改权限

  ```
  chmod u=rwx,g=rwx,o=r file.txt
  ```

  查看组

  ```
  cat /etc/passwd     #可以查看所有用户的列表
  w                   #可以查看当前活跃的用户列表
  
  cat /etc/group      #查看用户组
  groups   #查看当前登录用户的组内成员
  groups   #test 查看test用户所在的组，以及组内成员
  whoami   #查看当前登录用户名
  ```

  删除账号

  ```
  userdel [-r] 用户名 -r 删除用户目录
  ```

  修改账号

  ```
  usermod [] 用户名
  ```

  赋予权限（u、g、o）

  ```
  chmod ugo+r a.sh 或 chmod a+r  a.conf 		   所有用户读权限
  chmod a+r,ug+w,o-w a.conf b.xml       	    当前用户和所在组可读写，其他只能读
chmod -R a+rw *															当前目录以及子目录所有用户可读写
  ```
  
- iterm

  ```
  
  命令	说明
  command + t	新建标签
  command + w	关闭标签
  command + 数字 command + 左右方向键	切换标签
  command + enter	切换全屏
  command + f	查找
  command + d	垂直分屏
  command + shift + d	水平分屏
  command + option + 方向键 command + [ 或 command + ]	切换屏幕
  command + ;	查看历史命令
  command + shift + h	查看剪贴板历史
  ctrl + u	清除当前行
  ctrl + l	清屏
  ctrl + a	到行首
  ctrl + e	到行尾
  ctrl + f/b	前进后退
  ctrl + p	上一条命令
  ctrl + r	搜索命令历史
  ```

  