# mac

​	

```
alias ll='ls -alF'
alias la='ls -A'
alias l='ls -CF'
alias del='rm -f'
alias cc='clear'
alias bp='vim ~/.bash_profile'
```

​	

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

- github

  ```
  s 搜索
  i:name 
  
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
  ```

  