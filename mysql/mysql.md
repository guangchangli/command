### mysql

#### 1.数据类型

```
mysql 一行数据长度最大为 65535B
varchar 类型 最大 65535B-2B(存储长度 1-2B) [-1B(存储字段为空)]-1B(从第二个B开始存储)=65531.  
65532/4=16383 utfbmn4
65532/3=21844 utf8
字符集
utf8mb4  1:4 char:B
utf8     1:3 char:B
varchar(L) L就是字符长度 根据字符集计算长度
mysql8 非空字段没有占内存
```

```
utf-8 编码下，一个汉字 字符 占用 3 个 字节；数字属于汉字，和汉字占用一样字节
gbk 编码下，一个汉字  字符  占用 2 个 字节
```

### 数字类型

| **列类型**         | **需要的存储量**                          |
| ------------------ | ----------------------------------------- |
| `TINYINT`          | 1 字节                                    |
| `SMALLINT`         | 2 个字节                                  |
| `MEDIUMINT`        | 3 个字节                                  |
| `INT`              | 4 个字节                                  |
| `INTEGER`          | 4 个字节                                  |
| `BIGINT`           | 8 个字节                                  |
| `FLOAT(X)`         | 4 如果 X < = 24 或 8 如果 25 < = X < = 53 |
| `FLOAT`            | 4 个字节                                  |
| `DOUBLE`           | 8 个字节                                  |
| `DOUBLE PRECISION` | 8 个字节                                  |
| `REAL`             | 8 个字节                                  |
| `DECIMAL(M,D)`     | `M`字节(`D`+2 , 如果`M < D`)              |
| `NUMERIC(M,D)`     | `M`字节(`D`+2 , 如果`M < D`)              |

###  日期和时间类型

| **列类型**  | **需要的存储量** |
| ----------- | ---------------- |
| `DATE`      | 3 个字节         |
| `DATETIME`  | 8 个字节         |
| `TIMESTAMP` | 4 个字节         |
| `TIME`      | 3 个字节         |
| `YEAR`      | 1 字节           |

###  串类型

| **列类型**                    | **需要的存储量**                                         |
| ----------------------------- | -------------------------------------------------------- |
| `CHAR(M)`                     | `M`字节，`1 <= M <= 255`                                 |
| `VARCHAR(M)`                  | `L`+1 字节, 在此`L <= M`和`1 <= M <= 255`                |
| `TINYBLOB`, `TINYTEXT`        | `L`+1 字节, 在此`L`< 2 ^ 8                               |
| `BLOB`, `TEXT`                | `L`+2 字节, 在此`L`< 2 ^ 16                              |
| `MEDIUMBLOB`, `MEDIUMTEXT`    | `L`+3 字节, 在此`L`< 2 ^ 24                              |
| `LONGBLOB`, `LONGTEXT`        | `L`+4 字节, 在此`L`< 2 ^ 32                              |
| `ENUM('value1','value2',...)` | 1 或 2 个字节, 取决于枚举值的数目(最大值65535）          |
| `SET('value1','value2',...)`  | 1，2，3，4或8个字节, 取决于集合成员的数量(最多64个成员） |

```
text与blob的区别在于:text不能存储图片。blob是二进制流，text是非二进制。

mysql 的二进制数据类型 BINARY, VARBINARY, BLOB 都没有字符集的概念。
```

### 2.unsigned zerofill

```
两个unsigned  字段类型数据运算结果也是 unsigned 
#set sql_mode = 'NO_UNSIGNED_SUBTRACTION';解决 unsigned 运算错误
zerofill 为达到指定长度前面补0
```

### 3.修改数据库操作

```
添加字段
ALTER TABLE `tableName` ADD COLUMN `columnName` varchar(255) NOT NULL DEFAULT '0' ;
删除字段
alter table `tableName` drop `columnName`
修改字段类型
ALTER TABLE `tableName` MODIFY `columnName` VARCHAR(50);
修改字段名
ALTER TABLE `tableName` CHANGE `columnName` `newColumnName` VARCHAR(50);
修改表名
ALTER TABLE `tableName` RENAME TO `newTableName`;
```

### 4.操作

```
in  or  in 更快
and or  and 优先级更高
not 支持IN、BETWEEN和EXISTS子句取反
权限 show grants
状态 show status
创建信息 show create database/table databaseName/tableName
show errors (显示服务器错误)
show warnings (显示服务器警告)
```



### 2.TODO 

```
字段的约束信息在哪存？
```

### 3.index

```
什么时候走索引
```

