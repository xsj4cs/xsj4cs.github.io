title: hexo搭建
tags: "nothing"
---
# 1.安装
## 1.1 安装git
## 1.2 安装node.js
## 1.3 安装hexo,并启动
```	bash
npm install -g hexo
mkdir xxx
hexo init xxx
cd xxx
npm install
hexo g
hexo s
```
访问localhost:4000
# 2.配置
## 2.1选个主题
原来主题太难看，用个next主题吧，地址：https://github.com/iissnan/hexo-theme-next
下载后解压到themes文件夹中，
然后站配置文件中，themes后面写上对应的名字
## 2.1主题配置
### 2.1.1语言：
编辑 站点配置文件 的 _config.yml ，将 language 字段更改为你所需要的语言版本代号：
``` bash
language: en
# language: zh-Hans
# language: fr-FR
# language: zh-hk
# language: zh-tw
# language: ru
# language: de
```
### 2.1.2标签：
新建一个页面，命名为 tags 。命令如下：
``` bash
hexo new page "tags"
```
编辑刚新建的页面，将页面的类型设置为 tags ，主题将自动为这个页面显示标签云。页面内容如下：
``` bash
title: Tagcloud
date: 2014-12-22 12:39:04
type: "tags"
---
```
注意：如果有启用多说 或者 Disqus 评论，默认页面也会带有评论。需要关闭的话，请添加字段 comments 并将值设置为 false，如：
``` bash
title: Tagcloud
date: 2014-12-22 12:39:04
type: "tags"
comments: false
---
```
在菜单中添加链接。编辑 主题配置文件 ，添加 tags 到 menu 中，如下:
``` bash
menu:
  home: /
  archives: /archives
  tags: /tags
```
### 2.1.3分类
同标签一样

### 2.1.4代码高亮主题

NexT 使用 Tomorrow Theme 作为代码高亮，共有5款主题供你选择。

默认使用的是白色的 normal
### 2.1.5站点建立时间

这个时间将在站点的底部显示，例如 © 2013 - 2015

编辑 站点配置文件，新增字段 since。

since: 2013
### 2.1.5数学公式显示

NexT 借助于 MathJax 来显示数学公式，此选项默认关闭。

编辑 主题配置文件，将 mathjax 设定为 true 即可。
``` bash
# MathJax Support
mathjax:
ProTip: 使用七牛 CDN 来加速 MathJax 脚本的加载
```

### 2.1.6侧边栏头像

编辑 站点配置文件，新增字段 avatar， 值设置成头像的链接地址。

其中，头像的链接地址可以是：

完整的互联网 URL，例如：https://avatars1.githubusercontent.com/u/32269?v=3&s=460
站点内的地址，例如：

/uploads/avatar.jpg 需要将你的头像图片放置在 站点的 source/uploads/（可能需要新建uploads目录）
/images/avatar.jpg 需要将你的头像图片放置在 主题的 source/images/ 目录下。
### 2.1.7侧边栏社交链接

编辑 站点配置文件，新增字段 social，然后添加社交站点名称与地址即可。例如：
``` bash
# Social links
social:
  github: https://github.com/your-user-name
  twitter: https://twitter.com/your-user-name
  weibo: http://weibo.com/your-user-name
  douban: http://douban.com/people/your-user-name
  zhihu: http://www.zhihu.com/people/your-user-name
  #等等
```
### 2.1.8About页面

新建一个 about 页面：

hexo new page "about"
菜单显示 about 链接，在 主题配置文件 设置中将 menu 中 about 前面的注释去掉即可。
``` bash
menu:
  home: /
  archives: /archives
  tags: /tags
  about: /about
```
### 2.1.9友情链接

编辑 站点配置文件 添加：
``` bash
# title, chinese available
links_title: Links
# links
links:
  MacTalk: http://macshuo.com/
```
### 2.1.10腾讯公益404页面

简体中文增加腾讯公益404页面，寻找丢失儿童，让大家一起关注此项公益事业！效果如下 http://www.ixirong.com/404.html

使用方法，新建 404.html 页面，放到主题的 source 目录下，内容如下：
``` html
<!DOCTYPE HTML>
<html>
<head>
  <meta http-equiv="content-type" content="text/html;charset=utf-8;"/>
  <meta http-equiv="X-UA-Compatible" content="IE=edge,chrome=1" />
  <meta name="robots" content="all" />
  <meta name="robots" content="index,follow"/>
</head>
<body>

<script type="text/javascript" src="http://www.qq.com/404/search_children.js" charset="utf-8" homePageUrl="your site url " homePageName="回到我的主页"></script>

</body>
</html>
```
# 3.远程连接
## 3.1 github上
下面我们讲博客部署到github上面。

注册Github帐号。

已有就跳过。

这里的就不用介绍了。

创建repository

登录github后，将鼠标点击github右上角“+”号，在下拉菜单上，选择“New repository”项，将跳到如下页面，填写库名称，勾选“Initialize this repository with a README”，点击“create repository”，即可完成创建库。

由于你的本地Git仓库和GitHub仓库之间的传输是通过SSH加密的，所以，需要一点设置：

第1步：创建SSH Key。在用户主目录下，看看有没有.ssh目录，如果有，再看看这个目录下有没有id_rsa和id_rsa.pub这两个文件，如果已经有了，可直接跳到下一步。如果没有，打开Shell（Windows下打开Git Bash），创建SSH Key：
``` bash
$ ssh-keygen -t rsa -C "youremail@example.com"
```
你需要把邮件地址换成你自己的邮件地址，然后一路回车，使用默认值即可，由于这个Key也不是用于军事目的，所以也无需设置密码。

如果一切顺利的话，可以在用户主目录里找到.ssh目录，里面有id_rsa和id_rsa.pub两个文件，这两个就是SSH Key的秘钥对，id_rsa是私钥，不能泄露出去，id_rsa.pub是公钥，可以放心地告诉任何人。

第2步：登陆GitHub，打开“Account settings”，“SSH Keys”页面：

然后，点“Add SSH Key”，填上任意Title，在Key文本框里粘贴id_rsa.pub文件的内容：

点“Add Key”，你就应该看到已经添加的Key

部署到github上时修改_config.yml最后 
``` bash
deploy: 
type: git 
repository: git@github.com:nichunquan/nichunquan.github.io.git 
branch: master
```
deploy的type改成git，然后运行下
``` bash
npm install hexo-deployer-git --save

hexo g
hexo d
```
##3.2恢复
因为发布上去的并不是源文件markdown什么，而是html之类的文件，所以一旦markdown文件不见了就不能继续更新了，现在我们要在创建一个分支用来存markdown文件，可以是hexo
``` bash
git branch hexo
git checkout hexo
```
恢复脚本如下：
``` bash
git remote rm origin
git remote add origin git@github.com:xsj4cs/xsj4cs.github.io.git
git checkout hexo

do some thing
git add .
git commit -m
git push origin hexo
hexo g
hexo s
hexo d
```
