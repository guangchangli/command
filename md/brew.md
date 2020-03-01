### brew

1. tips

   ```
   一、实用的
   
   1、代替 cat 的工具：bat，支持语法高亮、同时显示行号，使用: bat xx.yyy
   
   安装：brew install bat
   
   2、man 命令的替代品：tldr
   
   安装：brew install tldr 
   
   二、好玩的
   
   1、命令行显示黑客帝国数字雨，运行: cmatrix
   
   安装: brew install cmatrix
   
   2、在命令行中开火车，运行：sl
   
   安装: brew install sl
   
   3、在命令行把输出变成七彩，运行: ls | lolcat，需要配合其他程序使用
   
   安装: brew install lolcat
   
   4、把你的命令行变成海洋馆，运行: asciiquarium
   
   安装: brew install asciiquarium
   
   5、会说话的 ascii 奶牛, 运行：cowsay <你想说的话>
   
   安装: brew install cowsay
   	   cowsay -l 查看可用
   	   cowsay -f turtle xxx
   ```

   ```
   alias lsl='ls|lolcat'
   ```

2. use command

   ```
   brew list 
   brew outdated   查询可以更新的包
   brew upgrade    更新所有包
   brew upgrade x  更新指定包
   brew cleanup    清理所有包的旧版本
   brew cleanup x  清理指定
   brew uninstall formula_name --force 卸载包
   brew pin $FORMULA       锁定某个包
   brew unpin $FORMULA     取消锁定
   brew info $FORMULA      显示某个包的信息
   brew info               显示安装了包数量，文件数量，和总占用空间
   brew deps --installed --tree  查看已安装的包的依赖，树形显示
   ```

   code节点

   ```
   /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/uninstall)"
   
   /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
   
   
   coding 
   $ cd "$(brew --repo)" && git remote set-url origin https://git.coding.net/homebrew/homebrew.git
   
   $ cd $home && brew update 
   五分钟一次刷新
   ```

   