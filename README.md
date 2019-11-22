# Git常用指令

## 1，创建自己的本地私有仓并初始化

 	在本地安装好Git后，在需要上传的项目所在的目录下打开Git命令界面（.git中存放的文件是与本地库相关的内容，不要删除修改）

```
$ git init
```

## 2，设置签名（区分不同的开发人员）

​	这里的签名与登录远程仓库的账号密码无关

### 	2.1 签名级别(就近原则 项目级别>系统级别）

​		项目级别

```
$ git config user.name zhou
$ git config uesr.email zhoujianan@163.com
```

​		系统用户级别

```
$ git config --global user.name zhou
$ git config --global uesr.email zhoujianan@163.com
```

​		查看用户

```
$ cat .git/config
```

## 3，查看状态

```
$ git status
```

![](C:\Users\fer miss together\AppData\Roaming\Typora\typora-user-images\1565084478099.png)

## 4，添加文件到暂存区（添加完成后  添加文件的颜色会改为绿色）

```
$ git add 文件名  
$ git add .   # 添加当前目录下所有可提交文件
```

### 	4.1 删除暂存区中的文件

```
$ git rm --cached 文件名 # 只是删除暂存区中跟踪的文件 不会删除本地工作区文件
```

### 	4.2 将暂存区的内容提交到版本库

```
$ git commit #将暂存区中所有文件全部提交到版本库  
$ git commit <file>  # 提交指定文件
```

![](C:\Users\fer miss together\AppData\Roaming\Typora\typora-user-images\1565084631643.png)

**执行提交命令后会出现如图的界面  在首行插入本次提交的内容的描述，告知协同者本次你的提交做了什么**

​	4.3 对于已经提交到版本库的内容  进行修改后可以直接进行   git commit <file> 重新提交到版本库，当然也可以按照之前的步骤先add  在commit   (**最好按部就班**)

​	4.4 对于单文件的修改提交操作（可以避免进入Vim界面操作）

```
$ git commit -m "对文件修改的内容描述" <file>
```

![](C:\Users\fer miss together\AppData\Roaming\Typora\typora-user-images\1565084675260.png)

## 5 查看版本库历史操作记录

```
$ git log
```

![](C:\Users\fer miss together\AppData\Roaming\Typora\typora-user-images\1565084756274.png)

### 	5.1 简便直观查看操作记录

```
$ git log --pretty=oneline
```

![](C:\Users\fer miss together\AppData\Roaming\Typora\typora-user-images\1565084795037.png)

### 	5.2 查看版本回退是需要操作的次数

```
$ git reflog
```

![](C:\Users\fer miss together\AppData\Roaming\Typora\typora-user-images\1565084828762.png)

## 6，基于HEAD指针的历史版本的前进与后退

### 	6.1 基于索引控制版本前进后退

```
$ git reset --hard 2e5a0de  # hard后面跟随的是相应版本的索引值
```

![](C:\Users\fer miss together\AppData\Roaming\Typora\typora-user-images\1565084856737.png)

### 	6.2  使用^符号（只能控制版本后退）

```
$ git reset --hard HEAD^   # 一个^表示后退一个版本，后退多个版本就用多个^
```

### 	6.3  使用~符号  （只能控制版本后退）

```
$ git reset --hard HEAD~1  #~后面的数字表示后退的版本数
```

​	**后面两种用的不多  最好使用索引的方法**

## 7，reset命令的三个参数

### 	7.1 --soft

​		仅仅在版本库移动HEAD指针

### 	7.2 --mixed

​		在版本库移动HEAD指针

​		重置暂存区

### 	7.3 --hard

​		移动版本库HEAD指针

​		重置暂存区

​		重置工作区

## 8，通过版本回退恢复彻底删除的文件（**前提是删除的文件之前有提交到版本库**）

```
$ git rm <文件>
```



![](C:\Users\fer miss together\AppData\Roaming\Typora\typora-user-images\1565084889365.png)

**Git版本控制会永久的记住之前每个版本的操作，所有虽然三个区里都已经没有该文件但是可以通过版本回退恢复删除的文件**

## 9，diff命令（文件比较）

```
$ git diff aaa.txt
```

![](C:\Users\fer miss together\AppData\Roaming\Typora\typora-user-images\1565084917501.png)

也可以与之前版本库中的历史版本进行比较（**不跟随文件名的时候就比较所有文件**）

![](C:\Users\fer miss together\AppData\Roaming\Typora\typora-user-images\1565084943522.png)

## 10 ，分支操作

### 	10.1 创建分支

```
$ git branch <分支名称>
```

### 	10.2 查看分支

```
$ git branch -v 
```

![](C:\Users\fer miss together\AppData\Roaming\Typora\typora-user-images\1565084975451.png)

### 	10.3 切换分支

```
$ git checkout <分支名>
```

### 	10.4 合并分支

​		1，合并分支之前必须将分支切换到被合并的分支（也就是增加内容的分支或者说该分支上一级）

```
$ git merge <分支名>
```

![](C:\Users\fer miss together\AppData\Roaming\Typora\typora-user-images\1565085023002.png)

### 	10.5 解决冲突

​		1 产生冲突的原因：两个分支操作同一个文件的同一处内容，git在合并的时候无法分辨该以哪一处修改为主，所以这里需要开发者手动操作

![](C:\Users\fer miss together\AppData\Roaming\Typora\typora-user-images\1565085059153.png)

![](C:\Users\fer miss together\AppData\Roaming\Typora\typora-user-images\1565085094140.png)

### 	10.6 删除分支

```
$ git branch -d <分支名>
```

​		1 不能删除当前分支

​		2 如果要删除的分支已经成功合并到当前分支，删除分支的操作会直接成功。

​		3 如果要删除的分支没有合并到当前所在分支，则会出现提示，如果确定无须合并而要直接删除，则执行命令：

```
$ git branch -D <分支名>
```

### 	10.7 分支重命名

```
$ git branch -m <旧分支名> <新分支名>
```

​		1 **-m**不会覆盖已有分支名称，即如果名为newname的分支已经存在，则会提示已经存在了。

　　如果改成**-M**就可以覆盖已有分支名称了，即会强制覆盖名为newname的分支，这种操作要谨慎。

## 11，本地库与远程库建立连接

### 	11.1 创建好远程库获取远程连接地址  在本地给地址去一个别名

```
$ git remote add <别名> <远程库连接地址>
$ git remote -v  #查看所有别名
```

​	![](C:\Users\fer miss together\AppData\Roaming\Typora\typora-user-images\1565142553207.png)

## 12， 本地库数据推送到远程库

```
$ git push tpp master   # 推送内容必须指定分支
```

![](C:\Users\fer miss together\AppData\Roaming\Typora\typora-user-images\1565142817133.png)

![](C:\Users\fer miss together\AppData\Roaming\Typora\typora-user-images\1565142859295.png)

## 13， 克隆操作

```
$ git clone <GitHub上项目的地址>
```

![](C:\Users\fer miss together\AppData\Roaming\Typora\typora-user-images\1565143435281.png)

## 14 ，远程库修改的拉取

​	pull操作其实在两个命令合并的结果：fetch  将远程库的修改拉取到本地但是不修改本地的文件

​									merge  将远程库修改的文件合并到本地库

```
$ git fetch tpp master  #  复杂的修改做好分步操作，避免数据混乱
$ git merge tpp/master
```

```
$ git pull tpp master # 较为简单的修改直接pull
```

## 15 ，远程库协同开发

​	协同开发人员操作将自己本地库的内容推送到远程库，如果不是基于GitHub最新版则无法推送，必须先进行拉取操作

​	拉取下来后如果进入冲突状态则按照"分支冲突解决"方式解决

## 16 ，打标签

在进行迭代开发的过程中，对于一些文档的版本可以打上便签（tag）,一边后期出现问题的时候进行版本回退

```
$ git tag -a v1.0 -m <对该版本的注释>  # 默认当前版本 如果在在其他版本打便签  要通过log切换版本
$ git show <标签名>
```

![](C:\Users\fer miss together\AppData\Roaming\Typora\typora-user-images\1565148579266.png)