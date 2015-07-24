title: About hexo
date: 
tags:
- hexo
- 技术记录
categories: 技术记录
---

## what is hexo
Hexo 是一个快速、简洁且高效的博客框架。Hexo 使用 Markdown（或其他渲染引擎）解析文章，在几秒内，即可利用靓丽的主题生成静态网页。

<!-- more -->

###安装hexo
* [Node.js](http://nodejs.org/)
* [Git](http://git-scm.com/)

上面程序安装完成，接下来只需要使用 npm 即可完成 Hexo 的安装。
``` bash
$ npm install -g hexo
```
###创建项目

	bash $ hexo init nodejs-hexo


###启动服务

	bash $ hexo server


接下来只需在本地浏览器打开 [http://localhost:4000](http://localhost:4000)

## how to deploy on the github web
###创建github repository
注意repository名字为*guxiaole.github.io*；前面换成自己的github账户名且全部***小写***
###配置_config.yml文件
```
deploy:
  type: git
  repository: git@github.com:guxiaole/guxiaole.github.io.git
  branch: master
```

之后执行下列指令即可完成部署

```bash
$ hexo clean
$ hexo generate
$ hexo deploy

```
接下来只需在浏览器打开 [guxiaole.github.io](guxiaole.github.io)

### 创建新文章
创建第一博客文章。Hexo建议通过命令行操作，当然你也可以直接在_posts目录下创建文件。

``` bash
$ hexo new 搭建hexo静态博客
``` 

##hexo资源
### [hexo主题](https://github.com/hexojs/hexo/wiki/Themes)