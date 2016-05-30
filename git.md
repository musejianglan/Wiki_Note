## git 流程  
初始化一个Git仓库，使用git init命令。  
添加文件到Git仓库，分两步：  
第一步，使用命令git add <file>，注意，可反复多次使用，添加多个文件；  
第二步，使用命令git commit，完成。  
要随时掌握工作区的状态，使用git status命令。  
如果git status告诉你有文件被修改过，用git diff可以查看修改内容。

## 基本命令

#### 设置用户名 邮箱  
```
$ git config --global user.name "Your Name"
$ git config --global user.email "email@example.com"
```  

因为Git是分布式版本控制系统，所以，每个机器都必须自报家门：你的名字和Email地址。你也许会担心，如果有人故意冒充别人怎么办？这个不必担心，首先我们相信大家都是善良无知的群众，其次，真的有冒充的也是有办法可查的。  

*注意git config命令的--global参数，用了这个参数，表示你这台机器上所有的Git仓库都会使用这个配置，当然也可以对某个仓库指定不同的用户名和Email地址。*

#### git init  
代表初始化 git 仓库  

#### git status  
查看你当前 git 仓库的一些状态  

#### git add <file>  
操作你想要提交的文件  

#### git commit  
git commit -m 'first commit':commit 是提交的意思，-m 代表是提交信息，执行了以上命令代表我们已经正式进行了第一次提交。  

#### git log  
git log 命令可以查看所有产生的 commit 记录  

#### git branch  
查看下当前分支情况  

##### git branch a（分支名）  
就新建了一个名字叫 a 的分支。这时候查看分支还是显示master主分支。  

#### git checkout a（分支名）  
切换到分支a  

##### git checkout -b a  
新建一个a分支，并且自动切换到a分支。  

#### git merge a（分支名）
代码合并到主分支master上。git merge 就是合并分支用到的命令，针对这个情况，需要先做两步，第一步是切换到 master 分支，如果你已经在了就不用切换了，第二步执行 git merge a ，意思就是把a分支的代码合并过来。  

#### git branch -d a（分支名）
删除分支，执行 git branch -d a 就可以把a分支删除了。  

#### git branch -D
强制删除a分支。有些时候可能会删除失败，比如如果a分支的代码还没有合并到master，你执行 git branch -d a 是删除不了的，它会智能的提示你a分支还有未合并的代码，但是如果你非要删除，那就执行 git branch -D a 就可以强制删除a分支。  

#### git tag

我们在客户端开发的时候经常有版本的概念，比如v1.0、v1.1之类的，不同的版本肯定对应不同的代码，所以我一般要给我们的代码加上标签，这样假设v1.1版本出了一个新bug，但是又不晓得v1.0是不是有这个bug，有了标签就可以顺利切换到v1.0的代码，重新打个包测试了。

所以如果想要新建一个标签很简单，比如 git tag v1.0 就代表我在当前代码状态下新建了一个v1.0的标签，输入 git tag 可以查看历史 tag 记录。  

#### git diff  
顾名思义就是查看difference，显示的格式正是Unix通用的diff格式。
