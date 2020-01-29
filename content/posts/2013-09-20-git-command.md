---
layout: post
title: 'Git - command'
date: 2013-09-20
comments: true
categories: [git]
---
## Git - command

```sh
git status
# 查看修改哪些檔案

git diff
# 比對修改了的地方與上一個 commit 有何不同
git diff <file>
# 比對修改的檔案與上一個 commit 有何不同
git diff <old commit id>..<new commit id>
# 比對不同 commit id 的檔案差異

git coheckout -- <file>
# 把檔案回復到修改前的樣子

git add <file>
# 加入要 commit 的檔案

git rm <file>
# 移除檔案(有 commit 過的檔案要移除, rm <file> 之後要執行的指令)

git reset HEAD <file>
# 把 git add 之後的檔案回復到 git add 前

git commit -m '註解'
# or
git commit
# commit 檔案進入版本控管系統
git commit --no-verify
# 不驗證 commit

git log
# git commit log 紀錄
git log -p
# 詳細的log紀錄(修改哪些部分)

git blame <file>
# 查看修改的紀錄

git clone <repository>
# 拉 repository 下來到 local 端

git branch <branch name>
# 建立一個 local 端的 branch

git checkout <branch>
# 切換到該 branch

git branch
# 查看本地端的 branch

git branch -r
# 查看 remote 端的 branch

git stash
# 檔案 不commit 跳 branch (暫存)
git stash pop
# 回復檔案不 commit 狀態(讀回)

git branch -d <local branch>
# 刪除本地端的 branch

git branch -r -d <remote branch>
# 刪除 remote 端的 branch

git checkout --track -b <local branch> origin/<remote branch>
# 將遠端的 branch 並在 local 建立 branch

```
[Refer](http://blog.longwin.com.tw/2009/05/git-learn-initial-command-2009/)
[Refer](http://ihower.tw/blog/archives/2620)
