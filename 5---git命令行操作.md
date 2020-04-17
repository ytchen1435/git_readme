注：除克隆项目外，所有git指令都需要在项目文件夹内部操作。即可以通过ls -a看到.git文件夹的那个目录。

git status -----查看当前版本库状态

git log -----查看当前版本库历史记录

git branch -----查看当前分支情况

git checkout 分支名称      -----切换到对应分支

git pull   ----更新本地仓库

# 1、克隆（下载）项目

git clone [-b 指定的分支] 远端ssh地址
 
# 2、上传项目

1)添加到暂存区

git add .

2)添加注释并提交到本地

git commit -m "注释"

3)推送到远端

git push [远端分支名称]

# 3、恢复本地未提交的修改

1）删除未提交的新增文件

git clean -dxf

2)恢复未提交的修改内容

git checkout .

# 4、回退版本

1)查看当前分支记录

git log

如下：

commit cbbd5f60d3749f8168ddc4727ad0b2e65014419c (HEAD, origin/master, origin/HEAD)

Author: chenyt <chenyt@ruhrtec.cn>

Date:   Fri May 31 10:24:27 2019 +0800

    234234

commit ec171888df01d92170cd8bc8398b36b3bcfc9cd4 (master)

Author: chenyt <chenyt@ruhrtec.cn>

Date:   Fri May 31 10:16:08 2019 +0800

    123

commit 9ad27fca19889c2ac242ed38f028e47c8852a0bd

Author: chenyt <chenyt@ruhrtec.cn>

Date:   Mon May 13 18:07:41 2019 +0800

    123

2）回退到相应版本

git reset 9ad27fca19889c2ac242ed38f028e47c8852a0bd

# 5、暂存修改
有时候需要切换分支，但是当前修改还不想提交，可以选择暂存修改。

1）暂存修改

`git stash --all

2）查看所有暂存

`git stash list

3）恢复暂存的修改

`git stash pop

# 6、A分支合并到B分支

1)切换到要A分支

git checkout origin/A

2)获取A分支最新内容

git pull origin A 

3)查看当前分支最新的编号

git log

commit 2d986946e1b42c93c6d548e2c5d47603bc3bf9b6 (origin/zhangcm)

Merge: 049a04b4 f0592682

Author: zhangcm <zhangcm@ruhrtec.cn>

Date:   Fri May 31 14:56:38 2019 +0800


    目录结构调整


4)切换到B分支

git checkout B

5)开始合并

git merge 2d986946e1b42c93c6d548e2c5d47603bc3bf9b6

6)查看冲突

git diff

7)上传最新版本

冲突解决完之后，按照2，上传项目的方法即可上传到远端

# 7、git lfs 操作

1）初始化

git lfs install

2）配置

git lfs track "*.psd" 即可使后缀为psd的文件变成大文件存储模式

或者在git根目录创建  .gitattributes  文件，并添加以下内容：

*.psd filter=lfs diff=lfs merge=lfs -text

3）常用指令

查看当前使用 Git LFS 管理的匹配列表
git lfs track

使用 Git LFS 管理指定的文件
git lfs track "*.psd"

不再使用 Git LFS 管理指定的文件
git lfs untrack "*.psd"

类似 `git status`，查看当前 Git LFS 对象的状态
git lfs status

枚举目前所有被 Git LFS 管理的具体文件
git lfs ls-files

检查当前所用 Git LFS 的版本
git lfs version

针对使用了 LFS 的仓库进行了特别优化的 clone 命令，显著提升获取
LFS 对象的速度，接受和 `git clone` 一样的参数。 git lfs clone https://github.com/user/repo.git