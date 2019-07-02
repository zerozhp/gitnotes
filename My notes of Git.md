# Git笔记

### 软件准备

#### 安装Git Bash

默认安装至C:\Program Files\Git

#### 配置

打开Git Bash，配置用户名和邮箱

```
git config --global user.name "<您的用户名>"
git config --global user.email "<您的邮箱>"
```

#### SSH秘钥生成

生成一对SSH密钥，用来和代码托管服务端进行鉴权认证

```
ssh-keygen -t rsa -C "<您的邮箱>"
```

输入3个回车（Enter键）即可，生成的SSH秘钥对默认在~/.ssh/id_rsa、~/.ssh/id_rsa.pub位置

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

### 远程仓库