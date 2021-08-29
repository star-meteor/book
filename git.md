# 安装git      

[廖雪峰的官方网站](https://www.liaoxuefeng.com/wiki/896043488029600)

## 在Windows上安装Git

在Windows上使用Git，可以从Git官网直接[下载安装程序](https://git-scm.com/downloads)，然后按默认选项安装即可。

安装完成后，在开始菜单里找到“Git”->“Git Bash”，蹦出一个类似命令行窗口的东西，就说明Git安装成功！

![install-git-on-windows](https://www.liaoxuefeng.com/files/attachments/919018718363424/0)

安装完成后，还需要最后一步设置，在命令行输入：

```
$ git config --global user.name "Your Name"
$ git config --global user.email "email@example.com"
```

注意`git config`命令的`--global`参数，用了这个参数，表示你这台机器上所有的Git仓库都会使用这个配置，当然也可以对某个仓库指定不同的用户名和Email地址。

# 创建版本库

## 创建版本库

* 选择一个合适的地方，创建一个空目录

  ```js
  $ mkdir learngit
  $ cd learngit
  $ pwd    //显示当前目录
  /Users/michael/learngit
  ```

* 通过`git init`命令把这个目录变成Git可以管理的仓库

## 把文件添加到版本库

  所有的版本控制系统，其实只能跟踪文本文件的改动,而图片、视频这些二进制文件，虽然也能由版本控制系统管理，但没法跟踪文件的变化，只能把二进制文件每次改动串起来，也就是只知道图片从100KB改成了120KB，但到底改了啥，版本控制系统不知道，也没法知道

把一个文件放到Git仓库只需要两步。

第一步，用命令`git add`告诉Git，把文件添加到仓库：

```
$ git add readme.txt
```

执行上面的命令，没有任何显示，这就对了，Unix的哲学是“没有消息就是好消息”，说明添加成功。

第二步，用命令`git commit`告诉Git，把文件提交到仓库：

```
$ git commit -m "wrote a readme file"
[master (root-commit) eaadf4e] wrote a readme file
 1 file changed, 2 insertions(+)
 create mode 100644 readme.txt
```

简单解释一下`git commit`命令，`-m`后面输入的是本次提交的说明，可以输入任意内容，当然最好是有意义的，这样你就能从历史记录里方便地找到改动记录

# 时光机穿梭

## 版本回退

## 工作区和暂存区

## 管理修改

## 撤销修改

## 删除文件

# 远程仓库

## GitHub账户

### 注册gitHub账户

### SSH加密

由于你的本地Git仓库和GitHub仓库之间的传输是通过SSH加密的，所以，需要设置GitHub

第1步：创建SSH Key。在用户主目录下，看看有没有.ssh目录，如果有，再看看这个目录下有没有`id_rsa`和`id_rsa.pub`这两个文件，如果已经有了，可直接跳到下一步。如果没有，打开Shell（Windows下打开Git Bash），创建SSH Key：

```
$ ssh-keygen -t rsa -C "youremail@example.com"
```

你需要把邮件地址换成你自己的邮件地址，然后一路回车，使用默认值即可，由于这个Key也不是用于军事目的，所以也无需设置密码。

如果一切顺利的话，可以在用户主目录里找到`.ssh`目录，里面有`id_rsa`和`id_rsa.pub`两个文件，这两个就是SSH Key的秘钥对，`id_rsa`是私钥，不能泄露出去，`id_rsa.pub`是公钥，可以放心地告诉任何人。

第2步：登陆GitHub，打开“Account settings”，“SSH Keys”页面：

然后，点“Add SSH Key”，填上任意Title，在Key文本框里粘贴`id_rsa.pub`文件的内容：

![github-addkey-1](https://www.liaoxuefeng.com/files/attachments/919021379029408/0)

点“Add Key”，你就应该看到已经添加的Key：

![github-addkey-2](https://www.liaoxuefeng.com/files/attachments/919021395420160/0)

## 添加远程库

* 在GitHub创建一个Git仓库

* 关联一个远程库  `git remote add origin git@server-name:path/repo-name.git`
* 第一次把本地库的所有内容推送到远程库上 `git push -u origin master`
* 之后 git push origin master
* 删除远程库
  * `git remote -v`查看远程库信息：
  *  git remote rm origin    解除了本地和远程的绑定关系，并不是物理上删除了远程库。远程库本身并没有任何改动。
  * 要真正删除远程库，需要登录到GitHub，在后台页面找到删除按钮再删除。

## 从远程库克隆

* 命令`git clone`克隆一个本地库  `git clone git@github.com:michaelliao/gitskills.git`

  



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

* 首先，切换到要打标签的分支

* `git tag <name>`就可以打一个新标签

* `git tag`查看所有标签

* 忘记打标签

  * 找到历史提交的记录 

    `git log --pretty=oneline --abbrev-commit`

  * 指定commit Id 打标签

    `git tag v0.9 f52c633`

* 标签不是按时间顺序列出，而是按字母排序的。可以用`git show <tagname>`查看标签信息：

  `git show v0.9`

* 创建带有说明的标签，用`-a`指定标签名，`-m`指定说明文字

  `git tag -a v0.1 -m "version 0.1 released" 1094adb`

## 操作标签

* 删除标签

  * 删除本地标签

  `git tag -d v0.1`

  因为创建的标签都只存储在本地，不会自动推送到远程。所以，打错的标签可以在本地安全删除。

  * 删除远程标签

    * 先本地删除

    * 从远程删除。删除命令也是push

      git push origin :refs/tags/v0.9

* 推送标签到远程

  * 如果要推送某个标签到远程，使用命令`git push origin <tagname>`：git push origin v1.0

  * 一次性推送全部尚未推送到远程的本地标签

    git push origin --tags
