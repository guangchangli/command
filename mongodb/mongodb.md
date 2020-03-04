### mongodb

1. Brew 安装 

   ```
   brew install mongodb@4.0
   brew cask install mongodb-comprass
   // 启动
   brew services start mongodb-community@4.0
   // 关闭
   brew services stop mongodb-community@4.0
   ```

2. 基本操作

   ```
   启动 ./mongod --port=27017 --dbpath=/usr/local/xx
   存放在 /usr/local/var/mogodb
   客户端连接 ./mogo --port 27017
   查询所有库 show databases; | show dbs; 不显示库中没有集合的库
   选中库 use db;
   查询当前所在库 db;
   创建库 use xxx; 创建完直接切换到库
   查询集合 show collections | show tables
   创建集合 db.createCollection("xxx")
   
   ```

   ```
   库 
   删除库 use xx ; db.dropDatabase();
   db.help()
   ```

   ```
   集合
   显式创建 db.createCollection(“集合名称”)
   隐式创建 db.集合名称.insert({"name":"张三"})
   删除集合 db.集合名称.drop()
   db.集合名称.help()
   CRUD
   添加  db.集合名称.insert({})  db.集合名称.insert([{},{}]) 
   查询  db.集合名称.find() 查询所有
   		 db.集合名称.count 条数
   			
   删除  db.集合名称.remove({}) 删除所有
   		 db.集合名称.remove({删除条件})
          , == & {name:""，age:13}
   修改  db.集合名称.update({更新调价},{更新内容}) 先删除，在添加
        db.集合名称.update("更新条件",{$set:{name:""}}) 保留，只能修改符合条件的第一条数据
        db.集合名称.update("更新条件",{$set:{name:""}},{multi:true}) 开启多行更新
        db.集合名称.update("更新条件",{$set:{name:""}},{multi:true,upsert:true}) 
        没有符合条件时插入
        $inc 让指定的字段自增指定布长
   ```

3. 支持j s脚本，more分页显示20, it翻页



