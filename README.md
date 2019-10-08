![npm](https://img.shields.io/npm/v/ger-cli)

# ger-cli

> Gerrit in your command lines.
> Frok from [gerrit-cli](https://github.com/shanesmith/gerrit-cli), thanks to [shanesmith](https://github.com/shanesmith).

## 安装

```sh
$ sudo npm install -g ger-cli
```

**参考环境**

- NodeJS >= 0.12
- Gerrit >= 2.12.3

## 用法


### 获取帮助
```
gerrit help               获取命令列表
gerrit help <command>     获取命令详情
```

### 命令列表
```
help            获取帮助
config          配置
projects        显示远端的项目列表
clone           从远端拉取仓库
add-remote      为本地库添加远端源
install-hook    安装commit-msg hook
patches         显示当前工程在远端的patch列表
status          显示指定patch的详情
assign          定义当前patch的评审者
up              推送到评审分支
draft           推送草稿
checkout        检出分支
recheckout      重新检出当前分支
ssh             在远端执行任意Gerrit命令
review          提交评审
submit          正式提交
abandon         废弃提交
comment         提交评论
ninja           推送并立即正式提交
web             打开当前patch的网页
completion      启用自动补全
topic           创建新分支
clean           清空已经合并的分支
squad           管理评审组
```


### 最佳实践

基础配置

```sh
$ gerrit config

# Creating new configuration for "default"
# ? Host (ex: example.com) sprockets.com
# ? Port 29418
# ? User george
```

拉取项目

```sh
$ gerrit clone killer-app

# ? Clone to which folder? killer-app
# Cloning project killer-app from default config into folder killer-app...
# ...
# Installing commit-msg hook...
```

创建分支

```sh
$ gerrit topic lasers

# Branch lasers set up to track remote branch master from origin.
```

修改并提交代码

```sh
$ vim shark.js

# Hack, hack, hack...

$ git commit -m "Added fricken lasers"
```

为此次提交创建patch并推送到评审分支

```sh
$ gerrit up

# Pushing to origin (refs/for/master/lasers)
# remote:
# remote: New Changes:
# remote:   https://sprockets.com/gerrit/57420 Added fricken lasers
# remote:
# To ssh://sprockets.com:29418/killer-app.git
#  * [new branch]      HEAD -> refs/for/master/lasers
```

定义一个评审组

```sh
$ gerrit squad set dudes jmartin cbush

# Reviewer(s) "jmartin, cbush" set to squad "dudes".

$ gerrit assign @dudes slevasseur

# Assigned reviewer jmartin
# Assigned reviewer cbush
# Assigned reviewer slevasseur
```

查看远端的patch

```sh
$ gerrit patches --not-reviewed --assigned

# Number  Topic   Branch  Owner    Updated 
# ------  ------  ------  -----    --------
# 123456  fixBug  master  cbush    Mar 14th
# 713705  soleil  master  jmartin  Sep 3rd
```

检出patch

```sh
$ gerrit checkout fixBug

# Getting latest patchset...
# Refspec is refs/changes/56/123456/1
```

评审代码

```sh
$ gerrit review 1 -1 "Bug is fixed, but needs more cow bells."

# Reviews have been posted successfully.
```

如果需要评论某行代码，可以通过下面的命令快速打开patch对应的网页

```sh
$ gerrit web
```

更多用法参见`gerrit help`
