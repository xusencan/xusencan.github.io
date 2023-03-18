[Hexo](http://yiwangmeng.com/)是一个快速、简洁且高效的博客框架，支持 `Markdown` 的绝大部分功能；具有超快生成速度，让数百个 `MarkDown` 源文件在几秒内快速渲染成全站 `HTML` 页面；还拥有各式各样的插件支持功能扩展。

但是就像很多教程里面写的那样，搭建 Hexo 本地环境，需要安装 `Node.js`、`Git` 以及使用 `npm` 进行安装和配置。这对于毫无经验的新手来说，是一个很大的挑战。同时，由于这些环境的存在，导致如果需要更换计算机的时候，重新安装配置一个新的Hexo环境，又得花费一些功夫。

所以呢，我们整合了一个 Hexo 便携版，来简化本地环境的部署，这就是我们的GoodHexo。

![](https://cdn.jsdelivr.net/gh/828767/static/images/GoodHexo.png)

- 当你重装系统后，只要GoodHexo目录还在，直接接着用即可；
- 当你想换个电脑，只需要将GoodHexo目录移到新电脑上即可。甚至，你可以将这个文件夹装到U盘里，走哪插哪就行。

# 软件介绍
那么所谓的便携版到底是什么？便携版就是将 Hexo 本地环境所需要的各种依赖环境的整合到一起，做成不需要安装的版本。

本便携版当前版本所包含的软件如下：

程序       |     版本    |     更新时间
---       |     ---     |    ---
Git       |     2.7.4   |   2020-7-18
Nodejs    |     12.16.2 |   2020-7-18
Npm       |     6.14.4  |   2020-7-18
Hexo      |     5.1.1   |   2020-8-27
Hexo-cli  |     4.2.0   |   2020-8-27


> 适用平台：**Microsoft Windows**
> 关键词： **GoodHexo**，**Hexo绿色版**，**Hexo便携版**，**Hexo配置**，**Hexo**，**U盘携带**，**GitHub Hexo**


为了便携的需要，不能配置固定的环境变量，所以除此之外还有相应的批处理脚本，下文将详细介绍。

# 从零开始，一分钟使用 GoodHexo 写作环境
说了这么多，我们这就开始教你如何在1分钟内，从零开始使用 GoodHexo 写作环境！

## 认识文件目录
该订制的GoodHexo便携包基本上已经包含了Hexo博客所需的所有依赖，**添加新主题新功能如果缺依赖请按照主题文档去安装**更新即可。
上面的**压缩包下载解压**后，其目录结构如下：
```
GOODHEXO #便携包根目录
|   1.新建文章.bat  #要新建文章运行此批处理，填文件名建议别用中文
|   2.本地测试.bat  #写完文章可以启动本地服务端测试预览效果
|   3.渲染并部署.bat #确定文章写完了，那么就运行此批处理发布
|   启动命令行.bat #给有经验的人用，直达bash界面
|   清理旧文件后部署.bat  #部署也没报错，但博客就是没更新或者其他异常，那么用这个来部署试试
|   
+---hexo    #hexo程序工作目录
|   |   .gitignore  #指定Git提交时忽略的文件规则，一般也不要动
|   |   db.json  #程序自动生成的，不要动
|   |   package.json  #不要动
|   |   _config.yml  #hexo的主配置文件，定义标题，作者，导航菜单等
|   |   
|   +---node_modules  #hexo的依赖环境，不要动
|   +---scaffolds  #文章/页面/草稿模板，不会就不要动
|   +---source  #网站根目录
|   |   README.md #本便携包示例文档
|   |   \---images  #图片资源，网站路径为：/images
|   |   |   GoodHexo.png  #图片引用地址为：/images/GoodHexo.png，也可以：../images/GoodHexo.png
|   |   \---_posts  #你所有的文章都存在这个目录底下，通过批处理新建文章会自动建到这个目录下
|   |   |   hello-world.md  #示例文章源文件，该MarkDown文件会被hexo渲染成HTML页发布
|   |   
|   +---themes  #主题存放目录
|   |   \---landscape #默认主题
|   |   
|       
\---support #便携程序包，包含nodejs和Git环境，不要动
```

## 开始使用

### 详细个性化设置

拿到这个便携包，一些基础配置和基本的主题设置等院长都已经给你做好了，只需要自行对博客网站进行个性化详细设置即可。

个性化设置主要有两个地方：
1. Hexo目录下的 `_config.yml` ，详见相应的参数注释，按要求填写，不想写就默认
2. 主题目录下的 `_config.yml` ，主题不同设置项不同，所以请参考主题对应的文档进行修改设置

依次打开就能看个大概了，根据自己的需要及主题帮助完成自己要的个性化设置。更深入的个性化基本上需要在主题上做文章，请自行查看主题帮助，或者研究主题源代码即可完成。

修改的时候请注意格式，否则会导致错误而无法正常使用，比如 `:` 一定要是英文的且后面有内容的话至少要跟一个空格，配置内容跟后面的 `#` 注释之间至少要有一个空格，具体错误可以启动命令行输入 `hexo s --debug` 查看。

![网站配置](https://cdn.jsdelivr.net/gh/828767/static/images/goodhexo_config_site.png)

上图就是一个网站配置示例，配置项 `:` 后面**如果要添加值至少带了一个空格**，值带中文或者特殊符号建议用英文引号 `''` 引起来，一行以 `#` 开头表示注释内容，配置项后面加空格再 `#` 则后面部分才是注释，如下面一个配置项：
```
keywords: '一网盟,yiwangmeng,GoodHexo,hexo便携版' #网站SEO关键词，多个词用英文逗号区隔
```

### 写一篇自己的文章
设置好后，就可以开始动手写自己的文章了。

#### step1.新建文章
运行 `1.新建文章.bat` ，按提示填写文章名称，建议不要使用中文。

![](https://cdn.jsdelivr.net/gh/828767/static/images/hexo-new.gif)

回车确认后会在 `hexo` 目录下的对应目录新建个 `.md` 文件，文件名以刚才输入的文章名称命名，注意提示的文件路径和新创建的文件名，如： `hexo\source\_posts\helloworld.md`

#### step2. 编辑文章MarkDown文件
使用任意文本编辑器打开你刚新建的文章MarkDown源文件，按约定格式修改 `Front-matter` 中参数值，以及在 `Front-matter` 之后写你想写的内容即可，推荐编辑器首选用vscode或者Atom，关于编辑器以下文章可以阅读下：
1. [vscode-跨平台，绿色免费，基本接近完美的编辑器](https://code.visualstudio.com/)
2. [MarkDown编辑器推荐这篇文章](#)
3. [typora - 所见即所得MarkDown编辑器，推荐小白用这个](https://typora.io/)
4. [基于Moeditor修改集成Hexo功能的编辑器](https://github.com/zhuzhuyule/HexoEditor)

如果不依赖MarkDown编辑器，那么你需要掌握基本的MarkDown语法，然后就可以用任意文本编辑器「当然，Windows系统自带的记事本还是不推荐用」，按MarkDown语法写文档了。
MarkDown语法可以参考 [这个 Markdown 教程](http://xianbai.me/learn-md/article/about/readme.html)。

**需要额外注意的是**：Hexo对MarkDown文档头有规范，就是在文档最开始两个 `---` 中间的那部分，官方称之为 `Front-matter`

```
---
title: 'Hexo，从此开始...'  #文章标题，新建文章的时候填的会自动写到这里
date: 2018-1-12 17:19:27  #文章创建时间
categories: 搞软件 #分类，也可以如下一行那种换行后写分类
tags:  #标签
  - 晒酷软  #这是个标签
  - 做网站  #这是另一个标签
toc: true  #是否显示目录，false不显示，true显示，需要主题支持
top:  #填数字，值越大的文章在首页就越置顶，本包已集成
comments: true  #是否允许评论，需要主题支持
keywords: ''    #文章关键词，需要主题支持
description:  '文章摘要，可以是一大段，
可以换行，用英文引号括起来'  #不填则根据主题设计截取对应字数
---
上面部分是规定的头部信息，这行开始就是文章内容了...
```

对于文章来说，以上 `Front-matter` 参数除了 `title:` 都不是必须的，请根据自己的需求填写。
> **注意：每一个参数的 `:` 或者 `-` 后，都需要至少留一个空格，如果不填值就无所谓，或者将参数行删除都行，就是不能不留空格直接写，否则会报错。**

如果参数值中间涉及特殊字符或者空格等，请使用英文的单引号 `''` 将你的内容括起来，就如上面的示例一样。

更多 `Front-matter` 参数详见官方文档：https://hexo.io/zh-cn/docs/front-matter.html

文章参数设置完后，就可以在 `---` 下一行写自己想写的任何内容了，以下都属于你文章的内容。

![](https://cdn.jsdelivr.net/gh/828767/static/images/hexo-edit.gif)

#### step3.渲染并发布
文章写好保存，那就运行 `3.渲染并部署.bat` ，该批处理会将你的MarkDown源文件套用主题模板渲染成HTML静态页，并把静态页部署到网站空间，最后提示 `deploy done：git` 就表示已部署完成，要不了两分钟，访问你的网站地址就能看到效果了。

以上步骤请仔细阅读，再写新文章，重复以上步骤即可。

### 文章增/删/改
- 增：也就是新建文章，请按前一章第1、2、3步执行
- 删：删除一篇文章、页面或图片资源等，只需要将MarkDown等源文件删除，然后执行渲染并发布即可
- 改：也就是前一章的第2、3步
- 疑难杂症：有时候因为缓存或者一些莫名其妙的未知问题，可以尝试运行 `清理旧文件后部署.bat`

> 实际上任何增删改都需要重新渲染发布，等线上缓存更新完了才能在外网看到更改后的效果

新手在使用过程中可能会遇到一些问题，请参考我们整理的：[GoodHexo使用常见问题及解决办法](http://yiwangmeng.com/?p=90)。

# 进阶

如果你喜欢折腾，Hexo进阶部署使用可以参考[Hexo博客Git-VPS部署完整记录](http://yiwangmeng.com/?p=92)。

使用过程中如需帮助，欢迎关注微信公众号，淘宝店，我的博客或者加入我们的交流群。

<div style="float:left;border:solid 1px 000;margin:2px;"><img src="https://cdn.jsdelivr.net/gh/828767/static/images/QR-atm.png"  width="200" height="260" ></div>

<div style="float:left;border:solid 1px 000;margin:2px;"><img src="https://cdn.jsdelivr.net/gh/828767/static/images/QR-Taobao.png" width="200" height="260" ></div>

<div style="float:left;border:solid 1px 000;margin:2px;"><img src="https://cdn.jsdelivr.net/gh/828767/static/images/QR-QQ-260489333.png" width="200" height="260" ></div>
<div style="float:none;clear:both;"></div>

# 备注
>- 本文所有权归 [一网盟](http://yiwangmeng.com) 所有，[原文在此](http://yiwangmeng.com/?p=91)；
>- 本便携版由 [一网盟](http://yiwangmeng.com) 维护并提供技术支持；
