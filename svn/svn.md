# 服务器SVN

## 技术准备

#### 创建SVN仓库

```
svnadmin create <路径>
```

#### 配置版本库

**服务配置**：修改/conf/svnserve.conf

```
anon-access = none  #匿名不可读写访问
auth-access = write  #授权用户可以写
password-db = passwd  #用户账号文件路径
authz-db = authz #用户权限文件路径	
```

**添加用户**：修改/conf/passwd

```
<用户名> = <密码>
```

**权限控制**：修改/conf/authz

```
[/] #版本库或目录
<用户名> = r #读取权限
<用户名> = rw #读取和写入权限
```

#### 启动SVN服务

```
svnserve -d -r <路径> --listen-port <端口号>
```

- -r: 配置方式决定了版本库访问方式。

- --listen-port: 指定SVN监听端口，不加此参数，SVN默认监听3690

**单库svnserve方式**：路径指定到版本库

```
svnserve -d -r <版本库路径>
```

**多库svnserve方式**：路径指定到版本库的上级路径

```
svnserve -d -r <版本库上一级路径>
```

#### 停止SVN服务

```
killall svnserve
```

#### 查看SVN进程

查看SVN进程，获取进程号

```
ps -ef|grep svnserve
kill -9 <端口号>  //杀死进程
```

#### 检测SVN端口

```
netstat -ln |grep 3690
```

#### 参考

[菜鸟SVN教程](https://www.runoob.com/svn/svn-tutorial.html)

[Linux安装配置SVN服务器](https://www.cnblogs.com/puloieswind/p/5856326.html)

[linux服务器上配置多个svn仓库](https://blog.csdn.net/jesonjoke/article/details/77094867)

## 栗子——公司本地服务器SVN

### 需求

1. 一个站点对应一个仓库

2. 多个仓库共用用户文件及权限文件

3. 使用钩子更新到对应站点

### 环境

- CentOS 6.5
- 宝塔Linux面板 免费版 5.9.0
- SVN版本 1.6.11
- SVN仓库总目录 /var/svn/svnrepos

### 操作步骤

#### 第一步：宝塔新建站点

**域名**

```
www.160678.com  //识别区分站点
192.168.0.228:8022  //端口访问站点
```

**数据库**创建，**其他**不创建

**获取站点路径**：/www/wwwroot/www.160678.com

#### 第二步：SVN新建版本库

在仓库总目录下

```
svnadmin create /var/svn/svnrepos/www_160678_com
```

**配置版本库**：修改/var/svn/svnrepos/www_160678_com/conf/svnserve.conf

```
anon-access = none  #匿名不可读写访问
auth-access = write  #授权用户可以写
password-db = ../../conf/passwd #使用总仓库下统一的用户账号文件
authz-db = ../../conf/authz #使用总仓库下统一的用户权限文件
realm = /var/svn/svnrepos/www_160678_com #
```

**添加用户**：修改/var/svn/svnrepos/conf/passwd

```
zhangpeng = zhangpeng #用户名 = 密码
```

**设置用户权限**：修改/var/svn/svnrepos/conf/authz

```
## 用户组
[groups]
team_www_160678_com = chenshenggeng,zhengzhouyang,zhangpeng

## 仓库下用户组读取权限
[www_160678_com:/]
@team_www_160678_com = rw
```

现在就可以访问svn仓库了

#### 第三步：拉新



#### 第四步：创建钩子程序



#### 第五步：重启SVN

指定到SVN仓库总目录启动

```
svnserve -d -r /var/svn/svnrepos
```

