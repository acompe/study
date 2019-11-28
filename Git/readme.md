# Git学习

## 1.关于Git仓库创建
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
    - [整理-git init](https://github.com/acompe/study/blob/acompe/Git/20.git%20init.md)
    
## 2. 关于用户与分支
- 系统默认分支
    - master
        - 在初始化仓库的时候就会有一个master分支。
        - 一般master分支为发布分支，里面包括许多发布的版本。
    - dev
        - 在初始化分支之后，就应该创建一个的dev分支。
        - 该分支用于同步测试代码。
        - 当开发到达周期结束的时候，就会将该分支合并到master分支上。
        - 同步后的master分支打上tag版本标签，进行发布。
    