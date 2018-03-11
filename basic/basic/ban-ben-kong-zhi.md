# 版本控制

版本控制是一种软体工程技巧，藉以在开发的过程中，确保由不同人所编辑的统一档案都得到更新。

目前用到的最广泛的控制器就是SVN和Git。

SVN（Subversion）是集中式管理的版本控制器，Git是分布式管理控制器，这是两者最本质的区别。

集中式:

分布式:

#### svn

集中式管理的代表，版本库存放在中央服务器。

[https://tortoisesvn.net/](https://tortoisesvn.net/ "TortoiseSVN")

###### 

#### git

分布式管理的代表，每个人都是一个版本库，通常我们会也有选择一个“中心仓库”。

[https://git-scm.com/](https://git-scm.com/ "Git")

###### 常见托管平台

* [http://code.taobao.org/](http://code.taobao.org/)
* [https://www.oschina.net/](https://www.oschina.net/)

### Git基本使用

这里我们就根据开发需求，以操作为准去学习。

* 软件安装

```bash
add-apt-repository ppa:git-core/ppa
apt update
apt install git
```

* 注册github并激活

[https://github.com/](https://github.com/)

* 创建一个项目
* 命令初体验，下载项目

```
git clone URL
```

* 配置用户信息

  ```
  git config --global user.name "Rock"
  git config --global user.email "rockrong1204@aliyun.com"
  ```

* 用PyCharm打开项目并配置Git信息，Git忽略

* 图形化更新代码

* 图形化提交代码

#### 重要概念

* 工作区
* 暂存区
* 本地仓库
* 远程仓库
* 分支

#### Git指令

* git init
* git status
* git add
* git commit
  * git commit -m "Message"
* git log
* git diff
* git reset
  * git reset --hard version\_code
* git rm
  * git rm -f FileName
* git mv
* git branch
  * git branch BranchName
  * git branch -d BranchName
* git checkout
  * git checkout BranchName
  * git checkout -b BranchName
  * git checkout FileName
* git merge
* git tag
  * git tag "TAG\_name"
* * git tag -a "TAG\_name"  version\_code
  * git tag -d TAG\_name
* git show
  * git show TagName
* git stash
  * git stash drop
  * git stash pop
  * git stash apply
* git remote
* git rebase
  * git rebase BranchName
  * git rebase --continue
  * git rebase --abort



