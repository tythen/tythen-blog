[toc]
## 资源链接

[开源指北git手册](https://oschina.gitee.io/opensource-guide/git_tutorial/Git%20%E5%91%BD%E4%BB%A4%E8%AF%A6%E8%A7%A3/%E5%B8%B8%E7%94%A8%20Git%20%E5%91%BD%E4%BB%A4/#git-%E5%91%BD%E4%BB%A4%E6%89%8B%E5%86%8C)

## 跑个流程

`修改了本地的文件`  
`git add [filename]`添加到暂存库  
`git commit`添加到本地库  
`git push blog master`把当前master分支传到远程库

## 简介
>git是一个版本管理系统，起初是为了开发linux内核而诞生的，它可以保存更新文件的历史  
>集中式版本控制(SVN)，分布式版本控制(Git)  
>显然这个系统基于数据库(Repository)实现，数据库分为远程和本地两种。平时用手头上的机器在本地数据库上操作就可以了。如果想要公开在本地数据库中修改的内容，把内容上传到远程数据库就可以了。  
>提交：若要把文件或目录的添加和变更保存到数据库，就需要进行提交。
>执行提交后，数据库中会生成上次提交的状态与当前状态的差异记录（也被称为revision）。  
>提交时应附上提交信息，格式：  
>
>>第1行：提交修改内容的摘要  
>第2行：空行  
>第3行以后：修改的理由

## git基本配置  
配置都保存在文件中  
系统配置：`C:\Environment\Git\etc\gitconfig`  
用户配置：`C:\Users\tythen\.gitconfig`  
有关命令：  
`git config -l`查看git配置  
`git config --system --list`查看系统配置（全局）  
`git config --global --list`查看用户配置（设置用户  名、邮箱）  
设置我的用户名和邮箱地址：  
`git config --global user.name "tythen"`   
` git config --global user.email "tythen@qq.com"`  

## 三种区域

工作目录
暂存区
资源库  
要想上传到远程库，首先要用git add .存到暂存区


## git的初始化  
使用`git init`和`git clone [url]`

## 文件的四种状态
版本控制就是对文件的版本控制，要对文件进行修改、提交等操作，首先要知道文件当前在什么状态，不然可能会提交了现在还不想提交的文件，或者要提交的文件没提交上。

- Untracked: 未跟踪, 此文件在文件夹中, 但并没有加入到git库, 不参与版本控制. 通过`git add` 状态变为Staged.

- Unmodify: 文件已经入库, 未修改, 即版本库中的文件快照内容与文件夹中完全一致. 这种类型的文件有两种去处, 如果它被修改, 而变为Modified. 如果使用git rm移出版本库, 则成为Untracked文件

- Modified: 文件已修改, 仅仅是修改, 并没有进行其他的操作. 这个文件也有两个去处, 通过git add可进入暂存staged状态, 使用git checkout 则丢弃修改过, 返回到unmodify状态, 这个git checkout即从库中取出文件, 覆盖当前修改 !

- Staged: 暂存状态. 执行git commit则将修改同步到库中, 这时库中的文件和本地文件又变为一致, 文件为Unmodify状态. 执行git reset HEAD filename取消暂存, 文件状态为Modified  
  

## 查看文件状态  
`git status [filename]`或者`git status`

## 忽略文件
有些时候我们不想把某些文件纳入版本控制中，比如数据库文件，临时文件，设计文件等

在主目录下建立".gitignore"文件，此文件有如下规则：

1. 忽略文件中的空行或以井号（#）开始的行将会被忽略。

2. 可以使用Linux通配符。例如：星号（*）代表任意多个字符，问号（？）代表一个字符，方括号（[abc]）代表可选字符范围，大括号（{string1,string2,...}）代表可选的字符串等。

3. 如果名称的最前面有一个感叹号（!），表示例外规则，将不被忽略。

4. 如果名称的最前面是一个路径分隔符（/），表示要忽略的文件在此目录下，而子目录中的文件不忽略。

5. 如果名称的最后面是一个路径分隔符（/），表示要忽略的是此目录下该名称的子目录，而非文件（默认文件或目录都忽略）。
```
#为注释
*.txt        #忽略所有 .txt结尾的文件,这样的话上传就不会被选中！
!lib.txt     #但lib.txt除外
/temp        #仅忽略项目根目录下的TODO文件,不包括其它目录temp
build/       #忽略build/目录下的所有文件
doc/*.txt    #会忽略 doc/notes.txt 但不包括 doc/server/arch.txt
```
## SSH操作

1. 设置本机绑定SSH公钥，实现免密码登录！（免密码登录，这一步挺重要的，码云是远程仓库，我们是平时工作在本地仓库！)
2.   使用命令 ssh
```
# 进入 C:\Users\Administrator\.ssh 目录
# 生成公钥
ssh-keygen
```
生成两个文件分别是公钥和私钥  

3. 将公钥信息public key 添加到码云、GitHub账户中即可！  

## 远程仓库操作
1. 在GitHub上面创建远程仓库后，会提供一个链接（HTTPS、SSH）用来克隆到本地
2. 提供的链接太长了，可以创建一个别名
   - 用`git remote -v`查看有哪些别名
   - 用`git remote add [filename] [url]`创建别名
   - 我已经将blog添加为仓库别名

3. 用`git add .`把所有文件添加到暂存库
4. `git commit -m "message"`把文件提交到本地库
5. `git push blog master`把master分支同步到远程仓库，别名blog


## git文件操作
`git commit -m `"提交信息" 提交暂存区文件到本地仓库
`git commit`进行一次提交到本地仓库   
`git branch <name>`创建一个分支  
`git checkout <name>`切换到另一个分支  
`git checkout -b <name>`创建并切换到分支  