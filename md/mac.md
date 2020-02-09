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

- homebrew

  ```
  /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/uninstall)"
  
  /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
  

  coding 
  $ cd "$(brew --repo)" && git remote set-url origin https://git.coding.net/homebrew/homebrew.git
  
  $ cd $home && brew update 
  五分钟一次刷新
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
  command shift B 时间轴
  ```

  

