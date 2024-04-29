# Git basic

Progit

1.Introduction 介绍 Chapter 1 What Git is, Why it comes, How to install and set up it. 主要讲述了 Git 的历史背景及如何安装设置。 Chapter 2 Basic Git usage. 主要介绍了 Git 80% 的常用基础命令操作。 Chapter 3 Branching model in Git. 主要介绍了 Git 的分支模型。 Chapter 4 Git on the server. 主要介绍了个人服务器上如何设置 Git。 Chapter 5 Full detail various distributed workflows and how to accomplish them with Git. 介绍了分布式工作流以及如何通过 Git 来协作。 Chapter 6 GitHub hosting service and tooling. 介绍了 Github 托管服务和工具。 Chapter 7 Git commands. 介绍了一些高级命令。 Chapter 8 Custom Git environment 如何自定义 Git 环境。 Chapter 9 Deals with Git and other VCSs. Chapter 10 Depths of Git internals 深入理解 Git。 Appendix A Examples of using Git. Git 使用示例。 Appendix B Scripting and extending Git. 如何编写 Git 脚本。 Appendix C Major Git commands. 主要的 Git 命令。

2.Chapter 1 Updates: git clone git://git.kernel.org/pub/scm/git/git.git

git config: 优先级 1>2>3

1. \[path]/etc/gitconfig file: 对所有用户生效 --system
2. \~/.gitconfig or \~/.config/git/config file：对特定用户生效 --global
3. .git/config：对本地仓库生效 --local

查看 git config: git config --list --show-origin

\*必须设置用户名和地址： git config --global user.name "hxj" git config --global user.email hxj@example.com

配置文本编辑器： git config --global core.editor emacs git config --global core.editor "'C:/Program Files/Notepad++/notepad++.exe' -multiInst -notabbar -nosession -noPlugin"

修改默认分支 master 的名字为 main: git config --global init.defaultBranch main

查看配置： git config --list

查看某项配置值 git config

查看帮助文档 git help git --help,-h 简洁版 man git-

本地目录初始化存储库 git init

追踪并提交 git add \*.c git add LICENSE git commit -m 'Initial project version'

克隆现有库 git clone https://github.com/libgit2/libgit2 git clone https://github.com/libgit2/libgit2 mylibgit

工作目录里文件的只有两种状态： tracked(unmodified,modified,staged) or untracked

检查文件状态 git status

忽略文件功能 cat .gitignore

比较修改内容 git diff

提交文件内容 git commit git commit -m "Story 182: fix benchmarks for speed" 跳过跟踪文件步骤提交 git commit -a -m 'Add new benchmarks'

从缓存区中删除文件 git rm git rm -f 强制删除已经修改的文件 git rm --cached README 不追踪但保留文件内容 git rm \*\~ 正则删除

重命名文件 git mv file\_from file\_to <==> mv,rm,add

查看历史提交 git log git log -p -2 查看近两次提交的差异 git log --stat 查看总体信息 git log --pretty=format:"%h - %an, %ar : %s" 格式化打印 git log --pretty=format:"%h %s" --graph 图形打印 git log --since=2.weeks 限制日志输出 git log -S function\_name 打印特定函数修改的log git log -- path/to/file 查看指定文件在 Git 仓库中的提交历史 git log --pretty="%h - %s" --author='Junio C Hamano' --since="2008-10-01"\
\--before="2008-11-01" --no-merges -- t/

撤销提交 git commit --amend 修改上一次提交

git reset 取消追踪，更推荐使用 git restore git checkout -- 取消所有本地修改，恢复成初始文件

显示远端仓库 git remote origin 是默认的远端仓库的名字 git remote -v 显示远端的 URL git remote add 增加一个远端仓库 git fetch 从远端拉取 git fetch origin git push 推送至远端，不允许同时推送。脑裂问题 git remote show origin 查看远端信息 git remote rename 重命名远端 git remote remove 移除远端

lightweight and annotated 标记 git tag git tag -l 过滤 git tag -a v1.0 -m "my version 1.0" 信息会存储在 tag 里面 git tag v1.4-lw 轻量级 tag git tag -a v1.2 9fceb02 补标签需要提供对应文件校验和 git push origin 将 tag 推送至远端同步，默认不会推送 git push origin --tags 推送所有 tag git tag -d 删除标签 git push :refs/tags/ git push origin --delete 两种删除远端标签的方式 git checkout 检查标签的指向 git checkout -b version2 v2.0.0 修复旧版本时候，根据标签指向创建新分支，类似于私人版本打补丁

别名 git config --global alias.co checkout git config --global alias.br branch git config --global alias.ci commit git config --global alias.st status

Git 的存储机制 Git doesn’t store data as a series of changesets or differences, but instead as a series of snapshots. 元数据对象：blobs,tree,commit pointer branch 就是指针头 HEAD 为 loacl pointer，指示当前所在的 branch

创建 branch git branch 显示分支列表 git branch -v 查看每个分支的最后一次提交 git branch --merged 查看已合并的分支 git branch --no-merged 查看未合并分支 git branch --move bad-branch-name corrected-branch-name 本地重命名分支 git push --set-upstream origin corrected-branch-name 远端重命名分支 git push origin --delete bad-branch-name 远端删除分支 git log --oneline --decorate 显示当前 HEAD 指向哪个 branch git checkout 切换分支，及将 HEAD 指针指向对应的 branch 指针

git log --all 显示所有分支 log git log branch 显示指定分支 log git checkout -b 切换到新分支

合并到当前分支到目标分支 git merge

如果要合并两个不同快照流上面的分支，git 会再创建一个指向这两条流分支的一个新快照，并将 master 分支前移。

git pull == git fetch + git merge

git rebase 从不同分支的父亲派生，比之前的好处在于会得到线性的分支流历史。即看起来好像没有分叉过 Do not rebase commits that exist outside your repository and that people may have based work on.

git diff --check

$ git clone $ cd project $ git checkout -b featureA   ... work ... $ git commit   ... work ... $ git commit $ git remote add myfork git push -u myfork featureA $ git checkout -b featureB origin/master   ... work ... $ git commit $ git push myfork featureB $ git request-pull origin/master myfork   ... email generated request pull to maintainer ... $ git fetch origin $ git checkout featureA $ git rebase origin/master $ git push -f myfork featureA

Git 本质 key-value data store Git is fundamentally a content-addressable filesystem with a VCS user interface written on top of it “plumbing” commands 和 UNIX 集合 “porcelain” commands

git init test ls -a git init: config 项目的配置信息 description 用于 GitWeb program hooks/ hook scripts info/ .gitignore file objects/ 存储所有 database refs/ stores pointers into commit objects in that data (branches, tags, remotes and more) HEAD points to the branch you currently have checked out, and the index file is where Git stores your staging area information

$ echo 'test content' | git hash-object -w --stdin 获取文本写入数据库并返回唯一键 d670460b4b4aece5915caf5c68d12f560a9fe3e4 #40-character checksum SHA-1 hash

$ find .git/objects/ -type f .git/objects/d6/70460b4b4aece5915caf5c68d12f560a9fe3e4

The subdirectory is named with the first 2 characters of the SHA-1, and the filename is the remaining 38 characters 前两个字符为子目录名，后38个字符为文件名

$ git cat-file -p d670460b4b4aece5915caf5c68d12f560a9fe3e4 test content 显示对象内容值

保留工作区里面的每一个数据对象哈希值，这种哈希只对文件内容进行哈希映射。对文件名不涉及 $ find .git/objects/ -type f .git/objects/1f/7a7a472abf3dd9643fd615f6da379c4acb3e3a #blob 01 .git/objects/83/baae61804e65cc73a7201a7252750c76066a30 #blob 02 .git/objects/d6/70460b4b4aece5915caf5c68d12f560a9fe3e4 #blob 03

对象 blob 解决单个文件存储问题，对象 tree 解决组文件存储以及文件名存储问题。 tree 类似于 UNIX 的目录及子目录， blob 类似于 UNIX 的文件, 子 tree 是一个指针

$ git cat-file -p master^{tree} 指定查看 master 最后一次 commit 的 tree 040000 tree f1653c425eee577567d7251931b163ba6e663ca4 2022\
100644 blob 283691da4bc3feb545cc2d1c7c067cf5ae5ea65c README\
040000 tree 14e4a2e97ba4e495a4616112140908a1b5b1c844 archives\
040000 tree f3900be0ec2f0fcdbd7899d88ad25663ede23e64 css\
040000 tree b1627a58bfc1fa0e1e107f174bd42dd4d13cabf7 images\
100644 blob a5424bf06647233e874004f7296d61d3806c0a1a index.html 040000 tree e4a6ecd8f26f8bbf734698ef9c5e392a205c6a9a js <----

$ git cat-file -p e4a6ecd8f26f8bbf734698ef9c5e392a205c6a9a <-------- 100644 blob 8e3ae6adf5c1309ba6b9340076f0da9f2c3e9532 bookmark.js\
100644 blob 505c21b7d826c718d118727f47e14c5704dd7d0f comments-buttons.js 100644 blob 4045e8c0630c8307ce64667b2122df9bec8eaadd comments.js\
100644 blob caa0075b16ebe50efa9c6240c066fcc924c88113 config.js 100644 blob faaab32606cffa9b4de851c17ca307443aeb630a motion.js 100644 blob 6262daa53ddc8f3263bca4a39ae4388aaf63b986 next-boot.js\
100644 blob da6113603d54fcc71b34619579439ec6fe52e71e pjax.js 100644 blob 6b58acd7bcddf73b00b2874a91f94b609dbb47cb schedule.js 040000 tree 369e1e5a82cbebaf6dfcea56d3e653da3c83ba75 schemes 040000 tree 9da2bcb1df752ae60fb8b6e5b6e5e2fb8189cbee third-party 100644 blob 0a0665b04cceeba44a8c946b8eb5770dbbe8b784 utils.js

git update-index 命令可以更新索引 $ git update-index --add --cacheinfo 100644\
83baae61804e65cc73a7201a7252750c76066a30 test.txt 100644 普通文件 100755 可执行文件 120000 符号链接文件

git write-tree 写入 tree 对象命令，指向刚刚对应的 blob 对象 $ git write-tree d8329fc1cc938780ffdd9f94e0d364e0ea74f579 $ git cat-file -p d8329fc1cc938780ffdd9f94e0d364e0ea74f579 100644 blob 83baae61804e65cc73a7201a7252750c76066a30 test.txt

git read-tree 读取树命令 git read-tree --prefix=bak d8329fc1cc938780ffdd9f94e0d364e0ea74f579 读取一个已存在的 tree

commit object about who saved the snapshots, when they were saved, or why they were saved

$ echo 'First commit' | git commit-tree d8329f fdf4fc3344e67ab068f836878b6c4951e3b15f3d

类似于根目录，必须有根目录才能找到子目录及其文件。不同的根代表着不同的 commit，也就是不同的 snapshot

本质上所有的用户友好命令其实都是在调用类 UNIX 命令来创建 blob，tree, commit 对象。

Git 如何构造 HEAD 和 blob 对象？ 1.内容+一个空格+内容长度+空字符 $ irb

> > content = "what is up, doc?" => "what is up, doc?" header = "blob #{content.bytesize}\0" => "blob 16\u0000"

2.重新组装报头和内容后，计算 SHA-1 哈希值。

> > store = header + content => "blob 16\u0000what is up, doc?" require 'digest/sha1' => true sha1 = Digest::SHA1.hexdigest(store) => "bd9dbf5aae1a3862dd1526723246b20206e5fc37"

$ echo -n "what is up, doc?" | git hash-object --stdin bd9dbf5aae1a3862dd1526723246b20206e5fc37

3.使用 zlib 压缩内容

> > require 'zlib' => true zlib\_content = Zlib::Deflate.deflate(store) => "x\x9CK\xCA\xC9OR04c(\xCFH,Q\xC8,V(-\xD0QH\xC9O\xB6\a\x00\_\x1C\a\x9D"

4.根据计算出来的哈希值存储原始内容文件

> > path = '.git/objects/' + sha1\[0,2] + '/' + sha1\[2,38] => ".git/objects/bd/9dbf5aae1a3862dd1526723246b20206e5fc37" require 'fileutils' => true FileUtils.mkdir\_p(File.dirname(path)) => ".git/objects/bd" File.open(path, 'w') { |f| f.write zlib\_content } => 32

如果将这些常用的哈希值写进一个文件里面，就方便很多。也就是 refs/ 的内容

$ git update-ref refs/heads/master 1a410efbd13591db07496601ebc7a059dd55cfe9 更新引用文件 $ git update-ref refs/heads/test cac0ca 即创建一个 branch

HEAD file is a symbolic reference to the branch you’re currently on. 这个文件其实就是当前 branch 文件的一个链接文件 git branch

$ cat .git/HEAD ref: refs/heads/master

git checkout test

$ cat .git/HEAD ref: refs/heads/test

$ git symbolic-ref HEAD refs/heads/test 修改此文件

第四种对象 Tag，通常指向的是 commit 对象，不修改只是指向。 $ git update-ref refs/tags/v1.0 cac0cab538b970a37ea1e769cbbde608743bc96d 直接指向 $ git tag -a v1.1 1a410efbd13591db07496601ebc7a059dd55cfe9 -m 'Test tag' 带注释会先创建指向的指向 $ cat .git/refs/tags/v1.1 9585191f37f7b0fb9444f35a9bf50de191beadc2

remote 指向

Packfiles 将所有对象统统压缩成一个压缩包 只存储增量 $ curl https://raw.githubusercontent.com/mojombo/grit/master/lib/grit/repo.rb > repo.rb $ git checkout master $ git add repo.rb $ git commit -m 'Create repo.rb' \[master 484a592] Create repo.rb  3 files changed, 709 insertions(+), 2 deletions(-)  delete mode 100644 bak/test.txt  create mode 100644 repo.rb  rewrite test.txt (100%)

自动清理 git gc --auto

未完待续...
