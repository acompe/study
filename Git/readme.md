# Git学习

## 1. 关于仓库配置
- 介绍
    - 可以配置用户姓名、邮箱。
    - 可以配置别名，以达到快速输入的目的。
- [git config 配置相关](https://github.com/acompe/study/blob/acompe/Git/1.git%20config.md)

## 2.关于Git仓库创建
- 已经存在的仓库
    - 在GitHub上创建一个空仓库
    - 通过git remote add origin +gitHub地址
    - 推送并为master添加远程分支，git push -u origin master
- 尚未存在的仓库
    - 方法一
        - 在GitHub上创建仓库。
        - 通过git clone +仓库地址 进行克隆。
        - 在克隆好的仓库进行 git init 初始化。
    - 方法二
        - 通过git init 对仓库进行初始化。
        - 在GitHub上创建一个空仓库
        - 通过git remote add origin +gitHub地址添加远程仓库。
        - 推送并为master添加远程分支，git push -u origin master。
- [git init 仓库初始化](https://github.com/acompe/study/blob/acompe/Git/20.git%20init.md)
- [git clone 仓库克隆](https://github.com/acompe/study/blob/acompe/Git/3.git%20clone.md)
- [git remote 配置远程仓库](https://github.com/acompe/study/blob/acompe/Git/15.git%20remote.md)

## 3. 关于用户与分支
- master
    - master 分支为系统默认分支。
    - 在初始化仓库的时候就会有一个master分支。
    - 一般master分支为发布分支，里面包括许多发布的版本。
- dev
    - 在初始化分支之后，就应该创建一个的dev分支。
    - 该分支用于同步测试代码。
    - 当开发到达周期结束的时候，就会将该分支合并到master分支上。
    - 同步后的master分支打上tag版本标签，进行发布。
- 自建分支
    - 在多人协作开发过程中，每个人都会有一个分支。
    - 个人在自己分支上进行开发。
    - 开发完毕后，将dev分支pull到本地，并将开发代码合并到dev
    - 将合并后的dev推送到远程仓库中。
- 分支切换
    - 切换当前分支
    - git checkout
- 分支合并
    - 单步合并分支
        - git rebase 
    - 一起合并分支
        - git merge
- [git branch 分支管理](https://github.com/acompe/study/blob/acompe/Git/5.git%20branch.md)
- [git checkout 分支切换](https://github.com/acompe/study/blob/acompe/Git/11.git%20checkout.md)
- [git merge 分支合并](https://github.com/acompe/study/blob/acompe/Git/12.git%20merge.md)
- [git rebase 分支合并](https://github.com/acompe/study/blob/acompe/Git/16.git%20rebase.md)

## 4.关于文件状态
- 未跟踪状态
    - 当创建新的文件或文件夹时，文件处于为追踪状态。
    - 该状态下，默认情况显示状态为红色。
    - git add
        - 当文件处于未跟踪状态时。
        - 通过该命令将文件放入暂存区。
- 更新状态
    - 当文件被修改时，文件处于更新状态。
    - 该状态下，默认情况下显示状态为红色。
    - git add
        - 当文件处于修改状态时。
        - 通过该命令将文件放入暂存区。
- 暂存状态
    - 当文件追踪后，且还未提交之前，文件处于暂存状态。
    - 当文件修改后，且还未提交之前，文件处于暂存状态。
    - 该状态下，默认情况显示状态为绿色。
    - git commit
        - 当文件处于暂存区时。
        - 当文件还没有提交，使用该命令进行提交。
- 入库状态
    - 当文件提交之后，该文件即已经进入仓库中。
- 文件对比
    - 对比文件与仓库内容
    - git diff
        - 对比未追踪文件与仓库文件。
        - 对比暂存区文件与仓库文件。
- 状态暂存
    - 将当前文件入栈
        - git stash
    - 将当前文件出栈
        - git stash pop
- [git status 文件状态浏览](https://github.com/acompe/study/blob/acompe/Git/6.git%20status.md)
- [git add 文件入暂存区](https://github.com/acompe/study/blob/acompe/Git/8.git%20add.md)
- [git commit 文件入库](https://github.com/acompe/study/blob/acompe/Git/9.git%20commit.md)
- [git diff 文件对比](https://github.com/acompe/study/blob/acompe/Git/7.git%20diff.md)
- [git stash 状态入栈](https://github.com/acompe/study/blob/acompe/Git/19.git%20stash.md)

## 5.仓库的拉取
- 介绍
    - 当开发人员进行开发之前，首先要保证自己仓库目前处于最新状态。
    - 通过仓库拉取操作更新仓库代码，用来保证仓库目前处于最新状态。
- git pull
    - 当前仓库版本低于远程仓库时。
    - 开发人员直接将远程仓库拉取到本地。
- git fetch
    - 当前仓库版本与远程仓库版本不一致时。
    - 开发人员将远程仓库同步到本地。
    - 可以查看同步内容，用来判断合并后是否出现问题。
    - 分支只能拉取到对应分支上去。
    - git merge
        - 将拉取来的内容同步到本地仓库中。
- [git pull 仓库拉取](https://github.com/acompe/study/blob/acompe/Git/10.git%20pull.md)
- [git fetch 仓库获取](https://github.com/acompe/study/blob/acompe/Git/13.git%20fetch.md)

## 6.仓库的推送
- 介绍
    - 当开发人员开发完成后。
    - 将开发代码都提交到仓库后。
    - 需要通过推送的方式将仓库放入远程仓库。
- git push 远程仓库 分支名称
    - 分支只能推送到对应分支上去。
- 该操作可以删除远程分支
    - git push 远程仓库 -d 分支名称
- 该操作可以推送标签到远程
    - git push --tag
- 该操作可以建立分支连接
    - git push -u 远程仓库 分支名称
- [git push 仓库推送](https://github.com/acompe/study/blob/acompe/Git/14.git%20push.md)

## 7.回滚操作
- 暂存区回滚
    - 将 add 入暂存区的文件回滚到之前的状态。
    - git reset HEAD 
- 仓库回滚
    - 将 commit 入库的内容进行回滚。
    - git reset --hard 提交ID
    - git revert 提交ID
- [git reset 回滚操作](https://github.com/acompe/study/blob/acompe/Git/17.git%20reset.md)
- [git revert 回滚操作](https://github.com/acompe/study/blob/acompe/Git/18.git%20revert.md)

## 8.仓库的标签
- 介绍
    - 开发周期结束。
    - 将测试分支dev同步到master。
    - 就会利用git tag -a 给版本添加标签。
- [git tag 仓库标签](https://github.com/acompe/study/blob/acompe/Git/4.git%20tag.md)

## 9.仓库的日志
- 介绍
    - 在git日常工作时，回产生日志。
    - 可以通过git log查看日志。
    - 可以根据git log 查看提交ID。
- [git log 仓库日志](https://github.com/acompe/study/blob/acompe/Git/2.git%20log.md)
[Git 英文相关文档](https://github.com/acompe/study/blob/master/Git/github-git-cheat-sheet.pdf)