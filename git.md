# 1.git常用命令

## 1.1 设置用户签名

```bash
git config --global user.name 用户名    #设置用户签名

git config --global user.email 邮箱     #设置用户签名
```

签名的作用是为了区分不同操作者身份，git首次安装必须设置用户签名，否则无法提交代码



## 1.2 初始化本地库

在要创建git仓库的文件夹路径下

```c++
git init
```



## 1.3 查看本地库状态

```c++
git status
```



## 1.4 添加暂存区

```c++
git add 文件名
git add . #可以将所有文件加入暂存区
```

**移除暂存区**，但是文件本身没有被删除

```c++
git rm --cached 文件名
```

**从暂存区删除，以及从本地文件夹也删除**

```c++
git rm 文件名
```



## 1.5 提交本地库

会创建版本号

```c++
git commit -m "日志信息" 文件名
```





## 1.6 历史版本

### 1.6.1 查看历史版本

```c++
git reflog #查看版本信息
git log #查看版本详细信息 
```

git log显示的版本号是完整的版本号，git reflog显示的是前7位

### 1.6.2 版本穿梭

```c++
git reset --hard 版本号 #这里的版本号用的是git reflog里查看到的版本号
```

**本质上是head的头指针变化**



## 1.7 撤销修改

### 1.7.1 撤销某个提交

```c++
git revert  版本号
```

git 会生成一个新的提交，效果是撤回了之前的某个提交

#### 将某个文件撤销到某个版本

**假如这个文件已经被add过 需要多加一步，将文件移除暂存区**

```c++
git restore --staged 文件名
```



**将某个文件撤销回某个版本**

```c++
git restore 文件名 #切换该文件为head指向的版本的文件
git restore --source 版本号 文件名 #HEAD可代指版本号表示当前head指针指向的版本
```



## 1.8 看差异

```c++
git diff #看工作区和暂存区的差异
git diff --staged #看暂存区和最近一次提交的差异
git diff 文件名 #看某个文件的差异
git diff 版本号1 版本号2 #比较两次提交
    
```



## 1.9 暂存

当前分支的代码还没add要去其他分支处理

```c++
git stash #暂存当前修改
git stash push -m "login page half done" #带说明的暂存
```

### **1.9.1 查看stash列表**

```c++
git stash list 
输出可能是
stash@{0}: On feature/login: login page half done
stash@{1}: On main: fix typo
```

### 1.9.2删除恢复stash

  

```c++
git stash apply #恢复最近一次stash，只恢复不删除stash记录
git stash pop #恢复并删除最近一次stash
git stash apply stash@{1} #恢复指定stash
git stash drop stash@{1} #删除某个stash
git stash clear 清空所有的stash
```



## 1.10 打标签

```c++
git tag 标签信息
git tag -a 
```



# 2.git 分支操作



## 2.1查看分支

```c++
git branch -v
git branch -a 查看所有分支，包括本地分支和远程分支
```



## 2.2 创建分支

```c++
git branch 路径名
```



## 2.3 切换分支

```c++
git switch 分支名 #切换到已有分支
git switch -c 分支名 #创建并切换到新分支
```



## 2.4 合并分支

```c++
git merge 分支名
```

```c++
git rebase 分支名 #和merge不同的是
假如现在是D版本，C分支是在B版本建立的 merge会把C接在B上就保持真实分叉的记录
rebase会把C直接接到D上，相当于把一棵树变成链了
```



###  合并冲突

合并分支时，两个分支在同一个文件的同一个位置，有两套完全不同的修改，必须人为决定新代码内容

此时打开冲突文件会出现这种 

```c++
<<<<<<< HEAD
master #这里是当前在的分支名的内容
=======
111 #这里是要被合并分支名的内容
>>>>>>> 1

```

**解决方法：手动的在当前的分支里修改要的内容，比如我master这一行和1这一行都要，那么把剩下三行都删了，然后重新add commit 此时commit不能加文件名**





# 3.远程仓库操作



## 3.1 创建远程仓库别名

**查看当前所有远程地址别名**

```c++
git remote -v
```



**给远程仓库起别名**

```c++
git remote add 别名 远程地址
```



## 3.2 推送本地分支到远程仓库

```c++
git push 别名 分支名 
git push -u 别名 分支名 #git会记忆别名和分支名 下次就直接git push和git pull
```



## 3.3 拉取远程库到本地库

```c++
git pull 别名 分支名
git fetch #把远程仓库哦的最新信息拉到本地，但不自动合并
```

git pull=git fetch +git merge

## 3.4 克隆远程仓库到本地

```c++
git clone 远程库链接
```

**拉取代码的同时会自动初始化仓库和创建别名（origin）**





# 4 .gitignore

**哪些文件不要被纳入版本控制**

在git仓库这个文件夹下创建一个.gitignore 的文件，里面写

```c++
node_modules/ #忽略整个目录
.env #忽略某个文件
*.log #忽略.log结尾的文件
```

