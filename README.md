# Paid_Q-A
### 配置

------

#### 环境

- ##### git

  使用 git 管理开发版本，GitHub账号注册等跳过不提，下面从git的安装开始说明

  - 安装git

    1. 首先在终端上输入命令`git --version`查看git版本，若没有显示版本号说明没有安装git，若显示版本号则跳过这一步直接看配置信息。
    2. 对于Mac用户，使用XCode安装，在Preferences中的Downloads下找到Command Line Tools点击安装即可；或者使用homebrew，执行`brew install git`。
    3. 对于window用户，可以在官网[https://git-scm.com/downloads](https://link.zhihu.com/?target=https%3A//git-scm.com/downloads%EF%BC%8C%E5%A6%82%E4%B8%8B%E5%9B%BE%EF%BC%9A)下载，安装过程中默认勾选不要更改，PATH环境配置选择第二种便于之后在命令行使用git。

  - 配置个人信息

    这一步比较简单，设置用户名和注册邮箱，便于之后commit到记录，执行一下两步

    `git config --global user.name "你的名字"`

    `git config --global user.email "你的邮箱"`

  - 配置公私钥

    其实配不配公私钥都不影响后面的开发，不过为了节省一些输入账号密码的时间，可以先花几分钟完成这一步。

    1. 首先查一下自己的电脑是否之前生成过rsa_key，使用命令`cd ~/.ssh`，如果可以找到路径说明之前已生成过，直接看第 步。

    2. 使用命令`ssh-keygen -t rsa -C “邮箱地址”`生成公私钥，生成后会通知保存的文件路径在哪里，找到路径后会发现.ssh文件夹中有两个文件，有pub后缀的是公钥，没有后缀的是私钥。

       ⚠️ 生成过程中会出现设置私钥密码，个人建议直接回车处理，不然之后管理项目会重复多次输密码，比用 http 还烦。

    3. 使用命令`cat id_rsa.pub`将公钥打印到命令行上并复制，接着打开GitHub，找到settings下的SSH粘贴上去，标题随便取。

    4. 接下来就可以使用ssh免密拉取项目了。

  - 本地开发与提交

    在自己的计算机新建文件夹，用来存放项目，从项目的克隆开始说起。

    1. 在对应文件夹打开终端使用命令`git clone <url>`将项目克隆到本地。

    2. 接着使用自己喜欢的 IDE 完成自己对应的工作。在修改或增删完项目代码后，执行以下几步命令用于提交：

       ```git
       //创建新分支，注意必须先创建分支再提交
       $ git checkout -b "feature/XXX"
       
       //查看状态
       $ git status
       
       //逐一添加更改后的文件，注意最好不要使用"git add ."，避免提交不需要的测试文件
       $ git add 文件名
       //如果不小心add错了文件，使用下面的命令回退
       $ git reset HEAD
       
       //add完成后使用commit提交，XXXXXXX替换为新添加的功能，使用英文输入
       $ git commit -m "feature:XXXXXXX"
       ```

    3. commit后使用`git push`将项目推到GitHub上，这时可能会出现以下几种错误：

       - 当前分支落后最新版本

         (1) 使用 rebase 命令先变基并解决冲突后，再push  ==推荐使用这种方法====，命令会比较复杂一些==

         ```git
         //切换到主分支
         $ git checkout origin
         
         //拉取最新代码
         $ git pull
         
         //切换回开发分支
         $ git checkout feature/XXX
         
         //变基
         $ git rebase master
         
         //如果有冲突手动解决，解决后执行
         $ git rebase --continue
         
         //提交
         $ git push
         
         //如果提交失败使用强制提交
         $ git push -f
         ```

         (2) 使用 merge 命令先合并并解决冲突后，再push   ==比rebase容易理解，但会保留过多分支==

         ```git
         //拉取最新的主分支代码
         $ git fetch origin
         
         //根据此主分支新建临时分支
         $ git checkout -b tmp origin
         
         //对比主分支与临时分支的不同
         git diff feature/XXX tmp
         
         //切换回开发分支
         git checkout feature/XXX
         
         //合并分支
         git merge tmp
         
         //如果此时出现合并冲突，手动改掉冲突再执行以下命令
         git add 冲突文件
         git commit -m "feature:XXXXXXX"
         
         //提交
         git push
         ```

         (3) 在GitHub上拉取最新的版本并重新手动更改，再push

       - 当前分支与主分支没有建立联系，执行错误后面提示的命令

       - 其他错误一般是git的使用顺序不对或者操作失误等因素造成，百度一下

- ##### web

  ==明天再更==

#### 开发软件

在以上环境以及操作都熟悉后，就可以开始开发了，下面介绍开发工具，由于本人主要使用的是VsCode，所以主要介绍它的配置和使用。

- ##### VsCode

  安装就跳过了，没有安装过的可以在官网上下载。下面从几款开发使用的插件开始介绍。

  - git相关

    - Git History

      以图表的形式查看git日志，可以查看任意文件的更改记录。

    - GitLens

      提供内容改变前后的清晰对比。

    等等......

  - 前端相关

    - Atuo Rename Tag

      修改HTML标签，自动完成尾部闭合标签的同步修改。

    - fileheader

      `ctrl+alt+i`插入顶部注释模版，`ctl+s`自动更新最新修改时间，规范开发。

    - Code Runner

      运行代码片段，支持多种语言，方便调试。

    - CSS Peek

      在HTML文件里查看相应类的具体内容。

    - Quokka

      实时调试工具。

    - TODO Tree

      快速区分TODO部分。

    等等......

  - 项目打包相关

    - docker

  - 其他

    包括改变括号颜色或者更改字体等插件，按照自己的兴趣安装。

- ##### WebStorm

  据说很好用，但是要花钱，23333







### 任务

------

#### 界面

#### 前端

#### 后端



