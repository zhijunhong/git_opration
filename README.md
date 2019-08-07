![Git](https://git-scm.com/images/logo@2x.png)

## Git常用命令和操作
### 1. 上传项目
1. 初始上传项目
```
*git init*
git remote add origin git@git.XXX.XXX.git
git add .
git commit -m "Initial commit"
git push -u origin master
```
2. 重新上传项目
```
git clone git@git.XXX.XXX.git
删除旧项目内容，拷贝新项目
git add .
git commit -m "commit"
git push origin
```
### 2. git打Tag操作
```
git tag -a 2.0.4 -m '创建TAG'
git push origin 2.0.4                   //将2.0.4标签提交到git服务器
git push origin --tag                   //提交所有tag至服务器
git tag -d 2.1.0                        //删除本地标签
git push origin :refs/tags/2.1.0        //删除远程标签
git push origin --delete tag <tagname>  //删除远程标签
```
### 3. 分支操作
1. 显示所有分支
```
git branch
```
2. 切换分支
```
git checkout master
```
3. 将develop分支merge到master分支
```
先将当前分支切换成master分支
git merge develop
```
4. 使用Git下载指定分支命令为
```
git clone -b special branch name git@git.XXX.XXX.git
```

### 4. git更换.gitignore文件
```
git rm -r --cached .                //将仓库中的index递归删除  
git add .                           //重新添加仓库索引
git commit -m 'update git.ignore'   //提交
``` 
### 5. git回滚操作
1. 方式一
```
git fetch --all
git reset --hard origin/develop
```
2. 方式二
[https://www.cnblogs.com/wancy86/p/5848024.html](https://www.cnblogs.com/wancy86/p/5848024.html)
