title: 最全Hexo博客搭建+主题优化+插件配置+常用操作+错误分析（  转）
author: 洛克
tags:
  - 'hexo '
  - ''
  - 学习
categories:
  - 技术
date: 2019-07-31 12:53:00
---
【持续更新】最全Hexo博客搭建+主题优化+插件配置+常用操作+错误分析
- https://www.simon96.online/2018/10/12/hexo-tutorial/

前言

    欢迎在文末留言，或者点击加入QQ群933583982互相交流。
    本文采用 CC BY-NC-SA 4.0 许可协议，转载请注明出处！

博客搭建
准备环境

    Node.js 下载，并安装。详细步骤：https://www.simon96.online/2018/11/10/hexo-env/

    Git 下载，并安装。详细步骤：https://www.simon96.online/2018/11/10/hexo-env/

    安装Hexo，在命令行（即Git Bash）运行以下命令：

        npm install -g hexo-cli

    初始化Hexo，在命令行（即Git Bash）依次运行以下命令即可：

    以下，即存放Hexo初始化文件的路径， 即站点目录。

$ hexo init <folder>
$ cd <folder>
$ npm install

新建完成后，在路径下，会产生这些文件和文件夹：

    .
    ├── _config.yml
    ├── package.json
    ├── scaffolds
    ├── source
    |   ├── _drafts
    |   └── _posts
    └── themes

    注：

        hexo相关命令均在站点目录下，用Git Bash运行。

        站点配置文件：站点目录下的_config.yml。

        ​ 路径为<folder>\_config.yml

        主题配置文件：站点目录下的themes文件夹下的，主题文件夹下的_config.yml。

        ​ 路径为<folder>\themes\<主题文件夹>\_config.yml

    启动服务器。在路径下，命令行（即Git Bash）输入以下命令，运行即可：

        hexo server

    浏览器访问网址： http://localhost:4000/

至此，您的Hexo博客已经搭建在本地。
实施方案
方案一：GithubPages

    创建Github账号

    创建仓库， 仓库名为：<Github账号名称>.github.io

    将本地Hexo博客推送到GithubPages

    3.1. 安装hexo-deployer-git插件。在命令行（即Git Bash）运行以下命令即可：

$ npm install hexo-deployer-git --save

3.2. 添加SSH key。

    创建一个 SSH key 。在命令行（即Git Bash）输入以下命令， 回车三下即可：

$ ssh-keygen -t rsa -C "邮箱地址"

添加到 github。 复制密钥文件内容（路径形如C:\Users\Administrator\.ssh\id_rsa.pub），粘贴到New SSH Key即可。

测试是否添加成功。在命令行（即Git Bash）依次输入以下命令，返回“You’ve successfully authenticated”即成功：

    $ ssh -T git@github.com
    $ yes

3.3. 修改_config.yml（在站点目录下）。文件末尾修改为：

# Deployment
## Docs: https://hexo.io/docs/deployment.html
deploy:
  type: git
  repo: git@github.com:<Github账号名称>/<Github账号名称>.github.io.git
  branch: master

注意：上面仓库地址写ssh地址，不写http地址。

3.4. 推送到GithubPages。在命令行（即Git Bash）依次输入以下命令， 返回INFO Deploy done: git即成功推送：

    $ hexo g
    $ hexo d

    等待1分钟左右，浏览器访问网址： https://<Github账号名称>.github.io

至此，您的Hexo博客已经搭建在GithubPages, 域名为https://<Github账号名称>.github.io。
方案二：GithubPages + 域名

在方案一的基础上，添加自定义域名（您购买的域名）。

    域名解析。

    类型选择为 CNAME；

    主机记录即域名前缀，填写为www；

    记录值填写为<Github账号名称>.github.io；

    解析线路，TTL 默认即可。

    仓库设置。

    2.1. 打开博客仓库设置：https://github.com/<Github账号名称>/<Github账号名称>.github.io/settings

    2.2. 在Custom domain下，填写自定义域名，点击save。

    2.3. 在站点目录的source文件夹下，创建并打开CNAME.txt，写入你的域名（如www.simon96.online），保存，并重命名为CNAME。

    等待10分钟左右。

    浏览器访问自定义域名。

    至此，您的Hexo博客已经解析到自定义域名，https://<Github账号名称>.github.io依然可用。

方案三：GithubPages + CodingPages + 域名

GithubPages 在国内较慢，百度不收录，而CodingPages 在国外较快。所以在方案二的基础上，添加CodingPages 。

    创建Coding账号

    创建仓库， 仓库名为：<Coding账号名称>

    进入项目里『代码』页面，点击『一键开启静态 Pages』，稍等片刻CodingPages即可部署成功。

    将本地Hexo博客推送到CodingPages

    4.1. 鉴于创建GithubPages 时，已经生成过公钥。可直接复制密钥文件内容（路径形如C:\Users\Administrator\.ssh\id_rsa.pub）， 粘贴到新增公钥。

    4.2. 测试是否添加成功。在命令行（即Git Bash）依次输入以下命令，返回“You’ve successfully authenticated”即成功：

$ ssh -T git@git.coding.net
$ yes

4.3. 修改_config.yml（在存放Hexo初始化文件的路径下）。文件末尾修改为：

# Deployment
## Docs: https://hexo.io/docs/deployment.html
deploy:
- type: git
  repo: git@github.com:<Github账号名称>/<Github账号名称>.github.io.git
  branch: master
- type: git
  repo: git@git.dev.tencent.com:<Coding账号名称>/<Coding账号名称>.git
  branch: master

4.4. 推送到GithubPages。在命令行（即Git Bash）依次输入以下命令， 返回INFO Deploy done: git即成功推送：

    $ hexo g
    $ hexo d

    域名解析

        添加 CNAME 记录指向 <Coding账号名称>.coding.me

        类型选择为 CNAME；

        主机记录即域名前缀，填写为www；

        记录值填写为<Github账号名称>.coding.me；

        解析线路，TTL 默认即可。

        添加 两条A 记录指向 192.30.252.153和192.30.252.154

        类型选择为 A；

        主机记录即域名前缀，填写为@；

        记录值填写为192.30.252.153和192.30.252.154；

        解析线路，境外或谷歌。

        在『Pages 服务』设置页（https://dev.tencent.com/u/<Coding账号名称>/p/<Coding账号名称>/git/pages/settings）中绑定自定义域名。

至此，您的Hexo博客已经解析到自定义域名，https://<Github账号名称>.github.io和https://<Coding账号名称>.coding.me依然可用。
主题优化
选择主题

Hexo默认的主题是landscape，推荐以下主题：

    snippet
    Hiero
    JSimple
    BlueLake

详见：https://github.com/search?q=hexo-theme
应用主题

    下载主题
    将下载好的主题文件夹，粘贴到站点目录的themes下。
    更改站点配置文件_config.yml 的theme字段，为主题文件夹的名称：

# Extensions
## Plugins: https://hexo.io/plugins/
## Themes: https://hexo.io/themes/
theme: <主题文件夹的名称>

主题优化

以上主题都有比较详细的说明文档，本节主要解决主题优化的常见问题。

主题优化一般包括：

    设置「RSS」

    添加「标签」页面

    添加「分类」页面

    设置「字体」

    问题：引用国外字体镜像较慢。

    解决：可以改用国内的。将\themes\*\layout_partials\head external-fonts.swig文件中fonts.google.com改成fonts.lug.ustc.edu.cn。

    设置「代码高亮主题」

    侧边栏社交链接

    问题：图标哪里找？

    解决：Font Awesome

    开启打赏功能

    问题：微信支付宝二维码不美观，规格不一。

    解决：在线生成二维码

    设置友情链接

    腾讯公益404页面

    站点建立时间

    订阅微信公众号

    设置「动画效果」

    问题：慢，需要等待 JavaScript 脚本完全加载完毕后才会显示内容。
    解决：将主题配置文件_config.yml中，use_motion字段的值设为 false 来关闭动画。

    设置「背景动画」

主题优化还包括：
添加背景图

在 themes/*/source/css/_custom/custom.styl 中添加如下代码：

body{
    background:url(/images/bg.jpg);
    background-size:cover;
    background-repeat:no-repeat;
    background-attachment:fixed;
    background-position:center;
}

修改Logo字体

在 themes/*/source/css/_custom/custom.styl 中添加如下代码：

@font-face {
    font-family: Zitiming;
    src: url('/fonts/Zitiming.ttf');
}
.site-title {
    font-size: 40px !important;
	font-family: 'Zitiming' !important;
}

其中字体文件在 themes/next/source/fonts 目录下，里面有个 .gitkeep 的隐藏文件，打开写入你要保留的字体文件，比如我的是就是写入 Zitiming.ttf ，具体字库自己从网上下载即可。
修改内容区域的宽度

编辑主题的 source/css/_variables/custom.styl 文件，新增变量：

// 修改成你期望的宽度
$content-desktop = 700px

// 当视窗超过 1600px 后的宽度
$content-desktop-large = 900px

网站标题栏背景颜色

打开 themes/*/source/css/_custom/custom.styl ,在里面写下如下代码：

.site-meta {
  background: $blue; //修改为自己喜欢的颜色
}

自定义鼠标样式

打开 themes/*/source/css/_custom/custom.styl ,在里面写下如下代码：

// 鼠标样式
  * {
      cursor: url("http://om8u46rmb.bkt.clouddn.com/sword2.ico"),auto!important
  }
  :active {
      cursor: url("http://om8u46rmb.bkt.clouddn.com/sword1.ico"),auto!important
  }

文章加密访问

打开 themes/*/layout/_partials/head.swig文件,在 之前插入代码：

<script>
    (function(){
        if('{{ page.password }}'){
            if (prompt('请输入密码') !== '{{ page.password }}'){
                alert('密码错误');
                history.back();
            }
        }
    })();
</script>

写文章时加上password: *：

---
title: 2018
date: 2018-10-25 16:10:03
password: 123456
---

实现点击出现桃心效果

    在/themes/*/source/js/src下新建文件click.js，接着把以下粘贴到click.js文件中。
    代码如下：

!function(e,t,a){function n(){c(".heart{width: 10px;height: 10px;position: fixed;background: #f00;transform: rotate(45deg);-webkit-transform: rotate(45deg);-moz-transform: rotate(45deg);}.heart:after,.heart:before{content: '';width: inherit;height: inherit;background: inherit;border-radius: 50%;-webkit-border-radius: 50%;-moz-border-radius: 50%;position: fixed;}.heart:after{top: -5px;}.heart:before{left: -5px;}"),o(),r()}function r(){for(var e=0;e<d.length;e++)d[e].alpha<=0?(t.body.removeChild(d[e].el),d.splice(e,1)):(d[e].y--,d[e].scale+=.004,d[e].alpha-=.013,d[e].el.style.cssText="left:"+d[e].x+"px;top:"+d[e].y+"px;opacity:"+d[e].alpha+";transform:scale("+d[e].scale+","+d[e].scale+") rotate(45deg);background:"+d[e].color+";z-index:99999");requestAnimationFrame(r)}function o(){var t="function"==typeof e.onclick&&e.onclick;e.onclick=function(e){t&&t(),i(e)}}function i(e){var a=t.createElement("div");a.className="heart",d.push({el:a,x:e.clientX-5,y:e.clientY-5,scale:1,alpha:1,color:s()}),t.body.appendChild(a)}function c(e){var a=t.createElement("style");a.type="text/css";try{a.appendChild(t.createTextNode(e))}catch(t){a.styleSheet.cssText=e}t.getElementsByTagName("head")[0].appendChild(a)}function s(){return"rgb("+~~(255*Math.random())+","+~~(255*Math.random())+","+~~(255*Math.random())+")"}var d=[];e.requestAnimationFrame=function(){return e.requestAnimationFrame||e.webkitRequestAnimationFrame||e.mozRequestAnimationFrame||e.oRequestAnimationFrame||e.msRequestAnimationFrame||function(e){setTimeout(e,1e3/60)}}(),n()}(window,document);

    在\themes\*\layout\_layout.swig文件末尾添加：

<!-- 页面点击小红心 -->
<script type="text/javascript" src="/js/src/clicklove.js"></script>

静态资源压缩

在站点目录下：

$ npm install gulp -g

安装gulp插件：

npm install gulp-minify-css --save
npm install gulp-uglify --save
npm install gulp-htmlmin --save
npm install gulp-htmlclean --save
npm install gulp-imagemin --save

在 Hexo 站点下新建 gulpfile.js文件，文件内容如下：

var gulp = require('gulp');
var minifycss = require('gulp-minify-css');
var uglify = require('gulp-uglify');
var htmlmin = require('gulp-htmlmin');
var htmlclean = require('gulp-htmlclean');
var imagemin = require('gulp-imagemin');
// 压缩css文件
gulp.task('minify-css', function() {
  return gulp.src('./public/**/*.css')
  .pipe(minifycss())
  .pipe(gulp.dest('./public'));
});
// 压缩html文件
gulp.task('minify-html', function() {
  return gulp.src('./public/**/*.html')
  .pipe(htmlclean())
  .pipe(htmlmin({
    removeComments: true,
    minifyJS: true,
    minifyCSS: true,
    minifyURLs: true,
  }))
  .pipe(gulp.dest('./public'))
});
// 压缩js文件
gulp.task('minify-js', function() {
    return gulp.src(['./public/**/.js','!./public/js/**/*min.js'])
        .pipe(uglify())
        .pipe(gulp.dest('./public'));
});
// 压缩 public/demo 目录内图片
gulp.task('minify-images', function() {
    gulp.src('./public/demo/**/*.*')
        .pipe(imagemin({
           optimizationLevel: 5, //类型：Number  默认：3  取值范围：0-7（优化等级）
           progressive: true, //类型：Boolean 默认：false 无损压缩jpg图片
           interlaced: false, //类型：Boolean 默认：false 隔行扫描gif进行渲染
           multipass: false, //类型：Boolean 默认：false 多次优化svg直到完全优化
        }))
        .pipe(gulp.dest('./public/uploads'));
});
// 默认任务
gulp.task('default', [
  'minify-html','minify-css','minify-js','minify-images'
]);

只需要每次在执行 generate 命令后执行 gulp 就可以实现对静态资源的压缩，压缩完成后执行 deploy 命令同步到服务器：

hexo g
gulp
hexo d

修改访问URL路径

默认情况下访问URL路径为：domain/2018/10/18/关于本站,修改为 domain/About/关于本站。 编辑 Hexo 站点下的 _config.yml 文件，修改其中的 permalink字段：

permalink: :category/:title/

博文置顶

    安装插件

    $ npm uninstall hexo-generator-index --save
    $ npm install hexo-generator-index-pin-top --save

然后在需要置顶的文章的Front-matter中加上top即可：

---
title: 2018
date: 2018-10-25 16:10:03
top: 10
---

    设置置顶标志

打开：/themes/*/layout/_macro/post.swig，定位到
，插入以下代码即可：

{% if post.top %}
  <i class="fa fa-thumb-tack"></i>
  <font color=7D26CD>置顶</font>
  <span class="post-meta-divider">|</span>
{% endif %}

在右上角或者左上角实现fork me on github

    选择样式GitHub Ribbons,
    修改图片跳转链接,将<a href="https://github.com/you">中的链接换为自己Github链接：
    打开 themes/next/layout/_layout.swig 文件，把代码复制到<div class="headband"></div>下面。

主页文章添加边框阴影效果

打开 themes/*/source/css/_custom/custom.styl ,向里面加代码:

// 主页文章添加阴影效果
.post {
   margin-top: 0px;
   margin-bottom: 60px;
   padding: 25px;
   -webkit-box-shadow: 0 0 5px rgba(202, 203, 203, .5);
   -moz-box-shadow: 0 0 5px rgba(202, 203, 204, .5);
}

显示当前浏览进度

修改themes/*/_config.yml，把 false 改为 true：

# Back to top in sidebar
b2t: true

# Scroll percent label in b2t button
scrollpercent: true

创建分类页

在终端窗口下，定位到 Hexo 站点目录下，新建：

$ cd <站点目录>
$ hexo new page categories

