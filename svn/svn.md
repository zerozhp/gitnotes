# 服务器SVN

## 技术准备

#### 创建SVN仓库

```bash
svnadmin create <路径>
```

#### 配置版本库

**服务配置**：修改/conf/svnserve.conf

```bash
anon-access = none  #匿名不可读写访问
auth-access = write  #授权用户可以写
password-db = passwd  #用户账号文件路径
authz-db = authz #用户权限文件路径	
```

**添加用户**：修改/conf/passwd

```bash
<用户名> = <密码>
```

**权限控制**：修改/conf/authz

```bash
[/] #版本库或目录
<用户名> = r #读取权限
<用户名> = rw #读取和写入权限
```

#### 启动SVN服务

```bash
svnserve -d -r <路径> --listen-port <端口号>
```

- -r: 配置方式决定了版本库访问方式。

- --listen-port: 指定SVN监听端口，不加此参数，SVN默认监听3690

**单库svnserve方式**：路径指定到版本库

```bash
svnserve -d -r <版本库路径>
```

**多库svnserve方式**：路径指定到版本库的上级路径

```bash
svnserve -d -r <版本库上一级路径>
```

#### 停止SVN服务

```bash
killall svnserve
```

#### 查看SVN进程

查看SVN进程，获取进程号

```bash
ps -ef|grep svnserve
kill -9 <端口号>  //杀死进程
```

#### 检测SVN端口

```bash
netstat -ln |grep 3690
```

#### 检出命令

```bash
svn checkout svn://<路径> <本地目录全路径> --username <用户名> --password <密码>
```

**检出不包括源文件夹根目录**

在svn文件夹后面打个空格，在加个“.”就行了

```
svn checkout svn://<路径>/ . <本地目录全路径> --username <用户名> --password <密码>
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

1.在仓库总目录下新建项目仓库

```bash
svnadmin create /var/svn/svnrepos/www_160678_com
```

2.配置版本库：修改/var/svn/svnrepos/www_160678_com/conf/svnserve.conf

```bash
anon-access = none  #匿名不可读写访问
auth-access = write  #授权用户可以写
password-db = ../../conf/passwd #使用总仓库下统一的用户账号文件
authz-db = ../../conf/authz #使用总仓库下统一的用户权限文件
realm = /var/svn/svnrepos/www_160678_com #
```

3.添加用户：修改/var/svn/svnrepos/conf/passwd

```bash
zhangpeng = zhangpeng #用户名 = 密码
```

4.设置用户权限：修改/var/svn/svnrepos/conf/authz

```bash
## 添加用户组
[groups]
team_www_160678_com = chenshenggeng,zhengzhouyang,zhangpeng

## 仓库下用户组读取权限
[www_160678_com:/]
@team_www_160678_com = rw
```

现在就可以访问svn仓库了（暂时不管）

```bash
#仓库路径
svn://192.168.0.228/www_160678_com
#账号
zhangpeng
#密码
zhangpeng
```

#### 第三步：站点目录检出仓库

1.进入站点目录

```bash
cd /www/wwwroot/www.160678.com
```

2.检出不包括仓库源文件夹根目录

```bash
svn checkout svn://192.168.0.228/www_160678_com/ . --username=zhangpeng --password=zhangpeng
```

***注意：一定要先checkout一次，才能同步，每次新建项目都需要***

3.将站点目录下的文件提交至仓库

3.1查看文件状态，是否版本控制

```bash
svn status #查看文件状态
# ?表示未版本控制
?       .user.ini
?       404.html
?       index.html
?       .htaccess
```

3.2添加所有文件进入版本库（建议使用第二条命令）

```bash
svn add * --force #添加所有文件，隐藏文件不会提交
svn add . --no-ignore --force #循环遍历文件夹中所有未添加的文件，添加到版本管理
# A表示加入版本库
A         .user.ini
A         404.html
A         .htaccess
A         index.html
```

3.3提交至仓库（会提示输入账号密码）

```bash
svn commit -m "<注释>" #提交
```

***注意：以防未受版本控制文件冲突，一定要进行将站点目录下的文件提交至仓库***

#### 第四步：创建钩子

1.进入钩子目录

```bash
cd /var/svn/svnrepos/www_160678_com/conf/hooks
```

2.复制新建钩子文件`post-commit`

```bash
cp post-commit.tmpl post-commit
```

3.修改文件`post-commit`

```bash
#!/bin/sh

REPOS="$1"
REV="$2"

#mailer.py commit "$REPOS" "$REV" /path/to/mailer.conf

export LANG=en_US.UTF-8
SVN_PATH=/usr/bin/svn
SVN_USER=webupdate
SVN_PASS=webupdate123
WEB_USER=www
WEB_ROOT=root
WEB_PATH=/www/wwwroot/www.160678.com
LOG_PATH=/tmp/svn.log
echo `date "+%Y-%m-%d %H:%M:%S"` >> $LOG_PATH
echo `whoami`,$REPOS,$REV >> $LOG_PATH
$SVN_PATH update $WEB_PATH --username $SVN_USER --password $SVN_PASS --no-auth-cache >> $LOG_PATH
chown $WEB_USER.$WEB_ROOT -R $WEB_PATH
```

> 说明：
>
> - whoami #执行此程序的用户
> - REPOS="$1" #svn项目绝对路径值
> - REV="$2" #最新版本号
> - --no-auth-cache #不保存账户认证信息

4.设置脚本所属用户组，www为web服务运行账户和组

```bash
chown www:www /var/svn/svnrepos/www_160678_com/hooks/post-commit
```

5.添加脚本执行权限

```bash
chmod +x /var/svn/svnrepos/www_160678_com/hooks/post-commit
```

#### 第五步：重启SVN

指定到SVN仓库总目录启动

```bash
killall svnserve
svnserve -d -r /var/svn/svnrepos
```

### 参考

[Linux下SVN服务器自动更新文件到Web目录的方法](<https://www.jb51.net/article/69234.htm>)

[Linux下SVN服务器自动更新文件到Web目录](<https://www.osyunwei.com/archives/9131.html>)

[php利用svn hooks将程序自动发布到测试环境](<https://www.bbsmax.com/A/Gkz1XmVjdR/>)

[svn使用post-commit实现自动部署,自动checkout](<https://blog.csdn.net/qq_42033352/article/details/81117185>)

[SVN常用命令之checkout](<https://blog.csdn.net/gengxiaoming7/article/details/50512195/>)