# 设置签名
    项目级别/仓库级别：仅在当前本地库范围内有效
        git config user.name tom_Pro
        git config user.email goodMorning_pro@qq.com
        信息保存位置：./.git/config
    系统用户级别：登录当前操作系统的用户范围
        git config --global user.name tom_glb
        git config --global goodMorning_pro@qq.com
        信息保存位置：~/.gitconfig
# 基本操作
    ## 状态查看
        git status
    添加
        git add [file name]
    提交
        git commit -m "commit message" [file name]
    查看历史记录
        git log
            多屏显示控制方式：
                空格 向下翻页
                b 向上翻页
                q 退出
        git log --pretty=online
        git log --oneline
        git reflog
    前进后退
        基于索引值操作（推荐）
            git reset --hard [局部索引值]
        使用^符号：只能后退
            git reset --hard HEAD^
        使用~符号：只能后退
            git reset --hard HEAD~n
    reset命令的三个三叔对比
        --soft
            仅仅在本地库移动HEAD指针
        --mixed
            在本地库移动HEAD指针
            重置暂存区
        --hard
            在本地库移动HEAD指针
            重置暂存区
            重置工作区
    删除文件并找回
        前提：删除前，文件存在时的状态提交到了本地库
        操作：git reset --hard [指针位置]
            删除操作已经提交到本地库：指针位置指向历史记录
            删除操作尚未提交到本地库：指针位置使用HEAD
    比较文件差异
        git diff [文件名]
            将工作区中的文件和暂存区进行比较
        git diff [本地库中历史版本] [文件名]
            将工作区中的文件和本地库历史记录比较
        git diff
            不带文件名比较多个文件
# 分支管理
    分支操作
        创建分支
            git branch [分支名]
        查看分支
            git branch -v
        切换分支
            git checkout [分支名]
        合并分支
            第一步：切换到接收修改的分支（被合并，增加新内容）上
                git checkout [被合并分支名]
            第二部：执行merge命令
                git merge [有新内容分支名]
        解决冲突
            冲突的表现
                如下：
                <<<<<<<< HEAD
                hhhhhhhhh edit by hot_fix
                ========
                hhhhhhhhh edit by master
                >>>>>>>> master
            冲突的解决
                1. 编辑文件，删除特殊符号
                2. 把文件修改到满意的程度，保存退出
                3. git add [文件名]
                4. git commit -m "日志信息"
                    注意：此时commit一定不能带具体文件名
        分离HEAD
            切换换到某个历史提交点（HEAD分离状态）,在这个游离的分支上可以修改、提交、切换分支，切换之后会有如下提示：执行git branch [hash]创建一个新的分支
            git checkout [hash]
# 标签
    列出标签
        git tag
        可以按照特定的模式查找标签，如下：
            git tag -l "v1.*"
    创建标签
        附注标签：
            git tag -a [标签名] -m "注释信息" [hash]
        轻量标签：
            git tag [标签名] [hash]
    展示标签
        git show [标签名]
    删除标签
        git tag -d [标签名]
    推送标签到远程
        git push origin [标签名]
        推送所有标签
            git push origin tags
# 屏蔽文件
    步骤
        1. 在目录下穿件.gitignore文件
        2. 在.gitignore文件中添加需要屏蔽的内容，如：
            .*
            Listings/
            Objects/
            ...
# 创建远程仓库
    创建远程库地址别名
        git remote -v 查看当前所有远程地址别名
        git remote add [别名] [远程地址]
    推送
        git push [别名][分支名]
    克隆
        git clone [远程地址]
        