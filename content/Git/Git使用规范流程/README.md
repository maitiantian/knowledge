# <p align="center" style="border-bottom: 3px solid #e7e7e7;">Git使用规范流程</p>

![Git使用规范流程](../../images/git_use_flows.png)

## 第一步：新建分支

每次开发新功能，都应该新建一个单独的分支：

```bash
# 获取主干最新代码
$ git checkout master
$ git pull

# 新建一个开发分支myfeature
$ git checkout -b myfeature
```

## 第二步：提交分支commit

分支修改后，就可以提交commit了：

```bash
$ git add .

# 使用git commit命令的verbose参数，会列出diff的结果
$ git commit --verbose
```

## 第三步：撰写提交信息

提交commit时，必须给出完整扼要的提交信息，下面是一个范本。

```bash
Present-tense summary under 50 characters

* More information about commit (under 72 characters).
* More information about commit (under 72 characters).

http://project.management-system.com/ticket/123
```

第一行是提要，不要超过50个字符；然后空一行，罗列出改动原因、主要变动、以及需要注意的问题；最后，提供对应的网址（比如Bug ticket）。

## 第四步：与主干同步

```bash
# git fetch是将远程主机的最新内容拉到本地，
# 用户检查后决定是否合并到本机分支中。

# 而git pull则是将远程主机的最新内容拉下来后直接合并，
# 即：git pull = git fetch + git merge，这样可能会产生冲突，需要手动解决。

$ git fetch origin
$ git rebase origin/master
```

## 第五步：合并commit

分支开发完成后，可能有一堆commit，但是合并到主干的时候，往往希望只有一个（或最多两三个）commit，这样不仅清晰，也容易管理。

```bash
$ git rebase -i origin/master
```

## 第六步：推送到远程仓库

合并commit后，就可以推送当前分支到远程仓库了。

```bash
# git push命令要加上force参数，
# 因为rebase后，分支历史改变了，跟远程分支不一定兼容
$ git push --force origin myfeature
```

## 第七步：发出Pull Request

提交到远程仓库以后，就可以发出 Pull Request到master分支，然后请求别人进行代码review，确认后可以合并到master。