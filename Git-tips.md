#  Git tips :rocket: 

####   1. Git配置                

**Git 配置**

  Git 提供一个git config 的工具，专门用来配置或读取相应的工作环境变量。这些环境变量，决定了Git在各个环节的具体工作方式和行为。这些变量可以存放在一下三个不同的地方：

  - ``/etc/gitconfig`` 文件：系统中对所有用户普遍适用的配置。使用``git config --system <verb>`` 更改系统git配置
  - ``~/.gitconfig`` 文件： 用户目录下的配置文件只适用于该用户。使用``git config --global <verb>``更改当前用户下git配置
  - 当前项目的Git目录中的配置文件（即工作目录中.git/config文件）：只对当前项目有效。每一个级别的配置会覆盖上层的相同配置。所以 ``.git/config`` 里的配置文件会覆盖``/ect/config`` 中的同名变量 

**用户信息**

配置个人用户名和邮箱

```git
git config --global user.name "username"
git config --global user.email "username@xxx.com"
```
查看配置文件 

```
vim ~/.gitconfig
```

**文本编辑器**

配置文本编辑器

```
git config --global core.editor vim
```

**查看配置信息**

检查已有配置信息

```
git config --list
```

其中重复变量名代表它们来自不同的配置文件，不过Git实际采用的是最后一个
这些配置可以再``~/.gitconfig`` 或 `` /etc/gifconfig`` 看到

```
vim ~/.gitconfig
```

也可以直接查阅某个环境变量设定，例如：
```git
git config user.name
```


#### 2. 将本地非空目录转化为Git仓库 

1. 将本地项目文件初始化为git版本库

```
git init
```

2. 将本地项目文件添加到版本库

```
git add .
```

3. 拍摄项目快照。*-m* 标志让Git将接下来的信息 *message* 记录到项目的历史记录中

```
git commit -m 'message'
```

4. 在github中新建一同名仓库
5. 给本地版本库设置远程仓库

```
git remote add origin <url>
```
6. 查看结果（可选）

```
git remote -v
```
7. 将本地版本库推送到git上

```
git push origin master
```

#### 3. 忽略文件 

将无需纳入Git管理的文件添加到创建的``.gitignore``的忽略文件中，列出要忽略文件的模式。

文件``.gitignore``的格式规范如下：
* 所有空行或者以``#``开头的行都会被Git忽略；
* 可以使用标准的**glob模式**匹配，它会地柜地应用到整个工作区中；
* 匹配模式可以以 `(/)` 开头防止递归；
* 匹配模式可以以 `(/)`结尾指定目录；
* 要忽略指定模式以外的文件或目录，可以在模式前加上叹号`(!)`取反。

所谓的**glob模式**是指shell所使用的简化了的正则表达式。星号 ``(*)`` 匹配零个或多个任意字符；[abc] 匹配任何一个列在方括号中的字符；问号 ``(?)``只匹配一个任意字符；如果方括号中使用短划线分隔两个字符，表示所有在这两个字符范围内的都可以匹配（比如[0-9]表示匹配所有0-9的数据）。使用两个星号（**）表示匹配任意中间目录。  

#### 4. 分支管理 

使用分支意味着你可以从开发主线上分离开来，在不影响主线的同时继续工作。Git 分支，其本质仅仅是指向提交对象的可变指针。

**创建``dev``分支**

``` git
git branch dev
```

> 创建分支实际上只是为你创建了一个可以移动的新的指针。

**切换到 ``dev`` 分支** 

``` git
git checkout dev
```
在git 2.23版本之后可以使用switch命令进行分支切换
```
git switch master
```
或者``git checkout`` 命令加上 ``-b``参数表示创建并切换
``` git
git checkout -b dev
```
或者
```
git switch -c dev
```
**查看当前分支 **

```
git branch
```
**在当前分支操作并提交**

**``dev`` 分支工作完成后，切换回``master``主分支 **

```
git checkout master
```
**将``dev``分支上内容合并到主分支``master`` ** 

```
git merge dev
```
合并分支时Git一般默认会用``Fast forward ``模式，但是此模式下，删除分支后，会丢掉分支信息。因此，可以选择禁用``Fast forward`` 模式，Git就会在merge时生成一个新的commit，这样，从分支历史上就可以看出分支信息。

```
git merge --no-ff -m 'merge with no-ff' dev
```

> ``git merge`` 命令用于合并指定分支到当前分支

**删除分支**

```
git branch -d dev
```

**查看分支合并图**

```
git log --graph
```

**复制特定提交到当前分支**

```
git cherry-pick [commit_id]
```

**强行删除没有合并过的分支**

```
git branch -D <branch_name>
```

**从远程抓取分支**

```
git pull
```

**在本地创建和远程对应的分支，本地和远程分支名称最好一致**

```
git checkout -b branch_name origin/branch_name
```

**关联本地分支和远程分支**

```
git branchn --set-upstrem branch_name origin/branch_name
```

##### Bug 分支(使用git stash命令保存和恢复进度)

我们有时会遇到这样的情况，正在dev分支开发新功能，做到一半有人过来反馈一个bug，让马上解决，但是新功能做到一半又不想提交，这时就可以使用``git stash``命令先把当前进度保存起来，然后切换到另一个分支去修改bug，修改完提交后，再切回dev分支，使用``git stash pop`` 来恢复之前的进度继续开发新功能。

* 保存当前进度

  ```
  git stash 
  git stash save 'message' # 添加注释
  ```

* 显示保存进度列表

  ```
  git stash list
  ```

* 恢复最新进度到工作区

  ```
  git stash apply [stash_id] 
  git stash pop [stash_id]  # 通过此命令恢复后，会删除当前进度
  ```

* 删除一个存储的进度

  ```
  git stash drop [stash_id]
  git stash clear  # 删除所有存储的进度
  ```

#### 5. 标签管理

**创建标签**

```
git tag <tag_name>
```

**查看所有标签**

```
git tag
```

> NOTE：默认标签是打在最新提交的commit的上的

**查看标签信息**

```
git show <tag_name>
```

**指定标签信息**

```
git tag -a <tag_name> -m 'message'
```

**推送标签**

推送本地标签

```
git push origin <tag_name>
```

推送全部未推送过的标签

```
git push origin --tags
```

**删除标签**

删除本地标签

```
git tag -d <tag_name>
```

删除远程标签

```
git push origin :refs/tags/<tag_name>
```

