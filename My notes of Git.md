# Git笔记

## 软件准备

#### 安装Git Bash

默认安装至C:\Program Files\Git

#### 配置

打开Git Bash，配置用户名和邮箱

```
git config --global user.name "<您的用户名>"
git config --global user.email "<您的邮箱>"
```

#### 生成SSH秘钥

生成一对SSH密钥，用来和代码托管服务端进行鉴权认证

```
ssh-keygen -t rsa -C "<您的邮箱>"
```

输入3个回车（Enter键）即可，生成的SSH秘钥对默认在~/.ssh/id_rsa（私钥）、~/.ssh/id_rsa.pub（公钥）位置

通过cd ~/.ssh可以访问目录位置

#### 复制秘钥

方式1.使用下面命令显示密钥然后手工复制

```
cat ~/.ssh/id_rsa.pub
```

方式2.使用命令直接复制密钥到剪贴板

```
clip < ~/.ssh/id_rsa.pub
```

#### 添加秘钥

登陆GitHub，打开“Account settings”-“SSH Keys”页面，在Key文本框里粘贴复制的秘钥

## 本地仓库

#### 创建本地库

进入项目文件夹，运行命令`git init`，把这个项目变成git可以管理的仓库

```
git init
```

#### 添加修改

小数点“.”，意为添加文件夹下的所有文件

```
git add .
```

#### 提交修改

引号内为提交说明

```
git commit -m "<说明文字>"
```

## 远程仓库

### 情况一：添加新的仓库

在GitHub创建一个新的空的仓库（无文件）

#### 复制地址

SSH地址：

HTTPS地址：相对较慢

#### 添加远程地址

```
git remote add origin <SSH or HTTPS>
```

#### 推送至远程库

```
git push -u origin master
```

由于远程库是空的，我们第一次推送`master`分支时，加上了`-u`参数，Git不但会把本地的`master`分支内容推送的远程新的`master`分支，还会把本地的`master`分支和远程的`master`分支关联起来，在以后的推送或者拉取时就可以简化命令。

#### 日常推送

```
git push origin master
```

#### SSH警告

当你第一次使用Git的`clone`或者`push`命令连接GitHub时，会得到一个警告

```
Are you sure you want to continue connecting (yes/no)?
```

输入`yes`回车即可

### 情况二：克隆已有的仓库

已有一个有文件的仓库

```
git clone origin
```


## 分支管理