# git简介

# 时光机穿梭

# 远程仓库

# 分支管理

## 创建并切换分支

```js
//第一种
git checkout -b dev 或  git switch -c dev  //创建并切换分支
//第二种
git branch dev   //创建分支
git checkout dev  或  git switch master//切换分支
```

## 查看分支

```js
git branch  
```

## 合并分支

```js
1.切换到master分支
 git checkout master
 2.合并指定dev分支到当前分支
 git marge dev
 3.删除分支
  git branch -d dev
```

## 解决冲突

当 dev分支和master分支都有新的更改，会造成冲突，

解决冲突，再提交，不需要再次合并

```js
git marge dev  //可以告诉我们冲突的文件
git status//可以告诉我们冲突的文件
git log --graph --pretty=oneline --abbrev-commit   //可以看到分支的合并情况
```

## 禁用Fast forward

```js
git merge --no-ff -m "merge with no-ff" dev  //Git就会在merge时生成一个新的commit,合并后的历史有分支，能看出来曾经做过合并 
```

## bug分支

修复bug时，我们会通过创建新的bug分支进行修复，然后合并，最后删除；

当手头工作没有完成时，先把工作现场`git stash`一下，然后去修复bug，修复后，再`git stash pop`，回到工作现场；

你可以多次stash，恢复的时候，先用`git stash list`查看，然后恢复指定的stash，用命令：git stash apply stash@{0} 

```js
 1.git stash  //以把当前工作现场“储藏”起来，等以后恢复现场后继续工作
 2.git stash list   //查看工作现场
 3.恢复工作现场的两个方法
 //第一种
 一是用git stash apply恢复，但是恢复后，stash内容并不删除，你需要用git stash drop来删除；
 //第二种
 用git stash pop，恢复的同时把stash内容也删了
 4. git stash apply stash@{0}   //恢复指定的stash
```

在master分支上修复的bug，想要合并到当前dev分支，可以用`git cherry-pick <commit>`命令，把bug提交的修改“复制”到当前分支，避免重复劳动。

```js
git cherry-pick 4c805e2   //复制一个特定的提交到当前分支
```

## Feature分支

如果在Feature分支上进行了开发，结果不需要了，进行删除分支

```js
git branch -d feature-vulcan   //Git友情提醒，feature-vulcan分支还没有被合并，如果删除，将丢失掉修改 ,如果要强行删除，需要使用大写的-D参数。
git branch -D feature-vulcan   //强行删除分支
```

## 多人协作

多人协作的工作模式通常是这样：

1. 首先，可以试图用`git push origin <branch-name>`推送自己的修改；
2. 如果推送失败，则因为远程分支比你的本地更新，需要先用`git pull`试图合并；
3. 如果合并有冲突，则解决冲突，并在本地提交；
4. 没有冲突或者解决掉冲突后，再用`git push origin <branch-name>`推送就能成功！

如果`git pull`提示`no tracking information`，则说明本地分支和远程分支的链接关系没有创建，用命令`git branch --set-upstream-to <branch-name> origin/<branch-name>`。

这就是多人协作的工作模式，一旦熟悉了，就非常简单。

注意：

- 查看远程库信息，使用`git remote -v`；
- 本地新建的分支如果不推送到远程，对其他人就是不可见的；
- 从本地推送分支，使用`git push origin branch-name`，如果推送失败，先用`git pull`抓取远程的新提交；
- 在本地创建和远程分支对应的分支，使用`git checkout -b branch-name origin/branch-name`，本地和远程分支的名称最好一致；
- 建立本地分支和远程分支的关联，使用`git branch --set-upstream branch-name origin/branch-name`；
- 从远程抓取分支，使用`git pull`，如果有冲突，要先处理冲突。

常见的命令

```js
1.git remote -v     //查看远程库信息
2.推送分支
 (1)git push origin dev   //推送时，要指定本地分支,Git就会把该分支推送到远程库对应的远程分支上
 (2)并不是一定要把本地分支往远程推送，那么，哪些分支需要推送，哪些不需要呢？
    * master分支是主分支，因此要时刻与远程同步；
	* dev分支是开发分支，团队所有成员都需要在上面工作，所以也需要与远程同步；
	* bug分支只用于在本地修复bug，就没必要推到远程了，除非老板要看看你每周到底修复了几个bug；
    * feature分支是否推到远程，取决于你是否和你的小伙伴合作在上面开发。
 3.你的小伙伴要在dev分支上开发，就必须创建远程origin的dev分支到本地，于是他用这个命令创建本地dev分支
  git checkout -b dev origin/dev
```

## Rebase

- rebase操作可以把本地未push的分叉提交历史整理成直线；
- rebase的目的是使得我们在查看历史提交的变化时更容易，因为分叉的提交需要三方对比。

命令

```js
git rebase   //提交历史整理成直线
git log --graph --pretty=oneline --abbrev-commit   //查看提交记录
```

# 标签管理

## 创建标签

## 操作标签



