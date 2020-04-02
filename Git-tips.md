#  Git tips :rocket: 

### 将本地非空目录转化为Git仓库 

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

### Git 切换本地账号 

* 切换本地账号 

```
git config --global user.name "Your_uesrname"
git config --global user.email "username@XXX.com"
```
* 查看配置文件 

```
vim ~/.gitconfig
```
