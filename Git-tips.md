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



