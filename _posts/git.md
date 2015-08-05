title: git笔记
date: 2014-12-10
tags:
- git
categories: 技术记录
---
![](http://7xk15u.com1.z0.glb.clouddn.com/gitgit-t-shirt.png)

## 前言
Git 确实是很好的版本管理系统。有关其优点这里暂时不说了，网上也有很多相关资料介绍。
把这些记录下来方便以后查阅理解。

<!-- more -->

* 一些好的Git学习资源


>   * [Git分支管理策略](http://www.ruanyifeng.com/blog/2012/07/git.html)
  * [Pro Git books](http://www.git-scm.com/book/en/v2)
  * [Git交互学习](http://pcottle.github.io/learnGitBranching/?demo)
  * [专为设计师而写的GitHub快速入门教程](http://www.ui.cn/project.php?id=20957)
  * [GotGitHub](http://www.worldhello.net/gotgithub/)

**以下记录一些简单笔记，以便日后查阅**，当然要想系统的学习下Git原理可以参考上面列出的学习资源
![IMG](http://7xk15u.com1.z0.glb.clouddn.com/study664d3ba6-3cd0-49da-ac75-5f84ee155ab8.png)

##关于安装
请移步[Git安装](http://www.liaoxuefeng.com/wiki/0013739516305929606dd18361248578c67b8067c8c017b000/00137396287703354d8c6c01c904c7d9ff056ae23da865a000)
当然最好能在Linux下。
##创建版本库
* 通过***git init***命令将你要所在的当前目录变成Git可以管理的仓库；在当前目录下你能看到** .git**目录
* 一般你要将新写好的文件要加入该仓库管理时，用命令***git add youfile***
* 将上面加入仓库的文件提交到仓库，用命令***git commit -m "your annotation information"***；**注意**：-m 参数后面记得填写你修改的注释说明，方便别的开发者能阅读。
*  ***git status***命令可以随时查看仓库当前的状态，如有哪些文件更改了，哪些已经提交，哪些文件没有跟踪.


##操作远程仓库

一般可以自己搭建一个自己运行的Git服务器。如果没条件，就用[Github](https://github.com/)网站吧，一个提供仓库托管服务的网站，这里你可以将Github理解为Git服务器，但是它不免费提供私有的仓库。
所以，要是你的项目不公开的话，要么交点费用，要么自己搭建个Git服务器。
不多说

  * 首先在上面注册个账号，[我的账号](https://github.com/guxiaole)
  * 然后你“Create a new repo”创建一个新的仓库（我的新仓库 [COS-IIAPP](https://github.com/guxiaole/COS-IIAPP)  ），按照默认情况设置就可以了。
  * 关联你的本地仓库。**注意**：最好本地仓库名字与你在Github上面新建立的仓库名字一样。在本地仓库所在目录下运行命令：
  
	``` bash
	$ git remote add origin git@github.com:yourcount/hello-world.git
	```
 
   其中**origin**即为远程库

  * 将本地库的所有内容  推送远程库
  
	``` bash
	$ git push -u origin master
	```
 当然，如果你在本地创建了其他分支（不知道什么是分支？别急，要不你先看我后面介绍的分支吧），也可以推送，将master改为你要推送的分支名称即可。
你也可以从远程库clone到本地库，效果一样。
好了，到这步恭喜你，你现在可以看看你的github上面的是不是和你本地的项目一样呢！妈蛋！没有？？，好了忘记下面这一步了。
###创建SSH Key
对了，在这之前需要创建SSH Key，因为你的本地Git仓库和GitHub仓库之间的传输是通过SSH加密。

   ``` bash
	$ ssh-keygen -t rsa -C “youremali.com”
   ```
 

##并行开发
Git强大地方就在于它的多人共同开发了。
现在假设你的另外成员一起在分支***dev***开发一个项目.
>* 他使用**git clone git@github.com:guxiaole/COS-IIAPP.git **命令克隆到他本地仓库
* 他要创建远程***origin***的***dev***分支到本地,用这个命令**git checkout -b dev origin/dev**；
* 他很厉害，很快就在***dev***分支上开发了一个伟大的Idea， 推送到远程库 **git push origin dev**后他很幸福的去看苍老师的电影了；

这个时候，你很痛苦的加班加点在***dev***上修改，终于搞定时候，试图也推送到远程库，这个时候就会提示报错。。次奥，那小子比我快！
原因：推送失败，因为远程分支比你的本地更新。
解决办法：
 * 先用***git pull***试图合并;  **注意**:要是git pull提示“no tracking information”，则说明本地分支和远程分支的链接关系没有创建，用命令***git branch --set-upstream dev origin/dev***
 *  如果合并有冲突，则解决冲突，并在本地提交；
 * 没有冲突或者解决掉冲突后，再用git push origin dev推送

##分支的操作
* 默认master初始分支，一般比较稳定的项目版本在这个分支上，一旦开发出成熟的其他功能分支，测试稳定后再和此分支合并
 ![IMG](http://7xk15u.com1.z0.glb.clouddn.com/study7854057.png)

* 现在你需要和其他成员开发一个新的功能，一般新建一个分支，并很愉快的在上面进行修改提交。当然，这个时候还没有和主分支进行合并
  ![IMG](http://7xk15u.com1.z0.glb.clouddn.com/study7928033.png)

     ![IMG](http://7xk15u.com1.z0.glb.clouddn.com/study7917627.png)
 

* 这个时候，突然有人报告你发布的稳定版本master的一个bug需要修复，这个时候停下手头上进行的dev分支；转到master分支。

    ![IMG](http://7xk15u.com1.z0.glb.clouddn.com/study7976377.png)
 
* 新建一个bugfix分支，修改提交
![IMG](http://7xk15u.com1.z0.glb.clouddn.com/study8048294.png)
 

* bug搞定，合并到主分支

 ![IMG](http://7xk15u.com1.z0.glb.clouddn.com/study8275837.png)
![IMG](http://7xk15u.com1.z0.glb.clouddn.com/study8210348.png)
 
* 回到dev 分支，继续工作，发现dev 新功能完成，合并master分支
 ![IMG](http://7xk15u.com1.z0.glb.clouddn.com/study8288130.png)
 
*  对了，忘记bugfix分支此时可以删掉了。
![IMG](http://7xk15u.com1.z0.glb.clouddn.com/study8354337.png)
![IMG](http://7xk15u.com1.z0.glb.clouddn.com/study8360779.png)
 
* 另外
当手头工作没有完成时，先把工作现场***git stash***一下，然后去修复bug，修复后，再***git stash pop***，回到工作现场

##小结
最常用的Git命令差不多就这么多了，随着后面学习继续更新吧。。当然，要想要彻底 搞清楚git原理，还是系统看看相关书籍吧。
![IMG](http://7xk15u.com1.z0.glb.clouddn.com/study1eeac211-8695-4ede-a47c-546cd61e898e.png)
<!-- more -->
