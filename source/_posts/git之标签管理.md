---
title: git之标签管理
date: 2017-04-14 12:16:01
categories: ['技术']
tags: ['git']
---

## git标签是什么？干什么用的？

git标签就是打标签时刻的版本库的快照，其实它就是指向某个 `commit` 的指针。能够方便将来查看版本库某个时刻的历史版本。

git中有commit，为什么还要引入tag？

"请把上周一的那个版本打包发布，commit号是6a5819e..."

“一串乱七八糟的数字不好找！”

如果换一个方法：

”请把上周一的那个版本打包发布，版本号是v1.2”

“好的，按照tag v1.2查找commit就行！”

所以，tag就是一个让人容易记住的有意义的名字，它跟某个commit绑在一起。

## 创建标签

git tag <name>: 打一个新的标签；

默认标签是打在最新提交的commit上的。有时候，如果忘了打标签，方法是找到历史提交的commit id，然后打上就可以了:
git log --pretty=oneline --abbrev-commit
git tag <name> <commit id>

git tag -a <name> -m <description，单、双引号都没有问题> <commit id>: 创建带有说明的标签；
e.g. git tag -a v0.1 -m 'version 0.1 released' 3628164

---

git tag: 查看所有标签；
标签不是按时间顺序列出，而是按字母顺序列出。

git show <tagname>: 查看标签信息；


## 操作标签

git tag -d <tagname>: 删除本地的标签；

如果要删除远程标签的话，先从本地删除；然后：
git push origin :refs/tags/<tagname>
可以登录github查看是否真的从远程库删除了标签；

git push origin <tagname>: 推送某个标签到远程；

git push origin --tags: 一次性推送全部尚未推送到远程的本地标签；

有一点需要注意，如果你只是push你的本地仓库到远程，但是并没有明确使用推送标签的命令推送标签，那么标签将只会在本地，不会出现在远程。

## References

- [廖雪峰 Git标签管理](http://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000/0013762144381812a168659b3dd4610b4229d81de5056cc000)
