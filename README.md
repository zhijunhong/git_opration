# Git工作流程和常用命令分享

![Git](https://github.com/zhijunhong/git_opration/blob/master/art/1280px-Git-logo.svg.png?raw=true)

## 历史

git是一个分布式版本控制软件，最初由林纳斯·托瓦兹创作，于2005年以GPL发布。最初目的是为更好地管理Linux内核开发而设计。林纳斯·托瓦兹在编写第一个版本时就使用了“git”这个名称， 他将工具描述为“愚蠢的内容跟踪器”。

## Git和SVN使用的区别

| <span style="white-space:nowrap;">**&emsp;&emsp;差异&emsp;&emsp;**</span> | **svn**| **git**|
| :-------- | :------------------------------------------------------------ | :----------------------------------------------------------- |
| 系统特点 | 1.集中式版本控制系统（文档管理很方便）<br>2.克隆一个拥有将近一万个提交(commit),五个分支,每个分支有大约1500个文件，用时将近一个小时 | 1.分布式系统（代码管理很方便）<br>2.克隆一个拥有将近一万个提交(commit),五个分支,每个分支有大约1500个文件，用时1分钟 |
| 灵活性   | 1.搭载svn的服务器出现故障，无法与服务器进行交互 <br>2.所有的svn操作都需要中央仓库交互（例：拉分支，看日志等） | 1.可以单机操作，git服务器故障也可以在本地git仓库工作<br>2.除了push和pull（或fetch）操作，其他都可以在本地操作 <br>3.根据自己开发任务任意在本地创建分支 4.日志都是在本地查看，效率较高 |
| 安全性   | 较差，定期备份，并且是整个svn都得备份                        | 较高，每个开发者的本地就是一套完整版本库，记录着版本库的所有信息 |
| 分支方面 | 1.拉分支更像是copy一个路径 <br>2.可针对任何子目录进行branch <br>3.拉分支的时间较慢，因为拉分支相当于copy<br>4.创建完分支后，影响全部成员，每个人都会拥有这个分支 <br>5.多分支并行开发较重（工作较多而且繁琐） | 1.可以在Git的任意一个提交点开启新分支<br>2.拉分支时间较快，因为拉分支只是创建文件的指针和HEAD<br>3.自己本地创建的分支不会影响其他人 4.比较适合多分支并行开发 |
| 版本控制 | 1.保存前后变化的差异数据，作为版本控制 <br>2.版本号进行控制，每次操作都会产生一个高版本号（svn的全局版本号，这是svn一个较大的特点，git是hash值） | 1.git只关心文件数据的整体发生变化，更像是把文件做快照，文件没有改变时，分支指向这个文件的指针不会改变，文件发生改变，指针指向新版本 <br>2. 40 位长的哈希值作为版本号，没有先后之分 |
| 工作流程 | 1.每次更改文件之前都得update操作，有的时候修改过程中这个文件有更新，commit不会成功<br>2.有冲突，会打断提交动作 | 1.开始工作前进行fetch操作，完成开发工作后push操作，有冲突解决冲突<br>2.git的提交过程不会被打断，有冲突会标记冲突文件 <br>3.gitflow流程（经典） |
| 内容管理 | svn对中文支持好，操作简单，适用于大众                        | 对程序的源代码管理方便，代码库占用的空间少，易于分支化管理   |
| 权限管理 | svn的权限管理相当严格，可以按组、个人针对某个子目录的权限控制（每个目录下都会有个.svn的隐藏文件） | git没有严格的权限管理控制，只有账号角色划分（在项目的home文件下有且只有一个.git目录） |

## Git工作流程

![3985563-ade5b67f52f8675c](https://github.com/zhijunhong/git_opration/blob/master/art/3985563-ade5b67f52f8675c.png?raw=true)

**四个专有名词：**

Workspace：工作区

Index / Stage：暂存区

Repository：仓库区（或本地仓库）

Remote：远程仓库

| <span style="white-space:nowrap;">**关键词**</span> | **解释**                                                     |
| :-------------------------------------------------: | :----------------------------------------------------------- |
|                     **工作区**                      | 程序员进行开发改动的地方，是你当前看到的，也是最新的。 平常我们开发就是拷贝远程仓库中的一个分支，基于该分支进行开发。在开发过程中就是对工作区的操作。 |
|                     **暂存区**                      | .git目录下的index文件, 暂存区会记录git add添加文件的相关信息(文件名、大小、timestamp...) 。可以使用**git** **status**查看暂存区的状态。暂存区标记了你当前工作区中，哪些内容是被git管理的。 |
|                    **本地仓库**                     | 保存了对象被提交过的各个版本，比起工作区和暂存区的内容，它要更旧一些。 git commit后同步目录树到本地仓库，方便下一步通过git push同步本地仓库与远程仓库。 |
|                    **远程仓库**                     | 远程仓库的内容可能被分布在多个地点的处于协作关系的本地仓库进行修改，因此它可能与本地仓库同步，也可能不同步，但是它的内容是最旧的。 |

## Git常用命令

![3985563-6b745d5fac15906c](https://github.com/zhijunhong/git_opration/blob/master/art/3985563-6b745d5fac15906c.png?raw=true)

### Git常用命令速查表

![3985563-c7f05348b711ebbe](https://github.com/zhijunhong/git_opration/blob/master/art/1801651-33d5c72002486bbb.png?raw=true)



### 初始化仓库

| **命令**        | **解释**                         |
| --------------- | -------------------------------- |
| git clone <url> | #克隆远程版本库,生成.git隐藏文件 |

打开本地生成的.git隐藏文件

| 文件夹  | 解释                                                   |
| ------- | ------------------------------------------------------ |
| hooks   | 存储钩子的文件夹                                       |
| logs    | 存储日志的文件夹                                       |
| refs    | 存储指向各个分支的指针（SHA-1标识）文件                |
| objects | 存放git对象                                            |
| config  | 存放各种设置文档                                       |
| HEAD    | 指向当前所在分支的指针文件路径，一般指向refs下的某文件 |

### 创建和添加

创建新项目gittest

创建新文件test.txt

git add <file>

git status显示有变更的文件

git restore <file> **撤回文件修改内容**

git commit –m “注释”

修改内容-> 执行git diff工作区和本地仓库的差异

git log显示当前分支的版本历史

### 版本回退

git reset  --hard HEAD^ 当前版本回退到上一个版本

git reset  --hard HEAD^ ^ 当前版本回退到上上一个版本

git reset  --hard HEAD~100 回退到前100个版本

恢复已经删除的版本

git reflog 展示所有的提交记录

git reset --hard <版本号> 回退到指定版本

### 推送至远程分支

git push origin master 将本地master分支推送到远程master分支，相当于创建远程分支

### 创建与合并分支

git checkout -b dev = git branch dev + git checkout dev 创建并切换分支

git branch 不带参数，会列出所有本地的分支；带参数表示创建分支

git branch –d name 删除本地分支(-D表示强制删除）

git branch –r 不带参数，会列出所有远程的分支

git branch --set-upstream-to=origin/<branch本地> 本地和远程分支关联

git push origin –delete <branch> 删除远程分支

### 合并分支

git merge release用于合并指定分支到当前分支上

注：Fast-forward表示的合并是“快进模式”，也就是直接把master指向dev的当前提交，所以合并速度非常快。在这种模式下，删除分支后，会丢掉分支日志信息。可以使用带参数 --no-ff来禁用”Fast forward”模式。

git merge --no-ff  -m “注释”dev

### 解决冲突

git checkout release 切换release分支

vim test.txt 修改某条内容

git commit test.txt -m “release修改某条内容”

git checkout master 切换master分支

vim test.txt 修改某条同release内容

git commit test.txt -m “master修改某条内容”

git merge release 显示冲突

git status 显示冲突提示

Git用<<<<<<<，=======，>>>>>>>标记出不同分支的内容，其中>>>>release 是指release上修改的内容
vim test.txt 修改内容

git add test.txt

git commit -a -m “fix conflict”

### 暂储stash功能

当前分支有没有提交但也不合适现在就提交的内容，Git提供了暂储功能stash

#### 1.产生场景

git checkout release

vim test.txt 修改test.txt内容

git checkout develop 此时会提示Aborting

#### 2.解决方式

```xml
Please commit your changes or stash them before you switch branches
git stash
```

git status 查看当前状态

Git stash list 查看所有暂储列表

#### 3.还原暂储

git stash apply恢复，恢复后stash内容并不删除，你需要使用命令git stash drop来删除；
另一种方式是使用git stash pop,恢复的同时把stash内容也删除了

### Git Tag功能

创建Git Tag并推送远程服务器

git tag -a V1.0.0 –m“注释” 							//创建TAG

git push origin V1.0.0               					//推送到远程服务器

git push origin --tag               	   				//提交所有tag至服务器

git tag -d V1.0.0                             				//删除本地标签

git push origin --delete tag <tagname>    //删除远程标签

## HEAD的理解

HEAD，它始终指向当前所处分支的最新的提交点。你所处的分支变化了，或者产生了新的提交点，HEAD就会跟着改变

![3985563-623d3cefdcb95045](https://github.com/zhijunhong/git_opration/blob/master/art/3985563-623d3cefdcb95045.png?raw=true)



## Add的理解

add相关命令很简单，主要实现将工作区修改的内容提交到暂存区，交由git管理。

git add .添加当前目录的所有文件到暂存区

git add 添加指定目录到暂存区，包括子目录

git add 添加指定文件到暂存区

![3985563-a5f92bd6f800959f](https://github.com/zhijunhong/git_opration/blob/master/art/3985563-a5f92bd6f800959f.png?raw=true)



## Commit的理解

commit相关命令也很简单，主要实现将暂存区的内容提交到本地仓库，并使得当前分支的HEAD向后移动一个提交点。

git commit -m 提交暂存区到本地仓库,message代表说明信息

git commit --amend -m 使用一次新的commit，替代上一次提交

![3985563-a5f92bd6f800959f](https://github.com/zhijunhong/git_opration/blob/master/art/3985563-a5f92bd6f800959f.png?raw=true)



## Push的理解

上传本地仓库分支到远程仓库分支，实现同步。

git push 上传本地指定分支到远程仓库

git push --force强行推送当前分支到远程仓库，即使有冲突

git push --all推送所有分支到远程仓库

## Branch的理解

关于分支，大概有展示分支，切换分支，创建分支，删除分支这四种操作。

git branch列出所有本地分支

git branch -r列出所有远程分支

git branch -a列出所有本地分支和远程分支

git branch 新建一个分支，但依然停留在当前分支

git checkout -b 新建一个分支，并切换到该分支

git checkout 切换到指定分支，并更新工作区

git branch -d 删除分支

git push origin --delete 删除远程分支

关于分支的操作虽然比较多，但都比较简单好记

![3985563-04bac8d079111a9f](https://github.com/zhijunhong/git_opration/blob/master/art/3985563-04bac8d079111a9f.png?raw=true)



## Merge的理解

merge命令把不同的分支合并起来。在实际开放中，我们可能从master分支中切出一个分支，然后进行开发完成需求，中间经过R3,R4,R5的commit记录，最后开发完成需要合入master中，这便用到了merge。

git merge 合并指定分支到当前分支

注：如果在merge之后，出现conflict，主要是因为两个用户修改了同一文件的同一块区域。需要针对冲突情况，手动解除冲突。

![3985563-29417c3862d0599c](https://github.com/zhijunhong/git_opration/blob/master/art/3985563-29417c3862d0599c.png?raw=true)



## Rebase的理解

rebase又称为衍合，是合并的另外一种选择。

在开始阶段，我们处于new分支上，执行git rebase dev，那么new分支上新的commit都在dev分支上重演一遍，最后checkout切换回到new分支。这一点与merge是一样的，合并前后所处的分支并没有改变。

git rebase dev，通俗的解释就是new分支想站在dev的肩膀上继续下去。

rebase操作不会生成新的节点，是将两个分支融合成一个线性的提交。

rebase也需要手动解决冲突。

![3985563-8d4e5fc624c0a23b](https://github.com/zhijunhong/git_opration/blob/master/art/3985563-8d4e5fc624c0a23b.png?raw=true)



## Merge和Rebase的比较

1.如果你想要一个干净的，没有merge commit的线性历史树，那么你应该选择git rebase

2.如果你想保留完整的历史记录，并且想要避免重写commit history的风险，你应该选择使用git merge

## Reset的理解

reset命令把当前分支指向另一个位置，并且相应的变动工作区和暂存区。

git reset —soft 只改变提交点，暂存区和工作目录的内容都不改变

git reset —mixed 改变提交点，同时改变暂存区的内容

git reset —hard 暂存区、工作区的内容都会被修改到与提交点完全一致的状态

![3985563-2d41240c43bc3f2e](https://github.com/zhijunhong/git_opration/blob/master/art/3985563-2d41240c43bc3f2e.png?raw=true)

## Revert的理解

git revert用一个新提交来消除一个历史提交所做的任何修改。

![3985563-02aab40cb9b6efb1](https://github.com/zhijunhong/git_opration/blob/master/art/3985563-02aab40cb9b6efb1.jpeg?raw=true)

## Revert与Reset的区别

在回滚这一操作上看，效果差不多。git revert是用一次新的commit来回滚之前的commit，git reset是直接删除指定的commit。

![3985563-93d402b6ebda56f8](https://github.com/zhijunhong/git_opration/blob/master/art/3985563-93d402b6ebda56f8.jpeg?raw=true)

## Gitignore 忽略

### 1.创建gitignore文件

在 Git工作区的根目录创建一个特殊的.gitignore文件。

在.gitignore文件中，添加需要忽略的文件。

### 2.更新gitignore文件

git rm -r --cached .          	//将仓库中的index递归删除

git add .                           //重新添加仓库索引

git commit -m “update git.ignore” //提交

git branch --set-upstream-to=origin/<branch> <branch> //重现将本地仓库和远程仓库关联

## 常用Git建立分支结构

![202104201](https://github.com/zhijunhong/git_opration/blob/master/art/202104201.png?raw=true)