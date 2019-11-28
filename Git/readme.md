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

    