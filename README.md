## Git与Github安装使用教程

#### 1. 什么是Git？  
- Git是目前世界上最先进的分布式版本控制系统（没有之一）。  
Git有什么特点？简单来说就是：高端大气上档次！

#### 2. Git与CSV及SVN区别  
- CVS及SVN都是集中式的版本控制系统，而Git是分布式版本控制系统  
集中式版本控制系统：版本库是集中存放在中央服务器的，而干活的时候，用的都是自己的电脑，所以要先从中央服务器取得最新的版本，然后开始干活，干完活了，再把自己的活推送给中央服务器。中央服务器就好比是一个图书馆，你要改一本书，必须先从图书馆借出来，然后回到家自己改，改完了，再放回图书馆。集中式版本控制系统最大的毛病就是必须联网才能工作，如果在局域网内还好，带宽够大，速度够快，可如果在互联网上，遇到网速慢的话，可能提交一个10M的文件就需要5分钟，这还不得把人给憋死啊。 
分布式版本控制系统：分布式版本控制系统根本没有“中央服务器”，每个人的电脑上都是一个完整的版本库，这样，你工作的时候，就不需要联网了，因为版本库就在你自己的电脑上。既然每个人电脑上都有一个完整的版本库，那多个人如何协作呢？比方说你在自己电脑上改了文件A，你的同事也在他的电脑上改了文件A，这时，你们俩之间只需把各自的修改推送给对方，就可以互相看到对方的修改了。和集中式版本控制系统相比，分布式版本控制系统的安全性要高很多，因为每个人电脑里都有完整的版本库，某一个人的电脑坏掉了不要紧，随便从其他人那里复制一个就可以了。而集中式版本控制系统的中央服务器要是出了问题，所有人都没法干活了

#### 3. 配置Git环境  
#### *Linux系统*
- Debian或Ubuntu Linux
```
$ sudo apt-get install git
```
- 老版本Debian或Ubuntu Linux
```
$ sudo apt-get install git-core	
```
- 其他版本Linux，官网下载源码解压，然后依次输入
```
$ ./config ——> make ——> sudo make install
```
#### *Windows系统*
- [官网下载](https://git-scm.com/downloads)安装完成后，找到 Git Bash 打开即可

#### *Mac系统*
- 首先看看自己有没有安装Git，终端terminal输入命令
```
$ git
The program 'git' is currently not installed. You can install it by typing:
sudo apt-get install git
```
- 推荐从AppStore安装Xcode，Xcode集成了Git，不过默认没有安装，你需要运行Xcode，选择菜单“Xcode”->“Preferences”，在弹出窗口中找到“Downloads”，选择“Command Line Tools”，点“Install”就可以完成安装了。Xcode是Apple官方IDE，功能非常强大，是开发Mac和iOS App的必选装备，而且是免费的！查看Git版本：
```
$ git --version
git version 2.14.3 (Apple Git-98)
```

- 安装完成后需要进行一些设置，完善个人信息，命令行输入以下命令：
```
$ git config --gloabal user.name "your name"
$ git config --global user.email "your email"
```
- 对应地方分别替换成你的名字和邮箱

#### 4. 创建版本库（仓库）  
- 什么是版本库呢？版本库又名仓库，英文名repository，你可以简单理解成一个目录，这个目录里面的所有文件都可以被Git管理起来，每个文件的修改、删除，Git都能跟踪，以便任何时刻都可以追踪历史，或者在将来某个时刻可以“还原”。
所以，创建一个版本库非常简单，首先，选择一个合适的地方，创建一个空目录：
```
$ mkdir demo
$ cd demo
```
- 第二步初始化版本库，把这个目录变成Git可以管理的仓库： (Windows系统请确保目录名（包括父目录）不包含中文)
```
$ git init
Initialized empty Git repository in /Users/admin/Documents/demo/.git/
```
- 瞬间Git就把仓库建好了，而且告诉你是一个空的仓库（empty Git repository），细心的读者可以发现当前目录下多了一个.git的目录，这个目录是Git来跟踪管理版本库的，没事千万不要手动修改这个目录里面的文件，不然改乱了，就把Git仓库给破坏了。  
如果你没有看到.git目录，那是因为这个目录默认是隐藏的，用ls -a命令就可以看见。
```
$ ls -a
. .. .git
```

#### 5. 添加文件
- 在该仓库中添加一个文件
```
$ echo "this is a demo repo" >> readme.txt
$ ls -l
total 8
-rw-r--r--  1 qw  staff  20  4 12 16:30 readme.txt
```
- 上面是一个简单的linus命令，向 readme.txt(没有就创建)追加内容，然后查看当前路径下的文件是否存在。我们可以随时使用 git stastus 查看当先仓库的状态：
```
$ git status
On branch master

No commits yet

Untracked files:
(use "git add <file>..." to include in what will be committed)

	readme.txt

nothing added to commit but untracked files present (use "git add" to track)
```
- 上面一大串的意思就是，我们目前在主分支上（master），还没有提交过任何东西。本地有一个新增的文件readme.txt，但是还没有被追踪（没有被添加），需要使用git add命令添加它。

- 文件的位置我们可以理解在这三个地方变化，1.本地临时的，2.暂存区的，3仓库中的。本地的需要先添加到暂存区中，最后提交到到仓库中，这个完整过程才算是把一个文件正确的添加在仓库中。  
```
$ git add readme.txt
```
- 执行添加命令，没有任何提示信息，就表示成功了，Unix的哲学是“没有消息就是好消息”，此时文件已经到暂存区中。
```
$ git status
On branch master

No commits yet

Changes to be committed:
(use "git rm --cached <file>..." to unstage)

	new file:   readme.txt
```
- 查看仓库状态，提示我们有一个新文件 readme.txt 需要提交。
```
$ git commit -m "upload a file"
[master (root-commit) 38b00ae] upload a file
1 file changed, 1 insertion(+)
create mode 100644 readme.txt
```
- 提交文件成功。该命令会把所有在暂存区中的文件都提交到仓库，参数 -m(essage)是要填写本地提交的信息，通俗的说就是要打个log，方便别人跟自己以后查看，回滚定位用。
```
$ git log 
commit 38b00ae6dcfadc59a728c10519c1a3f0d79fbbd7 (HEAD -> master)
Author: qiuwen <275894155@qq.com>
Date:   Fri Apr 12 16:46:35 2019 +0800

	upload a file
```
-  此时再查看仓库状态，会显示没有需要提交的，工作区是干净的
```
$ git status
On branch master
nothing to commit, working tree clean
```
- 我们修改readme.txt 文件内容，并查看修改了什么
```
$ echo "add new content" >> readme.txt
$ git diff
diff --git a/readme.txt b/readme.txt
index 3f54689..f0848ff 100644
--- a/readme.txt
+++ b/readme.txt
@@ -1 +1,2 @@
 this is a demo repo
+add new content
```
- 输出显示：我们修改了这个文件 并新增了一行，这个命令是比较工作区与暂存区（即上次git add的内容）的不同。


 - *为什么Git添加文件需要add，commit一共两步呢？因为commit可以一次提交很多文件，所以你可以多次add不同的文件 如：*
 ```
$ git add file1.txt
$ git add file2.txt file3.txt
$ git commit -m "upload 3 files"
 ```

#### *6. 创建远程仓库（以Github为例）*
- 默认已经有Github账号，没有[点击这里](https://git-scm.com/)注册一个。
#### *创建 SSH Key*

Git使用https协议，每次拉取、推送都要输入密码很麻烦，使用git协议，然后使用ssh密钥，这样可以省去每次都输密码。服务器把我们的公钥添加到他们的，这样每次我与服务器交互时服务器会用它绑定的公钥与我们本地的公钥对比，如果匹配，操作成功；如果不匹配，操作失败。大多数Git服务器都会选择使用 SSH 公钥来进行授权，系统中的每个用户都必须提供一个公钥用于授权，没有的话就要生成一个。

- 创建 SSH Key （这里的邮箱必须是你注册Github绑定的邮箱）
```
$ ssh-keygen -t rsa -C "your email"
```
- 之后会要求确认路径和输入密码，其他执行命令后一路回车就行。成功的话会在~/下生成.ssh文件夹，进去，打开id_rsa.pub，复制里面的key
```
$ cd ~/.ssh
$ ls 
id_rsa(私钥不能泄露)		id_rsa.pub(公钥可公开) 
$ cat id_rsa.pub
ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABAQDECKTHqNIvHHPuyTtmau+vt8aR64DL2V8JhN2F/nE7lQKTv7N5g2s6fx1mGpndpXxK5i+YZv5FUpmlkMaMnr6SahygvheJoktRdskzlHETEDe6cnj9SXY1L1UdfmcE3s1GpICD7V6shUwhFm9sDBZfB2j8E+Ba1ZhYLrcOAoFrCFkWJLvAIwF2RCQt+32lI63EDz99rG1pUEvYGfiyR7cedf5F+0lYFJ4ojjBn7pPSVd4w8lJ25lD1QP5zc2VjTXVyECLEwyFdXin5Y9fUHpUzJBiCtdT7hjfOR30ahdsW3IgPFMGo7tSBvUKqeqEEn+J+5hBpKL/9/NN6UC2Zr9Bd 275894155@qq.com
```
- cat打印公钥，复制里面的的一大串，网站登录Github上，进入 Account Settings（账户配置），左边选择SSH Keys，Add SSH Key，title随便填，粘贴在你电脑上生成的key。

- 为了验证是否成功，在git bash下输入：
```
$ ssh -T git@github.com
```
- 如果是第一次的会提示是否continue，输入yes就会看到：You've successfully authenticated, but GitHub does not provide shell access 。这就表示已成功连上github。接下来我们要做的就是把本地仓库传到Github上去，在此之前还需要设置username和email，因为github每次commit都会记录他们（如果已经设置过了，可以忽略这步），对应地方分别替换成你的名字和邮箱。
```
$ git config --gloabal user.name "your name"
$ git config --global user.email "your email"
```
#### *关联远程仓库*
- 进入到刚才的仓库

- 关联远程仓库（远程库默认名字为origin）
首先需要在github网站上创建一个空的仓库，登录github后在页面右侧自己的头像旁边点击加号选择第一个 new repository，填写 repository name:demo，选择Public，然后点击最下面绿色按钮 Create repository后成功创建一个空仓库,最后在终端中运行下面命令:
```
$ git remote add origin https://github.com/yourusername/demo.git
```
- 第一次推送到GitHub 后续推送（不再使用参数-u）
```
$ git push -u origin master 
warning: redirecting to https://github.com/yourusername/demo.git/
Enumerating objects: 6, done.
Counting objects: 100% (6/6), done.
Delta compression using up to 4 threads
Compressing objects: 100% (2/2), done.
Writing objects: 100% (6/6), 465 bytes | 155.00 KiB/s, done.
Total 6 (delta 0), reused 0 (delta 0)
To http://github.com/yourusername/demo.git
 * [new branch]      master -> master
Branch 'master' set up to track remote branch 'master' from 'origin'.
```
- 成功后会出现上面一串描述，第一次会有警告，不必理会，之后会消失。现在刷新你的github网站，会发现你创建的readme.txt文件，至此，本地仓库与远程github仓库连接成功。  
我们修改一下文件，再推送到github上：
```
$ echo "this is third modify" >> readme.txt
$ git add readme.txt
$ git commit -m "update file third"
```
- 此时我们更新github网站，发现并没有我们刚才添加的那句话，那是因为我们只是把它推到了本地的仓库上，没有推送到远程github库上，执行下面命令：
```
$ git push origin master
```
- 再次更新github后，发现我们添加的那句话已经出现。



- 从远程库克隆
```
$ git clone https://github.com/username/repositoryname.git
```






- 什么是Github？  
引用菜鸟上的一句话：如果你是一枚Coder，但是你不知道Github，那么我觉的你就不是一个菜鸟级别的Coder，因为你压根不是真正Coder，你只是一个Code搬运工。




[Git教程](https://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000/001373962845513aefd77a99f4145f0a2c7a7ca057e7570000)

- 1 [github教程](http://www.runoob.com/w3cnote/git-guide.html)
 
2 [git下载官方网址](https://git-scm.com/download/win)

3 [git安装详情](https://blog.csdn.net/xunhuanxiaogongzhu/article/details/80240078)

4  [git官网](https://git-scm.com/)

5 [git-github上教程](https://github.com/geeeeeeeeek/git-recipes/wiki)

6 [GIT为什么要配置公钥和私钥](https://www.jianshu.com/p/e93edea128a3)

7 [github上教程](https://github.com/geeeeeeeeek/git-recipes/wiki)

8 ! [github图标](http://i1.pcplus.fd.pchome.net/g1/M00/10/07/ooYBAFV_kTWIIKBHAACLcbG0bQkAACixwBtWesAAIuJ777.png)

9 [0基础的git教程，傻瓜都会用的Github Desktop](https://www.jianshu.com/p/06a960d991aa)

 10 [Git环境下载](https://git-scm.com/downloads)


参考资料（侵删）  
*参考资料1 [菜鸟教程·Github简明教程](http://www.runoob.com/w3cnote/git-guide.html)*

*参考资料2 [在线学习git命令](https://learngitbranching.js.org/?demo)*
