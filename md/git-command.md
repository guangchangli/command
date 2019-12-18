## git

1. #### 分支

   ##### 本地分支

   ```
   git branch
   ```

   ##### 远程分支

   ```
   git branch -r  remote
   ```

   ##### 全部分支

   ```
   git branch -a  all 
   ```

   ##### 远程分支和本地分支对应关系

   ```
   git remote show origin
   ```

   ##### 本地分支关联远程分支情况

   ```
   git branch -vv
   ```

   ##### 创建并切换到分支

   ```
   git checkout -b <branch-name>
   ```

   ##### 删除本地分支

   ```
   git branch -d <local-branchname>
   ```

   ##### 删除远程分支

   ```
   git push origin --delete <remote-branchname>
   git push origin :<remote-branchname>
   ```

   ##### 重命名分支

   ```
   git branch -m <new-branch-name>
   ```

   

2. #### 查看log

   ```
   显示【最近 n 次】每次提交差异 git log -p 【-n】
   显示简略提交信息 git log -stat
   显示格式 git log --pretty=oneline/short/full/fuller
   格式化输出 git log --pretty=format:"%h - %an, %ar : %s"
   ```

   ##### Git log

   | 选项             | 说明                                    |
   | ---------------- | --------------------------------------- |
   | -p               | 按补丁显示每个更新之间的差异            |
   | --stat           | 显示每次更新的文件修改统计信息          |
   | --shortstat      | 只显示-stat中最后的行数修改添加移除统计 |
   | --name-only      | 仅在提交信息后显示已修改的文件清单      |
   | --name-status    | 显示新增、修改、删除的文件清单          |
   | --abbrev-commit  | 仅显示SHA-1的前几个字符 不是所有40      |
   | --relative--date | 使用较短的相对时间显示                  |
   | --graph          | 显示ASCII图形表示的疯子合并历史         |

3. #### 撤销操作

   ```
   取消暂存 git reset HEAD fileName 
   ```

4. #### 工作区

   ##### 放弃工作区修改

   ```
   git checkout <file-name>
   git checkout . 放弃所有
   ```

   ##### 工作区和暂存区的区别

   ```
   git diff
   ```

   ##### Commit 之间的区别

   ```
   git diff <commit-id> <commit-id>
   ```

   











### git log --pretty=format参考

| 选项  | 说明                                    |
| ----- | --------------------------------------- |
| %H/ h | 提交对象的完整/简短哈希字串             |
| %T/t  | tree的完整/简短哈希字段                 |
| %P/p  | 父对象的完整/简短哈希字段               |
| %an   | 作者的名字                              |
| %ae   | 作者的电子邮箱地址                      |
| %ad   | 作者的修订日期，可以用 -date=yyyy-MM-dd |
| %ar   | 作者修订日期，按多久之前显示            |
| %cn   | 提交者的名字                            |
| %ce   | 提交者的电子邮件地址                    |
| %cd   | 提交日期                                |
| %cr   | 提交日期，按多久之前的方式显示          |
| %s    | 提交说明                                |

#### svn

##### 清楚账户信息

```
rm -fr  ~/.subversion/auth
```

