---
title: blog
categories: hexo
tags:  Hexo usage_methods and problems 
# permalink: /posts/hexo-blog
---
<!-- Welcome to [Hexo](https://hexo.io/)! This is your very first post. Check [documentation](https://hexo.io/docs/) for more info. If you get any problems when using Hexo, you can find the answer in [troubleshooting](https://hexo.io/docs/troubleshooting.html) or you can ask me on [GitHub](https://github.com/hexojs/hexo/issues). -->

## 如何使用Github 部署静态博客HEXO ？

（详细步骤）可参考 (https://tech.yemengstar.com/hexo-tutorial-deploy-githubpages-beginner/#header-id-9)

### Hexo 博客文件夹目录结构

_config.yml    --网站的配置信息
package.json   --应用程序的信息
scaffolds      --模版文件夹
source         --存放用户资源, Markdown 文档
themes         --主题文件夹
public         --网站文件

### Hexo全局配置文件_config.yml 
详情可参考(https://hexo.nodejs.cn/docs/configuration.html)



##  如何新建一个博客，并部署（deploy）到远程网站github ?
### Create a new post

``` bash
$ hexo new "My New Post"
```
然后使用  hexo g (generate) && hexo d (deploy)




### 每次修改完博客后，可以用以下命令重新部署到远程网站: 

``` bash
$ hexo clean (可不使用) && hexo g (generate) && hexo d (deploy)
```

## 如何安装和卸载hexo插件

### 安装插件
``` bash
$  npm install 插件名  --save
```
其中，插件名均以“hexo-”开头，Hexo会自动加载有此前缀的插件，而没有该前缀的插件是不会被自动识别的。--save参数告诉npm将插件名记录在网站目录的package.json里，以便于直接使用npm install（不带参数）更新或直接安装.

### 卸载插件
``` bash
$ npm list & npm uninstall 插件名  --save
```
然后删除相关配置和文件： 配置文件中有PLugins模块，删除对应的插件设置； 删除node
_modules/ 目录下对应的插件文件. 加上--save参数后，存储在package.json中的插件信息也会被移除；如果不加此参数，那么下次使用npm install安装时该插件还会被装上.

### 更换使用next主题时可能遇到的问题

#### 更换主题后，使用hexo g 命令后出现no layout...的问题如何解决？

比如使用next主题，先在终端控制台cd到博客主题（/themes）目录下，然后输入git clone https://github.com/next-theme/hexo-theme-next按下回车键，然后在本地文件夹中把hexo-theme-next文件夹修改成next, 并在站点的配置文件(不是next主题的配置文件)
_config.yml中将theme那一栏由landscape换成next.

#### 例: 安装latex相关插件及配置
``` bash
$  npm install hexo-filter-mathjax  --save
```
详情可参考(https://weilining.github.io/261.html)
为了修复Hexo和Mathjax的冲突，可以进行以下操作：
``` bash
$  npm uninstall hexo-renderer-marked  --save
$  npm  install  hexo-renderer-kramed  --save
```

为了在博客上显示（渲染）latex 环境，需要安装插件  hexo-renderer-pandoc， 而在此之前需要安装Pandoc. 安装完成后记得电脑重启一下，不然hexo g 后一直提示 pandoc exited with code null的. 然后在Hexo 项目的_config.yml 文件中，添加或修改以下配置:
``` bash
$ pandoc:
$   pandoc_path: 你的Pandoc 安装路径 (比如:C:/Users/ll/AppData/Local/Pandoc/    $  pandoc.exe)
$   args:    
$    - "--mathjax"
```
Hexo randerer pandoc 使用教程可参考(https://blog.csdn.net/gitblog_00216/article/details/141763934). 



#### 使用next主题，在themes/next/_config.yml 进行配置,开启 MathJax 渲染引擎: 

```bash
# MathJax
math:
  engine: 'mathjax'
  mathjax:
    src: https://cdnjs.cloudflare.com/ajax/libs/mathjax/2.7.4/MathJax.js?config=TeX-MML-AM_CHTML 
```bash
可参考(https://cps.ninja/2019/03/16/hexo-with-latex/).


Next主题可能依赖于某些插件或组件，确保这些依赖已经正确安装。例如，Next主题可能需要hexo-renderer-swig渲染器，可以通过以下命令安装：







## Hexo的常用命令


### Clean: hexo clean
该命令会删除整个***.github.io/public/文件夹. hexo clean这个命令其实很少用。使用情况常见于：更新了_config.yml文件夹，删除了一些已有博文等。原因就是速度慢，耗费不必要的时间。毕竟它会将整个public/文件夹删除，再重新生成。推荐偶尔清理使用即可。

### Generate: hexo generate
或者简写为hexo g。该命令会生成静态文件夹public/，也就是从markdown到网页文件html等的转换操作

### Server: hexo server
启动服务器常用的是hexo server或者简写为hexo s。
若需指定端口号则为hexo server -p 50005000可以更改为其他端口号。
该命令会把生成好的静态文件部署到本地的指定端口，之后即可在本地浏览器输入localhost:4000即可预览。若指定了端口号，则把4000改为你指定的端口，如上个示例中的localhost:5000

### deploy：hexo deploy
或者简写为hexo d。该命令将网站部署到服务器上。实际操作是：更新你在github上的仓库 .../github.io的指定分支（如果你采用Hexo系列第一节说到的两分支方式的话）。这是你最终发表的博客页面，你可以在浏览器上访问https://...github.io来查看更新后的博客啦。



在本地预览时，你仍可以更改markdown文件中一般的文字内容，然后直接在浏览器端刷新页面，就能看到实时更改的效果，而不需要再执行一次hexo g; hexo s，节省很多时间。常用于预览过程中进行微调操作。我的测试表明，此时更改文章的categories, tags等Front-Matter的属性的话，也可以动态刷新，很神奇。

但是，有些涉及到更深层次的操作，比如利用到themes文件里的js函数，css样式，文件链接等，可能无法实时更新。此时仍需要重新generate才可以预览最新效果。同理，如果你更改了themes文件夹下面的css文件, ejs文件, yml文件等，通常也需要重新渲染。

注意：在执行hexo s之后，想要中断操作，使用的是control + C快捷键。

### 其他命令

  help     获取帮助；

  init      新建一个Hexo 文件夹;

  list      列出网站信息清单 
  
  publish   将draft post  从 _drafts 文件夹转移到to _posts文件夹.

  render    Render files with renderer plugins.
  
  version   展示版本信息.


### 全局命令
Global Options:
  --config  Specify config file instead of using _config.yml
  --cwd     Specify the CWD
  --debug   Display all verbose messages in the terminal
  --draft   Display draft posts
  --safe    Disable all plugins and scripts
  --silent  Hide output on console
