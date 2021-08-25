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

    这一步比较简单，设置用户名和注册邮箱，便于之后commit到记录，执行以下两步

    ```git
    git config --global user.name "你的名字"
    git config --global user.email "你的邮箱"
    ```

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

         (1) 使用 rebase 命令先变基并解决冲突后，再push  ==推荐使用这种方法，命令会比较复杂一些==

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
    
    4. push后终端会出现一个网址，点击进去后提交pull request，最后由项目管理者决定代码的并入与否。

- ##### web

  开发语言主要是JS，HTML，CSS，Python，SQL等，下面从数据库的安装和配置开始说起。

  - SQL

    - **安装**  数据库类型有很多种，我们使用最常见的Mysql，Windows系统下首先在终端cmd中使用命令`services.msc`查询自己是否安装过，如果在弹出的服务页面找到了Mysql说明之前已经安装成功，若没有出现可以参考博客[Windows下安装MySQL详细教程 - m1racle - 博客园 (cnblogs.com)](https://www.cnblogs.com/zhangkanghui/p/9613844.html)安装。

    - **语法**  SQL语法比较复杂，在这里介绍一些常用的命令。

      ```sql
      //Windows
      //连接Mysql
      net start mysql
      
      //sql操作与Mac相同
      
      //关闭Mysql
      net stop mysql
      
      
      
      //Mac
      //开启Mysql服务器
      brew services start mysql
      
      //初次使用时设置密码
      mysqladmin -u root password 'xxxxxxxx'
      
      //连接Mysql
      mysql -u root -p
      
      //一些SQL操作
      mysql> show databases;
      mysql> create database test;
      mysql> use test;
      mysql> create table student(
      				-> id int primary key auto_increment,
      				-> name varchar(20),
        			-> sex varchar(2)
      				);
      mysql> desc student;
      
      //搜索
      mysql> SELECT id,name FROM student;
      mysql> SELECT * FROM student;
      mysql> SELECT DISTINCT sex FROM student;
      mysql> SELECT * FROM student WHERE sex='0' OR sex='1';
      mysql> SELECT * FROM student ORDER BY id;
      
      //插入,id自动更新不要插入指定值
      mysql> INSERT INTO student (name,sex)
      				-> VALUES('xxx','x');
      mysql> INSERT INTO student (sex)
      				-> VALUES('x');
      
      //修改,没有WHERE字段的UPDATE会将所有数据改掉
      myaql> UPDATE student SET sex='x' WHERE name='xxx'
      
      //删除
      mysql> DELETE FROM student WHERE name='xxx' AND sex='x'
      mysql> DELETE FROM student;
      
      //删除表并退出
      mysql> DROP TABLE student;
      mysql> drop database test;
      mysql> quit
      
      //关闭Mysql服务器
      brew services stop mysql
      ```

    - **连接**  由于本次后端采用flask框架，所以使用python连接数据库，具体操作可以参考[python web框架flask连接mysql数据库操作_29DCH的博客-CSDN博客_python的flask框架连接mysql数据库](https://blog.csdn.net/CowBoySoBusy/article/details/82712421)

    - **可视化**  可以下载Mysql可视化工具辅助操作，按照自己的喜好下载工具；也可以不下载额外工具只在命令行中查看数据库内容。当然，推荐安装一个可视化工具。

  - Python

    本项目后端使用python + flask开发，python3版本自由选择，flask教程自学（摊牌了，本人不会www）

  - JS，HTML，CSS

    - 使用Vue

      本项目前端使用Vue框架，使用Vue框架可以采用多种方式，推荐直接下载Vue.js并在文件中引入，下载地址为[安装 — Vue.js (vuejs.org)](https://cn.vuejs.org/v2/guide/installation.html)选择“开发版本”进行下载。

      ```html
      <!--引用格式-->
      <script src="vue.js" type="text/javascript" charset="utf-8"></script>
      ```

    - 文件分离

      Vue项目正常创建都是将js，html和css合并在一个文件中，虽然看起来比较方便但是当功能日趋完善时会给调试带来麻烦，所以我们可以借鉴无框架开发时的文件分离方法，每个界面分成三个文件开发，便于维护和管理。

      ```html
      //在.vue文件中设置如下
      <template src="./***.html"></template>
      <script src="./***.js"></script>
      <style src="./***.css"></style>
      
      //在.js文件设置如下
      import record from './***.vue';
      export default record;
      ```

    - 个人开发

      其实在具体前端开发过程中，可以使用框架也可以不使用，而且在同一项目中可以有文件使用Vue也可以有文件不使用，是兼容的。框架只是提升了底层的高度让我们可以不关注DOM的操作而只关注逻辑本身。如果不熟悉Vue可以在官网上看一下不到两小时的简洁介绍，以便更好上手。

    - 实际开发

      在本次项目中，我们使用Vue CLI，它是一个基于Vue.js进行快速开发的完整系统，使用Vue脚手架之后我们开发的将是一个完整项目而不再是单一页面再手动整合。对于初学Vue的人来说学习成本比较高，（不过还好我会一点点🤏），下面先介绍一下Vue CLI的优势。

      1. 配置方便  只需要执行命令就能下载相关依赖，比如我们要用一些官方的CSS，借助它就可以快速使用。
      2. 开发方便  之前开发单页面时我们需要引入vue.js,vue-router等文件，现在Vue CLI将他们都包含了进来；除此之外还可以方便地使用很多官方插件等。

      接着就是Vue CLI的安装和配置了

      1. 环境准备

         - 安装node.js

           先使用命令`node -v`查看之前是否安装过，如果出现版本号则跳过此步。如果没有出现：

           对于Windows系统，在官网中[Download | Node.js (nodejs.org)](https://nodejs.org/en/download/)下载安装，需要手动配置环境变量，在环境变量中添加以下配置：

           ```
           NODE_HOME = nodejs安装目录
           PATH = %NODE_HOME%
           ```

           对于Mac系统在官网下载pkg文件，不需手动配置。

           这时再使用命令`node -v`，如果出现版本号说明环境已经配置成功。

         - npm介绍

           npm是node.js的包管理工具，如今的npm可以对现在主流的前端技术进行管理，在上面安装步骤后npm已经随之安装好了，下面安装脚手架等步骤都需要用到npm。

           由于npm中心仓库在国外，所以在安装之后的内容之前，最好先配置一下淘宝的镜像：

           ```shell
           //配置镜像
           npm config set registry https://registry.npm.taobao.org
           
           //验证是否配置成功
           npm config get registry
           ```

           配置镜像后，我们最好再修改一下npm安装位置，这样可以利用本地缓存，不需要每次使用都去调动远程仓库：

           ```shell
           //Windows
           npm config set prefix "D:\nodejs\node_modules\node_global"
           npm config set cache "D:\nodejs\node_modules\node_cache"
           
           //Mac
           npm config set prefix "/Users/hanjiajun/dev/nodereps/node_global"
           npm config set cache "/Users/hanjiajun/dev/nodereps/node_cache"
           
           //查看是否更改成功
           npm config get prefix
           npm config get cache
           ```

      2. 安装脚手架

         我们使用v2版本开发，所以如果之前有下载过最新版本先使用下列命令删除

         ```shell
         npm uninstall -g @vue/cli
         ```

         安装命令为

         ```shell
         npm install -g vue-cli
         ```

      3. 开发项目

         ```shell
         //创建项目
         vue init webpack Paid_Q-A
         
         //以上只是介绍一个vue-cli，项目我已经创建好放到GitHub上了，所以大家不需要再重新创建了
         ```

         接下来简单介绍项目框架和流程

         ```markdown
         # 1. 框架
         	Paid_Q-A    ---------------->项目名
         		-build    ---------------->使用webpack打包使用build依赖
         		-config   ---------------->项目配置
         		-node-modules   ---------->管理项目依赖
         		-src      ---------------->写源代码
         			assets  ---------------->存放静态资源【‼️】
         			components    ---------->书写Vue组件【‼️】
         			router  ---------------->配置项目路由【‼️】
         			App.vue ---------------->项目根组件【‼️】
         			main.js ---------------->项目主入口【‼️】
         		-static   ---------------->其他静态
         		-.babelrc ---------------->将ES6转为ES5
         		-.editorconfig   --------->项目编辑配置
         		-.gitignore      --------->git版本忽略文件
         		-.postcssrc.js   --------->源码相关js
         		-index.html      --------->项目主页
         		-package-lock.json    ---->加锁文件
         		-package.json    --------->类似于依赖管理，不要修改
         		-README.md       --------->说明文件
         # 2. 运行项目
         	git clone之后的项目不包含node-modules，首先在终端中cd到项目文件夹，再执行npm install得到node-modules本地项目依赖后再进行下一步
         	在项目的根目录中执行 npm start
         	访问项目直接点击执行后输出的地址
         # 3. 项目开发方式
         	之前前端开发方式，一切皆组件，一个组件中包含了js代码、html代码和css样式。
         	
         	在vue-cli的开发方式中，实际是开发一个一个组件来实现一个一个功能模块，最后整合形成前端系		统。
         	因此在项目中可以将每个.vue文件看成一个具有独立功能的模块，它整合了js代码、html代码和css	样式，当然之前也提到过分离的思想，各有利弊。
         ```
         
      4. 在项目中使用axios
      
         ```markdown
         # 1. 安装axios
         	npm install axios --save-dir
         # 2. 配置main.js引入axios
         	import axios from 'axios'
         	Vue.prototype.$http = axios;
         # 3. 使用axios
         	在需要发送一步请求的位置：this.$http.get('url').then((res)=>{});
         # 4. 以上安装和配置我已经在项目中更新过了，所以只关注第三步使用即可
         ```
      
         由于axios要用到后端数据，为了提高开发效率和速度，前后端需要分离，淘宝有一个免费网站[RAP接口管理平台 (taobao.org)](http://rap2.taobao.org/)可以自定义接口和内容，方便前端开发，之后后端开发出类似接口再替换url即可。
      
      5. 在项目中使用Element UI
      
         ```markdown
         # 1. 安装Element UI
         	Element UI就是基于Vue的一个UI框架，提供了各种组件，可以快速开发页面。（自己开发页面真的很累很费时间，借助开源框架可以快速创建出比较好看的界面，当然非常炫酷的组件还是需要DIY的）
         	执行npm i element-ui -S
         # 2. 配置main.js引入Element UI
         	import ElementUI from 'element-ui';
         	import 'element-ui/lib/theme-chalk/index.css';
         	Vue.use(ElementUI);
         # 3. 使用Element UI
         	具体组件的使用可以查看下面的官方文档，其次我也写了几个基于Element UI设计的界面，也可以参考这开发新页面：
         	https://element.eleme.cn/#/zh-CN/component/installation
         # 4. 以上安装和配置我已经在项目中更新过了，所以只关注第三步使用即可
         ```
      
      6. 在项目中使用TailWind CSS
      
         这个配置浪费了我两个小时的时间，tailwind主要是将一些常见css封装了起来，可以不写css光使用HTML实现各式各样的样式，但是有了Element UI其实我们也不需要写多少css，甚至不需要写多少html，因此最后我放弃了引入TailWind CSS。（好吧，其实是我配置失败了，就先这样吧，之后要是基础开发结束想试一下tailwind再替换也不迟）

#### 开发软件

在以上环境以及操作都熟悉后，就可以开始开发了，下面介绍开发工具，由于本人主要使用的是VsCode，所以主要介绍它的配置和使用。

- ##### VsCode

  安装就跳过了，没有安装过的可以在官网上下载。下面从几款开发使用的插件开始介绍。

  - git相关

    - Git History

      以图表的形式查看git日志，可以查看任意文件的更改记录。

    - GitLens

      提供内容改变前后的清晰对比，查看更改记录。

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

  在开发过程中有几个需要强调的点：

  1. 项目开发遵循给定架构，各种不同后缀文件按照项目的实例放置以便管理调试。下方任务部分会给出设计原型图作为开发参考（如果我还有时间设计原型图的话），除此之外，可以使用部分开源代码或组件，但一定要在文件头部注释处标明以便最后汇总。
  2. 一切以实际为主，功能大于表面，界面的美观固然很重要但是功能的实现更重要，而且不要为了丰富功能去实现功能，要思考产品在现实生活中确切需要解决的问题是什么，如果我们作为用户最想体验到的是什么，优先解决这些问题。

- ##### WebStorm

  据说很好用，但是要花钱，23333

- **Pycharm**

  前端使用VsCode足够了，这里考虑到使用flask框架开发后端，所以Pycharm还是很方便的，可以快速创建一个flask项目，完成连接数据库、开发API的工作。

  当然使用VsCode也可以完成以上这些内容。







### 任务

------

本项目共分为两个系统，一个是问题审核系统，一个是付费问答系统，现在的计划是这两个系统独立开发，即开发两个Web应用。

出于前后端分离，界面分离的设计思想，每个Web应用的开发任务共分为界面、前端、后端三部分，最后整理打包任务量较小，暂且不做划分。下面开始任务拆解。

#### 界面

- 问答系统
  1. 登陆注册页面
     - [ ] 登陆页组件
     - [ ] 注册页组件
     - [ ] 找回密码组件
     - [ ] 密码可见选择组件
     - [ ] 邮箱注册验证码组件
  2. 主界面
     - [ ] 个人头像与昵称显示
     - [ ] 提问组件
     - [ ] 回答组件
     - [ ] 订单组件
     - [ ] 设置组件
     - [ ] 聊天组件
     - [ ] 余额与充值组件
     - [ ] 用户升级组件
  3. 提问界面
     - [ ] 搜索答主组件
     - [ ] 推荐形式组件
     - [ ] 答主展示组件
     - [ ] 展示方式组件
  4. 回答界面
     - [ ] 
  5. 订单界面
     - [ ] 
  6. 聊天界面
     - [ ] 
  7. 余额与充值界面
     - [ ] 
  8. 用户升级界面
- 审核系统
  1. 登陆页面
     - [ ] 登陆页组件
     - [ ] 密码可见选择组件
     - [ ] 找回密码组件
  2. 

#### 前端

- 问答系统
  1. 登陆注册功能
     - [ ] 对接后端API登陆
     - [ ] 对接后端API注册
     - [ ] 对接后端API找回密码
     - [ ] 对接后端API验证码
  2. 主界面
     - [ ] 提问、回答、订单、设置的切换逻辑
     - [ ] 余额与充值逻辑
     - [ ] 用户升级逻辑
  3. 提问功能
     - [ ] 搜索答主逻辑
     - [ ] 推荐排序逻辑
     - [ ] 展示逻辑
  4. 回答功能
     - [ ] 
  5. 订单功能
     - [ ] 
  6. 聊天功能
     - [ ] 
  7. 余额与充值功能
     - [ ] 
  8. 用户升级功能
- 审核系统
  1. 登陆功能
     - [ ] 对接后端API登陆
     - [ ] 对接后端API找回密码
  2. 

#### 后端

- 问答系统
  1. 登陆注册功能
     - [ ] 数据库对接登陆
     - [ ] 数据库对接注册
     - [ ] 数据库对接找回密码
     - [ ] redis对接验证码注册
  2. 主界面
     - [ ] 
  3. 提问功能
     - [ ] 
  4. 回答功能
     - [ ] 
  5. 订单功能
     - [ ] 
  6. 聊天功能
     - [ ] 
  7. 余额与充值功能
     - [ ] 
  8. 用户升级功能
- 审核系统
  1. 登陆功能
     - [ ] 数据库对接登陆
     - [ ] 数据库对接找回密码
  2. 

#### 打包



