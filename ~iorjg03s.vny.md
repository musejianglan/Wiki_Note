## git 流程  
初始化一个Git仓库，使用git init命令。  
添加文件到Git仓库，分两步：  
第一步，使用命令git add <file>，注意，可反复多次使用，添加多个文件；  
第二步，使用命令git commit，完成。  
要随时掌握工作区的状态，使用git status命令。  
如果git status告诉你有文件被修改过，用git diff可以查看修改内容。
HEAD指向的版本就是当前版本，因此，Git允许我们在版本的历史之间穿梭，使用命令git remote --hard commit_id。  
穿梭前，用git log可以查看提交历史，以便确定要回退到哪个版本。  
要重返未来，用git reflog查看命令历史，以便确定要回到未来的哪个版本。  
撤销修改：  
1. 当你改乱了工作区某个文件的内容，想直接丢弃工作区的修改时，用命令git checkout -- file。  
2. 当你不但改乱了工作区某个文件的内容，还添加到了暂存区时，想丢弃修改，分两步，第一步用命令git reset HEAD file，就回到了场景1，第二步按场景1操作。  
3. 已经提交了不合适的修改到版本库时，想要撤销本次提交，参考版本回退一节，不过前提是没有推送到远程库。

## 基本命令

#### 设置用户名 邮箱 (第一次安装git后) 
```
$ git config --global user.name "Your Name"
$ git config --global user.email "email@example.com"
```  

因为Git是分布式版本控制系统，所以，每个机器都必须自报家门：你的名字和Email地址。你也许会担心，如果有人故意冒充别人怎么办？这个不必担心，首先我们相信大家都是善良无知的群众，其次，真的有冒充的也是有办法可查的。  

*注意git config命令的--global参数，用了这个参数，表示你这台机器上所有的Git仓库都会使用这个配置，当然也可以对某个仓库指定不同的用户名和Email地址。*

### 创建新仓库
#### git init  
代表初始化 git 仓库  

#### git status  
查看你当前 git 仓库的一些状态  

### 检出仓库
#### git clone /path/to/repository
创建一个本地仓库的克隆版本

#### git clone username@host:/path/to/repository
克隆远端服务器上的仓库  
git clone git@github.com:musejianglan/Wiki_Note.git


### 添加和提交
#### git add file_name  
操作你想要提交的文件  

#### git add *
新增所有修改或者新建的文件

#### git add -A
新增所有修改或者新建的文件，包括删除的文件

#### git add -f App.class
App.class被忽略无法添加，使用该方法强制添加

#### git commit  
git commit -m 'first commit':commit 是提交的意思，-m 代表是提交信息，执行了以上命令代表我们已经正式进行了第一次提交。  

### git log
#### git log  
git log 命令可以查看所有产生的 commit 记录  

#### git log --author=username
某一个人的提交记录

#### git log --pretty=oneline
一个压缩后的每一条提交记录只占一行的输出

#### git log --graph --oneline --decorate --all
通过 ASCII 艺术的树形结构来展示所有的分支, 每个分支都标示了他的名字和标签  

#### git reflog  
用来记录你的每一次命令

#### git log --graph
命令可以看到分支合并图


### branch分支
#### git branch  
查看下当前分支情况  

##### git branch branch_name  
就新建了一个名字叫 branch_name 的分支。这时候查看分支还是显示master主分支。  


#### git branch -d branch_name
删除分支，执行 git branch -d branch_name 就可以把a分支删除了。  

#### git branch -D branch_name
强制删除branch_name分支。有些时候可能会删除失败，比如如果a分支的代码还没有合并到master，你执行 git branch -d branch_name 是删除不了的，它会智能的提示你branch_name分支还有未合并的代码，但是如果你非要删除，那就执行 git branch -D branch_name 就可以强制删除branch_name分支。  

#### git push origin branch_name
将分支推送到远端仓库，不然该分支就是 不为他人所见的

### 替换和改动

#### git checkout -- filename
替换掉本地改动  
此命令会使用 HEAD 中的最新内容替换掉你的工作目录中的文件。已添加到暂存区的改动以及新文件都不会受到影响  

#### git fetch origin   git reset --hard origin/master
假如你想丢弃你在本地的所有改动与提交，可以到服务器上获取最新的版本历史，并将你本地主分支指向它

#### git checkout branch_name  
切换到分支a  

##### git checkout -b branch_name  
新建一个a分支，并且自动切换到a分支。

#### git rm file_name  git commit
命令git rm删掉file_name文件，并且git commit

#### 合并

#### git merge branch_name
合并某分支到当前分支  
代码合并到主分支master上。git merge 就是合并分支用到的命令，针对这个情况，需要先做两步，第一步是切换到 master 分支，如果你已经在了就不用切换了，第二步执行 git merge branch_name ，意思就是把branch_name分支的代码合并过来。  

#### git merge --no-ff -m "merge with no-ff" branch_name
--no-ff参数，表示禁用Fast forward  
本次合并要创建一个新的commit，所以加上-m参数，把commit描述写进去  

### stash
#### git stash
可以把当前工作现场“储藏”起来，等以后恢复现场后继续工作

#### git stash list
用git stash list命令看看“储藏”列表

#### git stash apply
恢复stash，但是恢复后，stash内容并不删除，你需要用git stash drop来删除；  

#### git stash drop
删除stash

#### git stash pop
恢复的同时把stash内容也删了 

### git tag
#### git tag

我们在客户端开发的时候经常有版本的概念，比如v1.0、v1.1之类的，不同的版本肯定对应不同的代码，所以我一般要给我们的代码加上标签，这样假设v1.1版本出了一个新bug，但是又不晓得v1.0是不是有这个bug，有了标签就可以顺利切换到v1.0的代码，重新打个包测试了。

所以如果想要新建一个标签很简单，比如 git tag v1.0 就代表我在当前代码状态下新建了一个v1.0的标签，输入 git tag 可以查看历史 tag 记录。  

#### git tag tag_name commit_id
将提交的有一次打上标签

#### git diff  
顾名思义就是查看difference，显示的格式正是Unix通用的diff格式。

### reset
#### git reset  
git reset --hard HEAD^：首先，Git必须知道当前版本是哪个版本，在Git中，用HEAD表示当前版本，也就是最新的提交3628164...882e1e0），上一个版本就是HEAD^，上上一个版本就是HEAD^^，当然往上100个版本写100个^比较容易数不过来，所以写成HEAD~100。  
找到最新commit id是3628164...，于是就可以指定回到未来的某个版本：
`git reset --hard 3628164`版本号没必要写全，前几位就可以了，Git会自动去找。当然也不能只写前一两位，因为Git可能会找到多个版本号。  

#### git reset --hard HEAD^
版本回退  
上一个版本就是HEAD^，上上一个版本就是HEAD^^，当然往上100个版本写100个^比较容易数不过来，所以写成HEAD~10  

#### git reset --hard commit_id
版本的历史之间穿梭

### 撤销修改  
#### git checkout -- <file>  
可以丢弃工作区的修改  

#### git reset HEAD <file>
可以把暂存区的修改撤销掉（unstage），重新放回工作区,然后git checkout -- <file>；


## 远程库（github为例）

1. 创建SSH Key。在用户主目录下，看看有没有.ssh目录，如果有，再看看这个目录下有没有id_rsa和id_rsa.pub这两个文件，如果已经有了，可直接跳到下一步。如果没有，打开Shell（Windows下打开Git Bash），创建SSH Key：
`ssh-keygen -t rsa -C "musejianglan@163.com"`  
2. 登陆GitHub，打开“Account settings”，“SSH Keys”页面：然后，点“Add SSH Key”，填上任意Title，在Key文本框里粘贴id_rsa.pub文件的内容：

#### git remote
查看远程库的信息

#### git remote -v
显示更详细的信息

#### git remote add origin server_name
git remote add origin git@github.com:musejianglan/Wiki_Note.git  
把一个已有的本地仓库与远程仓库关联，然后，把本地仓库的内容推送到GitHub仓库

#### git clone username@host:/path/to/repository
克隆远端服务器上的仓库  
git clone git@github.com:musejianglan/Wiki_Note.git

### 推送改动

#### git push -u origin master
第一次推送master分支的所有内容

#### git push origin master
推送naster分支最新修改

#### git pull
更新你的本地仓库至中心仓库的最新改动


#### git checkout -b branch-name origin/branch-name
在本地创建和远程分支对应的分支，在本地创建和远程分支对应的分支

#### git branch --set-upstream branch-name origin/branch-name
建立本地分支和远程分支的关联

### 自定义git

#### git config --global color.ui true
让Git显示颜色，会让命令输出看起来更醒目


#### 忽略特殊文件

[忽略模板](https://github.com/github/gitignore)

#### git check-ignore

#### 配置别名
#### git config --global alias.st status
告诉Git，以后st就表示status


### 搭建Git服务器

1. 搭建Git服务器需要准备一台运行Linux的机器，强烈推荐用Ubuntu或Debian，这样，通过几条简单的apt命令就可以完成安装
2. `$ sudo apt-get install git`   安装git
3. `$ sudo adduser git`  创建一个git用户，用来运行git服务
4. 创建证书登录,收集所有需要登录的用户的公钥，就是他们自己的id_rsa.pub文件，把所有公钥导入到/home/git/.ssh/authorized_keys文件里，一行一个
5. 初始化Git仓库;先选定一个目录作为Git仓库，假定是/srv/sample.git，在/srv目录下输入命令：`$ sudo git init --bare sample.git`;Git就会创建一个裸仓库，裸仓库没有工作区，因为服务器上的Git仓库纯粹是为了共享，所以不让用户直接登录到服务器上去改工作区，并且服务器上的Git仓库通常都以.git结尾。然后，把owner改为git:`$ sudo chown -R git:git sample.git`;
6. 禁用shell登录;出于安全考虑，第二步创建的git用户不允许登录shell，这可以通过编辑/etc/passwd文件完成。找到类似下面的一行：`git:x:1001:1001:,,,:/home/git:/bin/bash`改为：`git:x:1001:1001:,,,:/home/git:/usr/bin/git-shell`这样，git用户可以正常通过ssh使用git，但无法登录shell，因为我们为git用户指定的git-shell每次一登录就自动退出
7. git clone git@server:/srv/sample.git


---
```
These are common Git commands used in various situations:

start a working area (see also: git help tutorial)
   clone      Clone a repository into a new directory
   init       Create an empty Git repository or reinitialize an existing one

work on the current change (see also: git help everyday)
   add        Add file contents to the index
   mv         Move or rename a file, a directory, or a symlink
   reset      Reset current HEAD to the specified state
   rm         Remove files from the working tree and from the index

examine the history and state (see also: git help revisions)
   bisect     Use binary search to find the commit that introduced a bug
   grep       Print lines matching a pattern
   log        Show commit logs
   show       Show various types of objects
   status     Show the working tree status

grow, mark and tweak your common history
   branch     List, create, or delete branches
   checkout   Switch branches or restore working tree files
   commit     Record changes to the repository
   diff       Show changes between commits, commit and working tree, etc
   merge      Join two or more development histories together
   rebase     Reapply commits on top of another base tip
   tag        Create, list, delete or verify a tag object signed with GPG

collaborate (see also: git help workflows)
   fetch      Download objects and refs from another repository
   pull       Fetch from and integrate with another repository or a local branch
   push       Update remote refs along with associated objects

'git help -a' and 'git help -g' list available subcommands and some
concept guides. See 'git help <command>' or 'git help <concept>'
to read about a specific subcommand or concept.
```

