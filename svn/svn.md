# 本地服务器SVN

#### 创建SVN仓库

```
svnadmin create <路径>
```

#### 配置版本库

**添加用户**修改/conf/passwd

```

```

**权限控制**修改/conf/authz

```

```

**服务配置**修改/conf/svnserve.conf

```

```

#### 启动SVN服务

```
svnserve -d -r <路径>
```

#### 关闭SVN服务

查看SVN进程，获取进程号

```
ps -ef|grep svnserve
```

杀死进程

```
kill -9 <端口号>
```

